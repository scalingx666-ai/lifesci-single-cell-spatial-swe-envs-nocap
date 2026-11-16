# Issue

**Title:** Build container actions & Dockerfile fix

## Description

- Add container build and publish workflow (requires secrets to be set)
- Fix Dockerfile to build specific tag instead of latest from git repo
- Update container badge con README

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `24fafecfce52`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.