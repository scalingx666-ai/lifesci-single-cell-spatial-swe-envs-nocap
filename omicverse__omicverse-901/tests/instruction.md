# Issue

**Title:** chore(docs): bump omicverse_guide to surface t_synbio_04 + case03 in the nav

## Description

The docs submodule already pointed at a tutorials commit that **contains** t_synbio_04_advanced and t_synbio_case03_dhfr_evaluation, but those two notebooks were missing from the tutorial **navigation** (Tutorial.md + the mkdocs toctree `tutorials/index_synbio.md`) — so they didn't surface in the built docs. omicverse-tutorials#92 fixed the nav; this bumps `omicverse_guide` to that HEAD (2a667fac) so the built docs list all 7 synbio tutorials.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0ff418728a43`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.