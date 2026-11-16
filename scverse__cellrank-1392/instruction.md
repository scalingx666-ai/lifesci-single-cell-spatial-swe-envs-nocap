# Issue

**Title:** ci: link to cookiecutter-scverse via cruft; PETSc/SLEPc + R tests via pixi; require pygpcca>=1.1

## Description

Part of #1389.

## Changes
- **Template link:** `.cruft.json` at cookiecutter-scverse v0.8.0 (`cruft check --checkout v0.8.0` is clean). Adopts the template's CI hardening: actions pinned by SHA, `persist-credentials: false`, least-privilege `permissions`, zizmor, codecov via OIDC, dependabot cooldown, `.codecov.yaml`, `.editorconfig`, `.gitignore`.
- **PETSc/SLEPc + R tests:** setup-miniconda is replaced by a pixi `krylov` environment in `pyproject.toml` (`pixi run -e krylov test`): PETSc, SLEPc, rpy2 and mgcv from conda-forge, everything else as in the hatch `test` group. No lockfile, so new petsc4py releases are tested as they appear. The job now gates `All tests pass` instead of being allowed to fail.
- **`pygpcca>=1.1`:** 1.1.0 works with petsc4py 3.26 (GPCCA/pyGPCCA#67), which fixes the 19 GPCCA failures in the old PETSc job. Its jinja2 pin is gone, so the uv override is removed.
- Project URLs point to scverse/cellrank; AGENTS.md, REVIEW_GUIDE.md and the contributing guide describe the pixi job.

Kept on purpose, differing from v0.8.0: autofix.ci (already on the template's `main`), panache, the macOS job and rendered-figures artifact, and the check name `All tests pass` (required by the `main` ruleset).

**Before the next release:** the release workflow's environment is now `pypi` (template default), so the PyPI trusted publisher's environment needs renaming from `deployment`.

Local: hatch py3.12 1143 passed / 102 skipped; `pixi run -e krylov test` 1223 passed / 22 skipped.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d7921520296`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.