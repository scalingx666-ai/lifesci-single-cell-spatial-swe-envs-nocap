# Issue

**Title:** Make pyreadr an optional dependency to avoid AGPL/BSD license conflict

## Description

## Summary

- `pyreadr` is AGPL-3.0 licensed, which conflicts with `infercnvpy`'s BSD license when bundled as a required dependency
- `pyreadr` is only used in one place: `read_scevan()` in `src/infercnvpy/io/_scevan.py` (three `pyreadr.read_r()` calls)
- This PR moves it to an optional `scevan` extra and imports it lazily inside the function

## Changes

**`pyproject.toml`**
- Remove `"pyreadr"` from `[project] dependencies`
- Add `optional-dependencies.scevan = ["pyreadr"]`

**`src/infercnvpy/io/_scevan.py`**
- Remove top-level `import pyreadr`
- Add `try/except ImportError` guard inside `read_scevan()` before the first use, following the same pattern as `rpy2` (`_copykat.py`) and `gtfparse` (`_genepos.py`)

## User impact

- `pip install infercnvpy` — no longer installs AGPL code; `read_scevan()` raises a clear `ImportError` with install instructions if called without the extra
- `pip install 'infercnvpy[scevan]'` — identical behaviour to before

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `89aac1ea0bdf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.