# Issue

**Title:** ov.space.seg: tiled three-view 3-D instance segmentation (tbs2/nis3d)

## Description

TBS RSI branch `tbs2/nis3d` at 75a5c84d (nis3d-hard-volume reward 1).

- `ov.space.segment_volume_multiview`: tiled three-view 3-D instance segmentation (floored per-slice normalisation, denormal flush, memory high-water tracking, densest-tile dry run).
- Tests: `tests/space/test_segment_volume_multiview.py`.

Generic method; no task constants.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b760a67bd7fc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.