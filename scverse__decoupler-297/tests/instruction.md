# Issue

**Title:** Refactor ensmbl_to_symbol to reuse _download

## Description

## Summary
- Replaces raw `requests.get` calls in `ds.ensmbl_to_symbol` with the centralized `_download` function (retries, progress bars, streaming)
- Fixes mirror fallback to actually switch between Ensembl mirrors (`www`, `useast`, `uswest`, `asia`)
- Adds robustness against empty/invalid BioMart responses by validating the parsed DataFrame before returning

## Test plan
- [x] `pytest tests/ds/test_utils.py` passes consistently (5/5 runs)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6249825d8e1d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.