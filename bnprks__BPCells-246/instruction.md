# Issue

**Title:** [r][cpp] Add missing user interrupt checks

## Description

I noticed that rowMaxs and colMaxs didn't check for users pressing ctrl-C when I was working on a recent PR, so I did a sweep of all the `*.cpp` files in the `src` dir to make sure everything quits promptly when ctrl-C is pressed.

My rule of thumb for check frequency is that every column is fine for a matrix since there are 1000s of columns usually, but for fragments it's necessary to check within each chromosome since a single chromosome might be too long to wait through.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b351734c9a31`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.