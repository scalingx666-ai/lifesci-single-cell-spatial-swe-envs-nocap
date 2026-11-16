# Issue

**Title:** {ts} debug per gene

## Description

The --gene-tag option previously assumed all gene tags were gene names. featureCounts and HTSeq both use the same tag for the gene as the assignment status. These commits introduces the --gene-tags-skip option to ensure unassigned reads do not cause bundles to be yielded prematurely and unassigned reads are not outputted.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cd652b425ee1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.