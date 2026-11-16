# Issue

**Title:** Fix travis testing

## Description

Hello Luke, Belinda, and Alicia,

Wouter and I noticed splatter wasn't passing the travis tests. We had a look and fixed two small issues:
- Added zimbwave to imports instead of suggests (25540a9)
- Added libgsl-dev apt package to be installed, for gsl/copula/zinbwave (2ea64a1)

You can check [our travis](https://travis-ci.org/dynverse/splatter/jobs/304827710) to see that splatter is now able to build.

Kind regards,
@Zouter and @rcannood

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b78f0b52f7ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.