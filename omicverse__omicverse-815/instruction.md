# Issue

**Title:** release: v2.2.1

## Description

Bumps `version` `2.2.1rc1` → `2.2.1` for the final 2.2.1 release.

Includes everything merged since v2.2.0 (~190 commits), most recently the
on-device MLX UMAP negative-sampling perf fix (#814).

Full changelog: v2.2.1 section of the release notes (8 new modules —
genetics / protein / mol / epi / airr / single-metabolism / EV / histo —
out-of-core preprocessing, rebuilt trajectory & pseudotime, edgeR/limma +
time-course DEG, unified MetaCell, GPU non-parametric UMAP, simpleaf
alignment, funkyheatmap, and bug fixes).

After this merges: tag `v2.2.1` and publish to PyPI.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2da751cd4848`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.