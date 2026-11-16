# Issue

**Title:** fix: eigh_threshold and compile=False no longer leak into later runs

## Description

`RCTD.__init__` wrote `RCTDConfig.eigh_threshold` and `compile=False` into module-level flags in `_irwls` / `_likelihood` but never reset them. One run with `eigh_threshold=64` (or `compile=False`) in a notebook kept every later run in that process on GPU eigh (or eager), whatever its own config said.

Found while benchmarking on an L40S (StrataMap breast, 21,425 cells, K=40): a leaked `eigh_threshold=64` made the full-fit step of a later default-config float32 run take 263 s; the same float32 fit takes 44 s in a fresh process.

Every `RCTD` now sets both flags from its own config. A compile fallback triggered by a real compile failure stays sticky. `tests/test_config_state.py` covers both leaks and the sticky fallback (fails on main, passes here); full suite passes locally.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1af2153e6b30`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.