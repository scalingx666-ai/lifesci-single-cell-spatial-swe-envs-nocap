# Issue

**Title:** remove custom fonts and seaborn

## Description

I have eliminated the usage of custom fonts and all additional Seaborn function calls without altering the final output of the plots. This action effectively removes the dependency on the Seaborn library. This adjustment addresses two primary issues:

1. The removal of custom fonts eliminates the persistent warnings about missing fonts. 

2. The eradication of the Seaborn dependency simplifies the overall package structure.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cfc1a2dddf46`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.