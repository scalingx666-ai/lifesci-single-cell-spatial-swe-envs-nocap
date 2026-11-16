# Issue

**Title:** Add CLI interface from spatialdata branch

## Description

Use CLI with `python -m napari_spatialdata ...` or `spatialdata ...`.

```
Usage: spatialdata [OPTIONS] COMMAND [ARGS]...

  Group of commands for napari-spatialdata CLI.

Options:
  --help  Show this message and exit.

Commands:
  view  Interactive visualization of SpatialData datasets with napari
```

Load a dataset using `spatialdata view /path/to/data.zarr`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f03f587267a4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.