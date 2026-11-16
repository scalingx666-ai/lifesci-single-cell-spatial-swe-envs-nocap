# Issue

**Title:** fix(cli): reject --hardtrim5 with --hardtrim3

## Description

. `--hardtrim5 N --hardtrim3 M` was accepted and only the 5' trim ran — the 3' request was silently dropped at exit 0 (Perl v0.6.x behaved the same way). The pair is now rejected in `Cli::validate()` with the remedy in the message: run the two trims as separate invocations, feeding the first trim's output to the second. The hardtrim docs page's Compatibility section now names the incompatibility too.

<details>
<summary>Detail (AI-assisted; bin freely)</summary>

Validate-level rather than clap `conflicts_with`, on the code reviewer's argument: the other hardtrim exclusions (`--clump_only`, `--passthrough`, `--clumpify`) are all validate-level with bespoke messages, so the generic clap wording would have been the family-inconsistent choice — and the sequential-runs remedy is non-obvious enough to belong in the error text rather than only the CHANGELOG. A validate check is symmetric by construction; both flag orders are tested and verified against the binary.

548 tests on the rebased branch. Negative control: disabling the check fails the conflict test while the each-flag-alone guards pass. Artefacts under `plans/08082026_hardtrim-conflict/` (plan — fast-tracked past agent plan-review on the user's explicit call, recorded; one scaled code review; COMPLETE coverage audit).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ad2639a751e1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.