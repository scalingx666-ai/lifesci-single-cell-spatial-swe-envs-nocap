# Issue

**Title:** Speed up breath first search

## Description

This should increase the speed of breath first search significantly, without using the recursive approach, that may or may not be broken.  Taking care of my problems from issue  #31.  I get a massive speed increase compared to the previous version.  

I tested this update on one full bam file, and saw no changes in the output.  Given that this is a change to a core algorithm, it might deserve some additional testing on your end before merging it into master.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `949b7c15224e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.