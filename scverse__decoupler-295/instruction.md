# Issue

**Title:** Fix dotplot vcenter=0 ignored due to falsy check

## Description

## Summary
- Fix `if vcenter:` → `if vcenter is not None:` in `_dotplot.py` so that `vcenter=0` correctly applies `TwoSlopeNorm`
- Add `vcenter=0` to the parametrized test to prevent regression

## Test plan
- [x] `tests/pl/test_dotplot.py` passes with all 3 parametrized values (`None`, `0`, `3`)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6249825d8e1d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.