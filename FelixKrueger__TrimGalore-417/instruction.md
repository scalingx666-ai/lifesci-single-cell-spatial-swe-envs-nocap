# Issue

**Title:** fix(main): refuse --rename into uBAM where the annotation cannot be represented

## Description

`--rename` appends `:clip5:SEQ`/`:clip3:SEQ` to the **end** of the read ID — matching Perl v0.6.11, which does the same at all eleven of its append sites. On FASTQ input that puts the annotation after any header description, and BAM read names cannot contain whitespace, so the tail is discarded and the explicitly-requested annotation goes with it. `--rename --output-format ubam` on a header like `@read 1:N:0:ACGTAC` produced the QNAME `read` and nothing else. That combination is now refused when at least one input is FASTQ **and** a clipping flag is set.

The clip-flag half of that condition matters: `--rename` reaches `append_to_id` only under `--clip_R1/R2`, `--three_prime_clip_R1/R2` or `--hardtrim5/3`, so on its own it appends nothing and is still accepted. A wrapper that threads `--rename` unconditionally alongside an optional `--clip_R1` keeps working in its no-clip configuration. All six flags were read off the call sites (`trimmer.rs:264`/`273`, `specialty.rs:62`/`106`/`166`/`219`) rather than inferred, so the list cannot let a lossy run through.

**Format-gated, not blanket.** uBAM input is lossless by SAM spec rather than by luck: a BAM read name cannot carry whitespace, so a record read from uBAM has no description, and `append_to_id` splices before the first TAB (code-review C1) so the aux-tag tail survives and the annotation lands on the name. Refusing that would withdraw a working path and would have broken the C1 regression guard at `tests/integration_ubam_out.rs:393`, which asserts this exact combination **succeeds** on uBAM input. That test is untouched.

The gate lives in `main.rs` rather than `cli.rs` §3.4a because it needs `input_formats`, which `Cli::validate()` cannot see. It sits behind the two structural pair checks, so `--paired` with a single FASTQ, or a mixed FASTQ+uBAM pair, still reports its own defect — including #363's deliberate "check for a mis-typed filename" hint — rather than a lecture about `:clip5:` representability for a run that is broken independently of `--rename`. Still ahead of `ensure_output_dir` and every dispatch arm: a refused run creates nothing, not even an absent `-o` directory. `--clump_only` keeps its own byte-identity message, and `--hardtrim5`/`--hardtrim3` are covered.

The message describes a format-level refusal and says why it is deliberately coarser than the loss — whether a given header loses the annotation is a per-record property, and deciding per record would mean failing part-way through a BAM. It does not claim impossibility (a description-free FASTQ honours the flag exactly), does not say "silently dropped" (#406 already prints a `NOTE` echoing the dropped text), and does not suggest converting afterwards, because `samtools import` drops the description identically, with and without `-T '*'`.

Also folded in: the output guide described `--rename` as "`--rename PREFIX` replaces the input filename stem in the output names", wrong in every clause. That is `--basename`, which had no dedicated section in the output guide; both now have accurate ones, including `--basename`'s two real limits — reports keep input-derived names, and the specialty modes ignore it entirely. The uBAM compatibility list gains `--rename`, and its preamble moves from "Rejected at CLI-validate time" to "Rejected at startup" — true of all eight entries rather than seven. `--rename`'s own `--help` now names both restrictions it is subject to.

Eight integration tests, 578 total, up from 570. Both refusals were run against an **unpatched build** first, where they succeed and lose the annotation.

Two follow-ups filed from the review, neither a regression here: #415 (a spec-violating uBAM QNAME silently drops preserved aux tags — the one hole in the assumption this gate rests on) and #416 (carry the annotation as an aux tag, which would let this refusal be lifted).

<details>
<summary>AI-assisted: what the dual code review changed, and three harness false-greens caught on the way</summary>

**The dual code review moved three things.** Both reviewers approved with no Critical or High, and both verified the mechanism independently on their own control builds — one via `git archive` plus a standalone BGZF parser, one via an isolated `CARGO_TARGET_DIR` plus an injected-warning control proving its clippy run could fail. What they changed: the gate was pre-empting the two structural pair messages, which is the same defect the plan congratulated itself for avoiding with `--clump_only`, one level down; the message's headline asserted impossibility where a description-free FASTQ demonstrably honours the flag, contradicting its own next sentence four lines later; and `--rename` with no clip flag — a pure no-op — was being refused, which neither the plan nor its two plan reviews had noticed. One reviewer also caught a **false claim in my own changelog entry**: I wrote that `--basename` was undocumented, when it is documented on the clump-only and passthrough pages. The accurate statement is that it had no dedicated section in the output guide.

**The plan's r1 was blanket rejection in `cli.rs`, and it would have failed.** Its assumption A2 — that no test asserts this combination succeeds — was false and had been explicitly deferred rather than checked. `tests/integration_ubam_out.rs:393` is the C1 tab-splice regression guard and it does assert exactly that, on uBAM input. Second time in the same session that a deferred pinning grep was the thing that broke a patch. r1 also framed uBAM safety as data-dependent good fortune when it is a spec guarantee, which is what made the blanket scope look free.

Two things the format gate bought beyond correctness, neither of which was an argument for it: the C1 guard survives with no edit, and the `--clump_only` pre-emption disappears because the check moved behind `validate()`.

**One deviation from the approved plan.** Its step 3 asked for `cli.rs` unit tests; those are unreachable, because the guard must see `input_formats` and therefore lives in the `[[bin]]`, which library unit tests cannot reach. All five tests are binary-driven instead. Validation 6 gains something from that: as an integration test it proves the *ordering* between `validate()` and the new guard, which a unit test could not.

**Three false-greens, all caught by checking rather than assuming.** A `${PIPESTATUS[0]}` exit check silently evaluated to nothing under zsh, hiding a `clippy` run that finished in 0.18 s — a cache hit, not a check; I injected a deliberate `unused_variable` to prove clippy actually lints the edited target, then removed it and re-ran on an invalidated cache. A by-name grep appeared to show one of the five tests missing, when the test binary's own stdout had interleaved and broken the `^test` anchor. And the 575 figure is counted against a 570 baseline from a separately-built worktree at the parent commit, because equal test counts are exactly how a stale-tree verification hides.

**One thing the plan did not ask for.** It asserted that `--hardtrim5`/`--hardtrim3` lose the annotation the same way. Rather than trust that, I confirmed `--hardtrim5 20 --rename` genuinely annotates on the FASTQ path (`:clip5:ACGTACGT`) — so the refusal covers a path that actually worked, not a no-op.

Follow-up worth filing separately, and expected by both plan reviewers: carrying the annotation as a BAM aux tag, which would make the refusal unnecessary.
</details>

 (manual close needed — dev is not the default branch).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aa9f764221f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.