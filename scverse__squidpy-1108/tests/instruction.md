# Issue

**Title:** Lower bound spatialdata and unpin dask

## Description

I also tested this with 
```
uv pip install 'rapids-singlecell[rapids12]' --extra-index-url=https://pypi.nvidia.com
```
so it works in one environment and current pyproject.toml

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f976fb02f0ea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.