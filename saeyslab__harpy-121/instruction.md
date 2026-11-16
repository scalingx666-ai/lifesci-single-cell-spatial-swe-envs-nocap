# Issue

**Title:** Refactor dependency groups and default installation.

## Description

.

This introduces a recommended Python-only installation with `uv`:
```bash
uv venv --python=3.12 # set python version
source .venv/bin/activate # activate the virtual environment
uv pip install 'harpy-analysis[extra]' # use uv to pip install dependencies
python -c 'import harpy; print(harpy.__version__)' # check if the package is installed
```

Some other installation related topics not solved or tested here:
- [ ] update documentation in installation guide #95 
- [ ] update documentation in contribution guide
- [ ] prefer uv and hatch, but also possible installation options are conda, mamba, pixi...
- [ ] Windows support
- [ ] basicpy support
- [ ] update HPC cluster installation documentation and usage of lockfile with `--frozen`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `50970dabf653`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.