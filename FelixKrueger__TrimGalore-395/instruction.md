# Issue

**Title:** fix(cli): say what the --passthrough alias check actually checks

## Description

The `--passthrough`-matches-R1/R2 check keeps its case-folded key (deliberately: on APFS/NTFS a case-variant passthrough IS the input and would be consumed twice, and this check is the sole guard for that) but stops claiming identity unconditionally. The message is now two-tier: pointing at an input directly says the passthrough must be a third file (e.g. the index read) and names the matched input; a case-variant match states the comparison is case-insensitive and suggests a rename. Accept/reject behaviour is unchanged — both branches bail identically. Companion fixes: `norm_path`'s rustdoc no longer claims direct use by `Cli::validate` or uses the "aliasing" framing; the envelope preamble drops the "#216 protection" label. Tests pin the honesty (negative assertion on the old identity claim) and a new lexical case-variant test covers the case-only branch identically on ext4 and APFS.

Plan + dual plan-review + implementation notes: `plans/08082026_passthrough-alias-wording/` (artifacts follow in a second commit after code review + coverage audit complete).

 (manual close needed — dev is not the default branch).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ea274184772`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.