# Issue

**Title:** Update utils_reduceDimension.py: bug fix

## Description

```
/dynamo/tools/utils_reduceDimension.py", line 27, in prepare_dim_reduction genes = adata.var_name.intersection(genes).to_list() AttributeError: 'AnnData' object has no attribute 'var_name'
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ae5df5bfbcd2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.