# Issue

**Title:** fix(volcengine): support current Ark CLI API key listing

## Description

## Summary

Fix Ark CLI 1.0.46 API key discovery after a successful Volcengine sign-in. Prefer `profile apikey list`, and fall back to `profile keys list` only when the CLI explicitly rejects the new subcommand. Auth, timeout, and malformed-output failures are not retried through the legacy command.

## Area

- [x] Server / gateway / API
- [x] Tests / harness / CI

## Change Type

- [x] Bug fix

## Verification

- Passed in WSL: `python -m pytest tests/test_volcengine_connector.py -q -x --tb=short`.
- Passed: targeted Black and Ruff checks, and `git diff --check`.
- Full offline run (`python -m pytest -n 4 --dist loadfile -x --tb=short`) stopped at build and kernel failures in the local WSL environment (1,188 passed before stopping).
- Live Ark CLI accepted the new subcommand. Key synchronization and inference were not verified end to end because the existing SSO session failed to renew its STS credentials.

## Risk and Reviewer Focus

Check the narrow unknown-subcommand detection and the tests for modern and legacy output. Key selection and credential storage are unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4de8520c27f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.