# Issue

**Title:** Update merfish.toml

## Description

Hi,

it seems the config file merfish.toml is not up to date anymore and creates error when directly integrated into the code.
As suggested in this issue #69, all it needs is to use the example config file in the same folder that is up to date.

This PR is simply implementing these simple modifications so other people don't have to do the same work :)

Thanks for the great repo!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `52039e813093`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.