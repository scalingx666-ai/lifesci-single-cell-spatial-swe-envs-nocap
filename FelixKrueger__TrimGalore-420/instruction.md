# Issue

**Title:** feat(io): one output directory per pair — reports and carrier follow R1

## Description

Without `--output_dir`, a paired run could scatter across three directories: the validated FASTQs went to R1's parent, each trimming report went beside *its own* mate, and `--passthrough`'s carrier output went beside the carrier input. All five primary paired namers already shared one directory expression; the report namers did not, because they are shared with the single-end paths where per-input parent is correct. That expression is now `pair_output_dir`, and the reports and the carrier consume it too.

Report **filenames** are unchanged — each keeps its own input-derived name, so `*_trimming_report.txt` globs and MultiQC still match. Only the directory is shared. Single-end is untouched.

Perl v0.6.11 had no per-mate report directories either: `sub trim` strips the input's directory with `(split /\//,$filename)[-1]` and opens the report at `$output_dir`, defaulting to the working directory. The split layout was a v2 regression rather than something inherited — though the anchor still differs, so this isn't "matches v0.6.x".

**This is a behaviour change in both directions, and one of them refuses runs that previously worked.**

Names derive from the input filename alone, so two inputs whose filenames fold-equal now resolve to one report path once co-located, and the run stops before writing anything. The layout that hits is reads split by mate rather than by sample — `--paired R1/s1.fq R2/s1.fq R1/s2.fq R2/s2.fq` — and the **whole invocation** is refused, not just the offending pair, because candidates for every chunk are collected before a single pre-flight call. Pass `--output_dir`; `--no_report_file` also clears it but discards the reports. The per-sample layout (`sampleA/reads_1.fq sampleA/reads_2.fq sampleB/…`) is unaffected, since each pair's R1 already sits in its own directory.

A refusal also **disappears**: a mate shared between two pairs whose R1s live in different directories no longer collides, because its two reports now resolve into those two directories. Eight distinct paths, nothing overwritten — continuing to refuse would be over-rejection. The #391 test asserting that refusal flips to asserting success, and the previously-untested trim twin of the same shape gains a test.

Relocating a report also opens an output-vs-**input** path: R2's report can now equal R1's own input (`--paired A/reads.fq_trimming_report.txt B/reads.fq`). The candidate builders move with the writers, so the pre-flight refuses it — this is #409's shape on an arm the change creates, and the tests assert the victim's read count rather than its mere existence.

11 new tests, 589 total. Every refusal was also run against a build made from `38deb1ee` in a fresh worktree, where the mate-side and report-on-input cases exit 0 and the shared-mate case exits 1.

<details>
<summary>AI-assisted: what the dual plan review changed, and the three test flips it let us predict</summary>

**The plan's r1 described this as one new refusal in one place. It is wider than that**, and the dual review is what established the shape. Both reviewers verified independently that the five-namer extraction is behaviour-preserving and that the arm table was complete — one of them enumerated all eleven pre-flight call sites to check. Between them they raised six Critical findings.

Three of them were behavioural footprint that r1 missed entirely: a **second** over-rejection guard on the clump arm, carrying almost the same "a builder that resolved reports into one directory would over-reject this" comment as the one r1 built a prominent warning around; an existing deliberate refusal that **disappears**; and the output-vs-input direction, which is the exact shape of the data-loss bug fixed three commits earlier. A fourth was a latent break: r1's instruction to stop `clump_report_candidates` deriving per input would have collapsed every single-end input's report into one directory — the same family, mirrored, on an arm r1 had declared out of scope. In the end that helper needed no signature change at all.

Because r2 enumerated those three test changes with line ranges and the correct resolution for each, the first full run produced **exactly three failures and no surprises**. That mattered: the natural way to make a red test named `..._do_not_over_reject` go green is to narrow the candidate list, which would restore the old paths on the pre-flight side while the writers moved — precisely how this bug family recurs. Both rewritten guards now name their twin and say not to do that. They were also renamed, since a test called `do_not_over_reject` that asserts a rejection reads as a contradiction.

Two smaller things worth recording. `cargo build --release` reported zero errors while the test targets were still broken by the `passthrough_output_name` signature change — a release build doesn't compile test targets, so it can't stand in for a compile check. And both reviewers told me to correct the docs path to `Docs/src/content/docs/`; both were wrong, since git tracks it lowercase and the capital only resolves because APFS is case-insensitive.

The reviews also produced the v0.6.11 output-directory fact above, which answers an open question r1 had left as a preference: `--hardtrim5/3` should **not** share this helper, because their current CWD anchor is the Perl-faithful one and the trim path's input-parent anchor is the v2 innovation.

Deferred to #414: dedicated paired report namers taking R1, which would make writer/candidate drift unrepresentable rather than tested-for. Both reviewers raised it; it belongs with the generator work rather than bundled into a behaviour change.
</details>

 (manual close needed — dev is not the default branch).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `38deb1eecb89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.