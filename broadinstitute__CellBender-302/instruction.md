# Issue

**Title:** Fix bugs with report generation across platforms

## Description

- make report generation platform-agnostic
- attempt to fix bugs with encoding of HTML (specify UTF-8 encoding, make it fault tolerant)
- fix a failing test due to IndexConverter.get_m_indices receiving torch tensors during posterior generation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `be360063c9f5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.