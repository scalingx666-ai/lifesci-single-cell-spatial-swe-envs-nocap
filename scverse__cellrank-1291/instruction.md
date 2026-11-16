# Issue

**Title:** CI workflow modernization

## Description

Modernize CI workflows (PR 5 of modernization plan)

## Changes

### test.yml → test.yaml
- Dynamic hatch-test matrix from `hatch env show --json` — pyproject.toml is the single source of truth for Python versions and dep variants
- Add Python 3.14 and pre-release dependency testing (with `continue-on-error`)
- Add pixi-based PETSc/SLEPc and R/GAMR jobs (deps installed via conda-forge)
- Add `re-actors/alls-green` gate job — single required check for branch protection
- macOS job via matrix `include`
- Bump actions: checkout@v6, setup-uv@v7, codecov-action@v5

### deployment.yml → release.yaml
- Replace tox with `uv build`
- Use `on: release: types: [published]` trigger (modern pattern)
- Keep existing `deployment` environment + trusted publishing

### New build.yaml
- `uv build` + `uvx twine check --strict` on every PR
- Catches packaging issues before release

### lint.yml → pre-commit.ci
- Delete GHA lint workflow; linting handled by pre-commit.ci
- Add `ci:` config block to `.pre-commit-config.yaml` (monthly autoupdate, autofix PRs)

### pyproject.toml
- Add Python 3.14 to hatch-test matrix
- Add pre-release matrix entry with `UV_PRERELEASE=allow` override

### pixi.toml
- Add shared `test` feature with test dependencies (pixi doesn't install dependency-groups from editable PyPI packages)
- Compose into slepc/r environments: `slepc = ["test", "slepc"]`, `r = ["test", "r"]`
- Run full test suite in pixi jobs (tests self-skip via `importorskip`/`skipif` when deps are absent)

## Post-merge steps
- Update branch protection required checks: use `All tests pass` as the single gate job

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac9e6e461477`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.