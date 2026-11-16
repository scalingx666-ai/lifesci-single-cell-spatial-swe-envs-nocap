# Issue

**Title:** using stack instead of recursion in DFS

## Description

For file `TESLA_package/TESLA/ConnectedComponents.py`,  when there are too many elements in adj matrix, the recursion level in DFS would be so high and would result in core.dump even `sys.setrecursionlimit(adj.shape[0])` were set.

So it is suggested that using stack (`from collections import deque`) instead of recursion. This DFS algorithm would run well with 30,000x 30,000 adj matrix after this change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e748a22fc03d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.