# Issue

**Title:** drop `tables` dependency

## Description

Hi @ManuSetty,

This PR addresses two specific issues:

1. **Removal of Unused `tables` Dependency**: The `tables` package does not seem to be used within the codebase, and it creates installation difficulties on Mac M1. By eliminating this dependency, we alleviate issue .

2. **Version Correction in `src/palantir/version.py`**: The version specified was incorrectly set to 1.3.2. This PR updates it to the accurate version, 1.3.1.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `870a9ba88b97`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.