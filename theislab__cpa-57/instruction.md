# Issue

**Title:** Update dependencies due to recent version changes in Google Colab

## Description

The whole installation should be a one-liner now: 
```
pip install cpa-tools
```
or
```
pip install git+https://github.com/theislab/cpa
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0079659badce`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.