# Issue

**Title:** Support Valkey

## Description

This PR adds support for `Valkey` while trying to be as unintrusive as possible: we are gating Valkey module with a feature flag and conditionally enable symbols (`src/redis/raw.rs`) and headers (`build.rs`) for it.

We are also adding end-to-end tests, again, w/o interfering with the existing flow: these tests require docker engine being available on the host since we are utilizing test containers for convenience and isolation and so they are also put behind a feature flag. CI jobs also added but not listed as wanted by the release job (also the Redis Cell for Valkey is not yet incorporated into the release job, we can address this in a follow-up if this PR gets accepted, so that artifacts are published for Valkey as well).

Utility commands are appended to `Makefile` for better DX.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e23dfec35985`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.