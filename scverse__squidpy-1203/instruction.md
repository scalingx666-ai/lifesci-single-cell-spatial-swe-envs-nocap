# Issue

**Title:** ci: bump codecov-action to v6 to fix signature verification

## Description

`codecov-action@v5` verifies the codecov CLI binary against Codecov's old Keybase key, which they bricked after migrating to a new account. The upload step now fails with `Could not verify signature`, and because `fail_ci_if_error: true` this hard-fails the Coverage job on every PR.

`@v6` (= 6.0.2) ships the updated key. One-line pin bump.

Ref:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b1cbc53f9626`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.