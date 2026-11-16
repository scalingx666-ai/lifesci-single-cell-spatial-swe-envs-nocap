# Issue

**Title:** Fix root logging level being set to INFO for all packages

## Description

## Summary
- Replaced `logging.basicConfig()` in `_log.py` with a named `decoupler` logger so importing decoupler no longer sets the root logging level to INFO for all packages
- Updated tests to capture logs from the named logger

## Test plan
- [x] Verified root logger is unaffected after `import decoupler`
- [x] All 31 tests in `tests/pp/test_net.py` and `tests/ds/test_toy.py` pass
- [x] Pre-commit checks pass

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `40092de680f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.