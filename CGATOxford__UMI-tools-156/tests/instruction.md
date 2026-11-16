# Issue

**Title:** {mp} hashed construction of adj list

## Description

This branch introduces a slightly modified version of the adjacency list constriction, which negates the necessity to do all-by-all comparisons in some cases. 

If we are looking for UMIs that differ by only a single base, then either their first or second halves must be identical. Thus we only need to do comparisons amongst those UMIs that share either the first or second half of their sequence. 

We compare identity using a hash, making it very quick. 

This can lead to substantial speed up in cases with a large number of UMIs. 

For example, for a fully saturated 10bp UMI network, instead of needing to do 1e12 comparisons, we would only need to do 1e6 comparisons, plus 1e6 hashing operations, improving the speed by more than 5 orders of magnitude! 

Gains are less for positions with fewer UMIs and at some point the costs of hashing out weight the costs of comparisons. Thus, this mode is only activated where there are more than 25 UMIs at a position. 

props to @mparker2 for this idea!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2bf371ffb1b0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.