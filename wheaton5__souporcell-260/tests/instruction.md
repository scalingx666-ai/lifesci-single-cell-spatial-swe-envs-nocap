# Issue

**Title:** Minimap2fix

## Description

Hi @wheaton5, as discussed in #259, I solved the error. It was due to an option in minimap2 that I needed to add. The `-I` argument allows users to increase the amount of memory that can be used to hold the target bases. Please see the minimap2 docs for further details: [https://lh3.github.io/minimap2/minimap2.html#4](https://lh3.github.io/minimap2/minimap2.html#4).
I am currently running `souporcell_pipeline.py` on my end to ensure that it runs smoothly. I will update this once it is complete.
I hope this helps others as well.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `08d3c2ef34a8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.