# Issue

**Title:** Add support for local StarDist models

## Description

This PR adds support for using **local StarDist models** in both the Python API and the CLI.

Previously, `sopa.segmentation.stardist` only supported loading pretrained models via StarDist aliases (e.g. `"2D_versatile_he"`). This change allows users to load models from a **local directory**.

## Usage

### Python API

```python
sopa.segmentation.stardist(
    sdata,
    local_model="path/to/model",
    ...
)
```
### CLI

```bash
sopa segmentation stardist  --local_model path/to/model ... 
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `42ab54f29057`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.