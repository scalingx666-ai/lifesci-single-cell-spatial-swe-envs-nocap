# Issue

**Title:** fix: report inconclusive package mutation diagnostics

## Description

## Revised upstream PR #30

Upstream:
Source and qualification record:

HEAD: `5792c83f716e3e5410f87a48c1591f478f1f3212`, rebased onto upstream `371938deefd77b9e6a95d2a0c3e2d3c6ead7eaac`. Current main is `ab114dcb1aad5cc1b2a53c58bc3ad3fcacd1107c`; the intervening main changes do not change kit files.

## Maintainer feedback addressed

A positive nonzero exit with the exact last nonempty line `FAIL` remains an `ok` rejection under the protocol in `kit/SUBMIT.md`. Missing shell, timeout, launch error, negative signal status and malformed or contradictory output remain inconclusive. Positive shell-like exit codes are not reserved by the protocol.

Existing clean PASS behavior remains unchanged; exact-line PASS hardening is a separate change. This supersedes the prior PASS-only interpretation.

## Local verification and scope

54 local synthetic tests passed. The test suite did not execute real scientific scripts. These are local results, not GitHub CI or new scientific results.

The root `SHA256SUMS` is intentionally unchanged; its regeneration and verification against the final integrated tree are left to the maintainer.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ab114dcb1aad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.