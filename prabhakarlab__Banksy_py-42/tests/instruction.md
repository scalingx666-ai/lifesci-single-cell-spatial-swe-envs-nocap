# Issue

**Title:** Lift numpy<2.0 and requires-python<3.13 caps for modern environments

## Description

Builds on #38 by @zhou-1314 — that commit is included here intact (authored by them), covering the numpy 2.x fix and the real-data integration test.

#38 removes the `numpy<2.0` cap but leaves `requires-python` at `<3.13`, which still blocks installation on Python 3.13 even after the numpy fix. This adds the matching version lift:

- *(from #38, @zhou-1314)* `numpy>=1.21,<2.0` → `numpy>=1.21`; add `test_with_real_data.py`; release 1.3.5
- `requires-python >=3.8,<3.13` → `>=3.8,<3.14`
- add the Python 3.13 trove classifier

Verified end-to-end on Python 3.13.13 / numpy 2.4.x via the bundled STARmap test (`test_with_real_data.py`) — all steps pass.

If you'd rather land the numpy change via #38 directly, happy to reduce this to just the `requires-python`/classifier commit and rebase onto it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `43e2d692db67`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.