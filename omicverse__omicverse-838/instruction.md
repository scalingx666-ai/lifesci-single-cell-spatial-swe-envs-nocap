# Issue

**Title:** chore(docs): bump omicverse_guide submodule (t_infercnv platform fix)

## Description

Advances the `omicverse_guide` submodule pointer to omicverse-tutorials@`d945972`, picking up:
- **#81** — `t_infercnv` tutorial now passes `platform='smartseq2'` (required after #822 made `platform=`/`cutoff=` mandatory for inferCNV; correct for Maynard 2020 Smart-seq2 data).
- **#80** — scenic tutorial notebook update.

Submodule-only change.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6107ef514e5a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.