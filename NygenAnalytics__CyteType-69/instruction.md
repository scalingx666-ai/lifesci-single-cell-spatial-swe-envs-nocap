# Issue

**Title:** Update version to 0.19.0 and enhance file upload functionality

## Description

- Bump package version to 0.19.0.
- Increase maximum workers for file uploads from 4 to 6.
- Introduce support for uploading chunks to presigned URLs, including progress reporting and error handling.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d45fe3f3dc2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.