# Issue

**Title:** test: centralize skip markers and enable strict markers/config

## Description

## Motivation

Test-suite hygiene around the skip surface:

- The `petsc_slepc_skip` marker was defined ad-hoc in `test_linear_solver.py`, while the other skip markers (`jax_not_installed_skip`, `gamr_skip`, `scvelo_skip`) live centrally in `tests/_helpers.py`.
- `test_gpcca.py::...::test_compute_schur_verbosity` gated the *same* PETSc/SLEPc dependency via inline `pytest.importorskip(...)` calls — a third, inconsistent way to express the same skip.
- Pytest ran without `--strict-markers`, so a typo'd or unregistered marker would silently pass instead of erroring.

## Changes

- **Centralize `petsc_slepc_skip`** in `tests/_helpers.py` alongside the other skip markers, reusing the production `_is_petsc_slepc_available` helper. `test_linear_solver.py` and `test_gpcca.py` now import it from there.
- **Convert the inline `importorskip`** in `test_compute_schur_verbosity` to the shared `@petsc_slepc_skip` marker, so the whole skip surface is declared in one place.
- **Enable `--strict-markers` and `--strict-config`** in `addopts`. The suite uses only built-in markers (`parametrize`, `skip`), so nothing needs registering — this just guards against future typos/misconfig.

## Testing

```
uv run pytest --collect-only -q          # 1175 tests collected, no marker/config errors
uv run pytest tests/test_linear_solver.py::TestLinearSolverPETSc \
              tests/test_gpcca.py -k "...verbosity" -rs
# 80 skipped via the centralized marker, consistent reason "PETSc or SLEPc is not installed."
```

(PETSc/SLEPc + R run in the dedicated `PETSc / SLEPc + R` CI job; this PR doesn't change which tests run there — only how the skip is declared.)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eb89baf3751e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.