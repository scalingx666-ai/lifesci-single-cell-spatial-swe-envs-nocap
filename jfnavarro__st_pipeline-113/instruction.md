# Issue

**Title:** Check that mapped.bam file exists

## Description

# Description

This PR ensures that the `mapped.bam` file is present when running with `--disable-mapping`. It fixes an issue where the wrong file was passed to `barcodeDemultiplexing`

Fixes # (issue)
#112 

## Type of change

Please delete options that are not relevant.

- [x] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] This change requires a documentation update

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `036ef4cbb33e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.