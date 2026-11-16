# Issue

**Title:** fix(main): paired report paths join the collision pre-flight

## Description

. Paired output names carry a positional discriminator (`_val_1`/`_val_2`) that report names do not, so two inputs with distinct trimmed outputs could still collide on their reports: `--paired -o out A/reads.fq B/reads.fq` exited 0 with one report pair for two inputs, R2's report having silently overwritten R1's. The four report paths per pair (text and JSON) now join the collision pre-flight on the paired FASTQ and paired uBAM-output paths, skipped under `--no_report_file` to match the writers.

Behaviour changes, both in the CHANGELOG: a pair whose R1 and R2 share a filename written to a common output directory is now refused on every filesystem (that run previously lost a report), and two distinct inputs whose filenames differ only in case are refused even on a case-sensitive filesystem — the #216 loud-error-over-silent-loss trade, extended to paired reports.

<details>
<summary>Detail (AI-assisted; bin freely)</summary>

The root cause is an argument that was true where it was written and false where it was reused: #385 established that report keys (full input filename) are finer than primary keys (stem) on the single-end path, so checking primaries suffices there. Paired primaries append `_val_N`, which report names lack — in that dimension the report key is *coarser*, and the SE argument does not transfer. The three comments stating that argument in general terms are now scoped to SE naming, so the trap is disarmed along with the bug.

Both paired sites also pass a remediation hint: the generic advice recommends different source directories or `--output_dir`, which are exactly the two things that cannot help a filename-keyed collision.

The same defect exists on `--clump_only --paired` (clumping reports) — found independently by both code reviewers, reproduced, and filed as #391 rather than grown into this diff, since that fix restructures `run_specialty_paired`'s signature.

**Verification.** 546 tests (6 new: three rejection shapes including a case-free one that exercises the fix on Linux CI, the uBAM twin, a `--no_report_file` gate test pinning candidates == writers, and boundary acceptance cases asserting the report filenames they claim are distinct). Both negative controls discriminate: disabling the FASTQ block fails its three rejection tests while acceptance and gate tests pass; disabling the uBAM block fails its test alone. Dual plan review rebuilt the entire first-draft validation section — all four original tests could neither pass nor fail as specified. Coverage audit: COMPLETE, 20/20, first pass.

Perl byte-identity matrix untouched (no CI invocation uses colliding paired filenames). Artefacts under `plans/08072026_paired-report-preflight/`.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c4599f56985b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.