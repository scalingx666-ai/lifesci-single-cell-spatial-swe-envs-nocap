# Issue

**Title:** ci: bump codecov-action to v6 to fix signature verification

## Description

`codecov-action@v5` verifies the codecov CLI binary against Codecov's old Keybase key, which they bricked after migrating accounts. Uploads now fail with `Could not verify signature`. `@v6` (= 6.0.2) ships the updated key. Version pin bump.

Ref:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ddf4bd3be004`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.