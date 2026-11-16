# Issue

**Title:** Build backend migration (setuptools → hatchling)

## Description

Migrate the build backend from setuptools to hatchling, following the current [scverse cookiecutter template](https://github.com/scverse/cookiecutter-scverse).

## Changes

### Build system (`pyproject.toml`)
- **Build backend**: `setuptools.build_meta` → `hatchling.build` + `hatch-vcs`
- **PEP 735 dependency-groups**: moved `dev`, `test`, `docs` from `[project.optional-dependencies]` to `[dependency-groups]` — these are not part of the public package interface and shouldn't be published in wheel metadata
- **Hatch environments**: `default` (dev, uv installer), `hatch-test` (matrix: 3.12/3.13), `docs` (sphinx build/open/clean scripts)
- **Removed**: `[tool.setuptools]`, `[tool.setuptools_scm]`, `[tool.tox] legacy_tox_ini` (~80 lines)
- **Deleted** `MANIFEST.in` (not needed by hatchling)

### RTD (`.readthedocs.yaml`)
- Adopted the scverse cookiecutter pattern: install `uv` via `asdf`, then `uvx hatch run docs:build`
- This bypasses RTD's native `extra_requirements` (which doesn't support PEP 735 dependency-groups)
- Bumped OS from `ubuntu-22.04` → `ubuntu-24.04`

### CI (`test.yml`)
- **Minimal fix** to keep CI passing after tox removal: replaced `pip install tox` + `tox -e ...` with `uv sync --group test` + `uv run pytest`
- Dropped `slepc` matrix entry and conda setup (full CI modernization in PR 5)
- ⚠️ CI check names change — branch protection required checks will need updating after merge

### New: `pixi.toml`
- Declarative conda environments for PETSc/SLEPc and R (CI-only, used in PR 5)

## Testing
- Pre-commit passes on all files
- Package builds (`python -m build` produces sdist + wheel)
- Editable install + import works
- 109 skips expected (PETSc/SLEPc, R not installed locally)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5913811dd3f1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.