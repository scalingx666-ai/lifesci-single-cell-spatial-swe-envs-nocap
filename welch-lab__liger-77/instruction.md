# Issue

**Title:** Added an error catch to suggestK

## Description

When I was running through the tutorial I initially ran suggestK before running ScaleNotCenter (the command is mixed in with those from the 'precomputed list' set). It gave a fairly cryptic error. To save people in the future digging through the code to figure out what's wrong, probably best to just add this line. 

Thanks for developing this great package!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `639d547a454b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.