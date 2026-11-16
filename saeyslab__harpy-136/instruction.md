# Issue

**Title:** Added channel_names to snr_ratio to fix wrong SNR scatter plot annotion - correction

## Description

modified: src/harpy/plot/_qc_image.py to solve issue #134. Previous pull request contained an error:

```python
channel_names = table.var_names
```

But table was undefined. Changed to

```python
channel_names = sdata.table.var_names
```

So everything should work now.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d28e245ccece`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.