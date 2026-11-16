# Issue

**Title:** avoid log4j

## Description

Pin bioformats version to ensure that we aren't vulnerable to [log4j](https://logging.apache.org/log4j/2.x/security.html) hacks

Any bioformats version since v4.0.0 and should be safe ()

Thanks for pointing this out @dmbrundage

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0baf8fbdb948`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.