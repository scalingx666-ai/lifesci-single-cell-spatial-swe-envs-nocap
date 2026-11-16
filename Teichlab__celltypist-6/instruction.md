# Issue

**Title:** Add `model_list` argument to download models by name

## Description

Add `model_list` argument to `models.download_models`. This argument is a list that serves as filter to download models. It allows users to download only a subset of models by providing a list of filenames. Usage:
```python
from celltypist import models
models.download_models(force_update = True, model_list=["Immune_Placenta_Low.pkl"])
```

This feature comes from #5

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5b29db790bdb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.