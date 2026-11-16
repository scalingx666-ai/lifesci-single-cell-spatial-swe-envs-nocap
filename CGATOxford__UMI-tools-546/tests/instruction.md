# Issue

**Title:** Ts add test action

## Description

Adds github actions to perform testing. 

Still relying on the same bespoke test script we repurposed from cgat which utilises `nose`. Note that `nose` is no longer supported and cannot be used to test python 3.10 (). I tried a few of the suggestions in that issue to resolve the issue but nothing worked straight out of the box. 

For now, I've dropped testing for `python 3.10` in favour of getting the CI testing back up and running. In the long run, it seems like we should be switching to `pytest`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `df2eba359764`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.