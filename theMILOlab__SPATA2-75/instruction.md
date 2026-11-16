# Issue

**Title:** Error when calling runSeuratClustering

## Description

getVariableNames is not a method on SPATA2 object - I think the correct one is getFeatureNames.

Before:
```
No such method getVariableNames
```

After:
```
14:34:40 Using matrix 'scaled'.
14:34:40 Using expression matrix 'scaled'.
Calculating gene variances
0%   10   20   30   40   50   60   70   80   90   100%
[----|----|----|----|----|----|----|----|----|----|
**************************************************|
Calculating feature variances of standardized and clipped values
0%   10   20   30   40   50   60   70   80   90   100%
[----|----|----|----|----|----|----|----|----|----|
**************************************************|
...
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `95b5fdd07430`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.