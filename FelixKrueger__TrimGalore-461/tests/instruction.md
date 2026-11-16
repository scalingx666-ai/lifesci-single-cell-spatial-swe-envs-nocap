# Issue

**Title:** fix(cli): stop refusing --rename over a clip flag that applies to no read

## Description

.

A single-end `--rename --output-format ubam --clip_R2 5` run warned that `--clip_R2` was being ignored and then refused the run because `--clip_R2` was set. The #408 guard counted all four clip values, including a Read 2 flag that reaches no read on a single-end run. It now counts only flags that apply to the run's shape, so that run proceeds with the warning; every other refusal is unchanged. Along the way, "which read does a clip flag belong to" moves from six open-coded sites into one `ClipFlag` enum, which is what the duplication had already cost us once.

`--help` and both statements of the gate in `docs/guide/outputs.md` said "when a clipping flag is set", which this makes inaccurate, so all three are updated.

<details>
<summary>Implementation and verification detail (AI-assisted)</summary>

**Why the narrowing is safe.** The guard's own comment stated the criterion it meant to apply — the clip-flag list must match every `--rename`-driven `append_to_id` site, "without one of them set, `--rename` appends nothing and there is nothing to lose". `trim_read` picks the clip value by `is_r2`, and the three production call sites passing `true` (`trimmer.rs` `run_paired_end` and `run_paired_end_to_bam`, `parallel.rs` `classify_paired`) are all gated on `cli.paired`, so on a single-end run no Read 2 value is read and no append site can fire.

That absence is *categorical*, which is the boundary of the change. The guard stays conservative about the statistical case: `clip_5prime` returns `None` when a read is shorter than the clip, so even a live Read 1 flag appends nothing for some reads, and the refusal is deliberately whole-run rather than per-record because of it. It is also the principle `rename_without_clip_flag_is_accepted_into_ubam` already established.

**The fold-in.** `ClipFlag::applies(paired)` replaces four hand-written spellings of `paired || !read_2`: `flag_summary`'s skip, the inert-flag warning ladder, the #408 guard, and the override-line filters in `main.rs` and `report.rs`. `ClipOverride` carries a `ClipFlag` rather than a `&'static str` plus a separate bool, so a wrong read-ownership bool is unrepresentable rather than merely tested. Only the guard changes behaviour.

Each display site keeps its own emission order, because the two differ and are both user-visible (`flag_summary`: R1, R2, 3'R1, 3'R2; the ladder: R1, 3'R1, R2, 3'R2). `ClipFlag::ALL` is deliberately in neither order, so no display site can iterate it and still look correct.

**Verification.** 788 tests (7 new), `fmt` and `clippy --all-targets --release -D warnings` clean.

- A 27-cell base-vs-new differential over 102 artifacts (stderr plus both trimming reports) has exactly one differing cell — the #450 shape. Each cell asserts it emitted a warning, a preset banner or the refusal before comparing, so a cell cannot pass by comparing two identical error messages.
- Four mutations, each red at its target: counting Read 2 regardless of `paired` turns the two new "must run" rows red; dropping the `paired ||` narrowing turns the paired "must refuse" rows red; flipping `read_2()` for `ClipR2` or for `ThreePrimeClipR1` turns the ownership oracle red, the latter also turning the `--three_prime_clip_R1` row red. The first two fail disjoint test sets, which is what shows they are opposite mutations rather than one.
- All twelve rows of the refusal truth table now have a test. `--three_prime_clip_R1` had none before — `grep -c` in `integration_ubam_out.rs` returns 0 at the base commit and 1 now.

**Two things deliberately not fixed.** `--rrbs` reaches the same append site without setting a clip flag, because `setup_trimming` sets `clip_r2 = 2` after the guard runs — an under-refusal in the opposite direction, filed as #459. And `--clip_R1 0` still triggers the refusal though a zero value can never append.

**Not held by any test:** the guard's siting after the two structural pair checks in `main()`, which is what makes a mixed-format pair report its own defect rather than this refusal. `Validate vs Perl TrimGalore` is the job to watch here, since `Cli::validate()` is edited.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc48bf0d2cf1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.