# Issue

**Title:** Check that `numpy` is not affected by critical bug #104 at import time

## Description

It's only natural for new users to install the latest Anaconda and run `velocyto`, potentially stumbling on bug #104 . This check stops them before they hurt themselves, and gives them useful advice on how to proceed.

I'll let you decide if it's a good idea or not...

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9881ac854194`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.