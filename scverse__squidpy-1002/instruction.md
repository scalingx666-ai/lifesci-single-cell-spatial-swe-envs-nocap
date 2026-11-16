# Issue

**Title:** Numba warning fix

## Description

Fixes: 

Without the fix this is the warning I get in a notebook:

```
[/Users/selman.ozleyen/mambaforge/envs/squidpy/lib/python3.11/site-packages/numba/parfors/parfor.py:2395](https://file+.vscode-resource.vscode-cdn.net/Users/selman.ozleyen/mambaforge/envs/squidpy/lib/python3.11/site-packages/numba/parfors/parfor.py:2395): NumbaPerformanceWarning: 
prange or pndindex loop will not be executed in parallel due to there being more than one entry to or exit from the loop (e.g., an assertion).

File "/Users/selman.ozleyen/projects/squidpy/docs/notebooks/tutorials", line 31:
<source missing, REPL/exec in use?>
```

I don't think it is possible to add a test case because in theory that part of the code is unreachable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c3277fb1509a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.