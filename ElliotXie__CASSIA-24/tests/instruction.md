# Issue

**Title:** Fix x86 Python env on Apple Silicon: layered managed-Python setup

## Description

## Problem (issue #23)

On Apple Silicon Macs, loading CASSIA auto-created an **x86_64** Python virtualenv on an **arm64** machine, so every `runCASSIA_batch()` failed with an architecture mismatch. Deleting `~/.virtualenvs/cassia_env` didn't help — `.onLoad` recreated it on the next namespace load, and because Python was bound eagerly at load time, a later `set_python_env()` had no effect.

Root causes in `.onLoad`:
- It force-set `RETICULATE_USE_MANAGED_PYTHON=FALSE`, disabling reticulate's uv-managed Python (which would have picked the correct arm64 interpreter), then hand-rolled a venv from whatever system Python it discovered — often x86.
- It auto-created the env on every (implicit) namespace load.
- It eagerly imported the Python module, locking in the wrong interpreter for the session.

## Fix

Replace env resolution with a three-tier strategy in `.setup_cassia_python()`:

| Tier | Strategy | When |
|---|---|---|
| 0 | Explicit user choice (`RETICULATE_PYTHON` / `set_python_env`) | always respected first |
| 1 | **Managed Python via uv** (default) | downloads a correct-architecture interpreter + installs declared deps — fixes the x86-on-arm64 mismatch |
| 2 | Legacy virtualenv/conda | fallback for offline / firewalled hosts |

A failed managed attempt does **not** bind an interpreter (`py_available()` stays `FALSE`), so falling through to the legacy tier within the same session is safe.

Also drops the malformed `Config/reticulate` field from `DESCRIPTION` (`conda_env` is not a recognized key; deps are now declared via `py_require()`, kept in sync with `CASSIA_python/setup.py`).

## Testing (arm64, R 4.5, reticulate 1.46 — same as the reporter)

All three tiers verified against the **installed** package:

| Tier | Scenario | `env_method` | Interpreter arch | Result |
|---|---|---|---|---|
| 0 | `RETICULATE_PYTHON` set | `user` | arm64 | ✅ respects user env |
| 1 | normal / online | `managed` | arm64 | ✅ correct arch, deps auto-installed |
| 2 | managed forced to fail (simulated offline) | `legacy` | arm64 | ✅ falls back to local `cassia_env` |

In every case `library(CASSIA)` loads, `py_cassia` imports, and `runCASSIA_batch` is available.

### Not yet covered
- A full end-to-end annotation run (needs an API key + data). The Python module **imports** cleanly under pandas 3.0.3, but runtime behavior on pandas 3.x wasn't exercised. If a tested upper bound is desired, pin in `.CASSIA_PY_DEPS`.
- Consider a patch version bump (1.3.9 → 1.3.10) before release.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1b4fcfc672e8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.