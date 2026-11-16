# Issue

**Title:** feat(models): make pygam an optional dependency

## Description

## Summary
- `pygam` moves from `dependencies` to a new `gam` extra. `cellrank.models.GAM` imports it lazily and raises `ModuleNotFoundError` with `pip install cellrank[gam]` when it is missing; `import cellrank` no longer needs it.
- `pygam` joins the `test` group; `docs/installation.md` and `AGENTS.md` list the extra.

## Why
Every pyGAM release (0.10.1–0.12.0) declares `scipy<1.17` (dswah/pyGAM#584, open since May). As a required dependency it holds pip users on scipy 1.16 and makes CellRank unsolvable wherever scipy is pinned by conda (e.g. pixi with conda-forge scipy 1.18). Only `GAM` uses it.

## Breaking change
Fitting gene trends with `cr.models.GAM` now needs `pip install "cellrank[gam]"` — worth a line in the release notes. The conda-forge recipe can keep pygam as a run dependency (conda-forge's pygam has no scipy cap).

## Testing
- `tests/test_model.py`, `tests/test_utils.py`: 272 passed, 14 skipped (Python 3.12, scipy 1.16.3, pygam 0.12.0).
- New tests: `import cellrank` with pygam blocked (subprocess), and `GAM()` raising the install hint.
- The `PETSc / SLEPc + R` job has failed on `main` since 2026-10-01 (petsc4py 3.26 removed `Mat.getVecs`); unrelated, follow-up PR.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `17fee147f46b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.