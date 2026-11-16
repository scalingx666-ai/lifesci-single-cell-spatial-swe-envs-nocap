# Issue

**Title:** fix dense int input

## Description

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Integer-valued dense inputs are now automatically converted to floating point for normalization and scaling, preventing dtype-related issues and improving result consistency.
  * Normalization now preserves expected totals after conversion, and scaling produces correctly centered and scaled output for integer inputs.

* **Tests**
  * Added coverage for dense integer input handling in normalization and scaling.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `908e02b8dbdd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.