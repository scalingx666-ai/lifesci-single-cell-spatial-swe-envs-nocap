# Issue

**Title:** feat(quant): implement --noFragLengthDist; confirm sketch fragment-length weighting

## Description

`--noFragLengthDist` was a no-op; now implemented (disables the fragment-length assignment-probability term in SA + sketch). Confirms sketch uses the FLD like SA (trains it from pairs, weights pairs by pmf(flen)-cmf(txpLen), and applies the orphan/SE ambiguous term now that sketch carries positions).

Sim accuracy (Spearman vs truth, FLD on vs off): easy SA +0.011 / sketch +0.012; hard SA +0.015 / sketch +0.016. Clippy + tests green.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `15ee01b107f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.