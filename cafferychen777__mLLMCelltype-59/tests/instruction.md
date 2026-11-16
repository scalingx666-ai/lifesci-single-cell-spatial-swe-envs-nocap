# Issue

**Title:** fix: Add robust type checking for API responses

## Description

This commit adds comprehensive type checking for API responses across all model providers:

- Add validation to ensure response content has the expected structure
- Add explicit checks to verify that response content is a character string before using strsplit
- Add detailed error logging for unexpected response formats
- Gracefully handle non-character responses by returning NULL instead of crashing
- Implement consistent error handling patterns across all API processing functions

This fixes the 'non-character argument' error that occurred when strsplit was called on non-character response content, which could happen due to API format changes, streaming responses, rate limiting, or network issues.

The changes make the code more robust against various API response scenarios and provide better diagnostic information when errors occur.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `320839a15d70`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.