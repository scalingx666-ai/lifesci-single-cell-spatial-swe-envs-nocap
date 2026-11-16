# Issue

**Title:** Adopt cookiecutter-scverse v0.8.0 CI/security hardening

## Description

Cherry-picks the low-risk, high-value parts of the v0.8.0 template sync (#1242), leaving squidpy's customized theme, dependencies, and squidpy-specific CI jobs intact.

## CI / security hardening
- **pre-commit**: add [zizmor](https://github.com/zizmorcore/zizmor) hook; bump biome/pyproject-fmt/ruff.
- **dependabot**: new, weekly grouped github-actions updates (pairs with SHA pinning).
- **build/release/test workflows**: pin actions to immutable SHAs, add least-privilege `permissions:` blocks, `persist-credentials: false`.
- **test workflow**: codecov upload via OIDC (`use_oidc: true`, drops `CODECOV_TOKEN`). Kept: `ensure-data-is-cached`, data cache, system deps + Xvfb, macOS matrix, figure artifacts.
- **readthedocs**: build on Python 3.14 + nodejs; kept the `docs/notebooks` submodule + `UV_CONSTRAINT`.
- **cruft**: record the v0.8.0 sync so the next auto-sync diffs from v0.8.0.

## Docs
- Adopt `scverse_misc.sphinx_ext` (v0.8.0 moved shared sphinx extensions into the `scverse-misc` package) and drop the local `docs/extensions/typed_returns.py` monkeypatch. Adds `scverse-misc[sphinx]` to the docs group. Theme, intersphinx, and the rest of `conf.py` stay squidpy's.
- `pyproject.toml` also carries the `pyproject-fmt` normalization from the bumped hook (pre-commit.ci).

## Deliberately NOT taken from #1242
Template's `pyproject.toml` (reverts deps/version/authorship to the seed skeleton), the full `docs/conf.py` rewrite (theme swap `sphinx_rtd_theme` -> `sphinx_book_theme`), `docs/_static/css/custom.css` (deletes 122 lines), `.vscode/*`, `docs/changelog.md`, and the stricter ruff `D`/`TID`/`RUF100` rules (worth a separate PR).

Supersedes #1242, which should be closed.

> Note: the `scverse_misc.sphinx_ext` swap is verified by the RTD preview build on this PR, not locally.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `959a73e3563f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.