# Issue

**Title:** [ci] Temporarily disable R-devel CI job

## Description

**Issue and/or context:** [SOMA-941]

R-devel (post-4.6.0) removed non-API C symbols (`PREXPR`, `PRENV`, `PRVALUE`) that Bioconductor's `S4Vectors` package depends on. This causes `S4Vectors.so` to fail to load with an `undefined symbol: PREXPR` error, breaking R package dependency installation in CI.

The fix is in S4Vectors 0.49.2 on the Bioconductor devel branch () but has not yet reached the release channel.

**Changes:**

- Comment out the R-devel matrix entry in `ci-pr-r.yml` and `ci-full.yml`
- Each is tagged with `TODO(SOMA-941)` for easy discovery when it's time to re-enable

**Notes for Reviewer:** This failure is already present on `main` and is unrelated to any open PRs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `126c23705fc8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.