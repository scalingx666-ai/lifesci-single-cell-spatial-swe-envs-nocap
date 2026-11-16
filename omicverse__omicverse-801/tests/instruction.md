# Issue

**Title:** chore(submodule): bump guide — ov.pl plots in epigenetics tutorials

## Description

Bumps the `omicverse_guide` submodule to omicverse-tutorials#76, which switches the epigenetics tutorials' generic plots (embedding/UMAP, marker dotplot, volcano) to omicverse's own plotters (`ov.pl.embedding` / `ov.pl.dotplot` / `ov.pl.volcano`). ATAC/Hi-C-native visuals keep their purpose-built plotters. Notebooks re-executed in `omicdev`; isolated `sphinx-build -W` clean.

No changes to `omicverse/epi/` code — docs/submodule only.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f829a9485b20`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.