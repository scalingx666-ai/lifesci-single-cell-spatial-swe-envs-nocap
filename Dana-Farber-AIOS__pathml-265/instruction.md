# Issue

**Title:** Fix env setup

## Description

This PR should help with environment setup problems. 

- Removed `spams` as a dependency (#142). Instead, if a user wants to use Vahadane stain normalization, we check if spams can be imported and throw an error if not. Also added a note in the documentation pointing to the spams website for users to install. We have faced a lot of issues with spams installation, so this should make things smoother especially since many users have no need for the one functionality which requires spams
- Updated `environment.yml` with a working and reproducible environment that supports deepcell (#259)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9d31034f592b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.