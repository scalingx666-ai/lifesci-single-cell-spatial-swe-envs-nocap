# Issue

**Title:** Update version to 0.19.1 and improve file upload initiation

## Description

- Bump package version to 0.19.1.
- Modify the file upload initiation to include the file size in the request, enhancing the upload process.
- Update validation logic to ensure the number of presigned URLs is at least equal to the expected chunk count, improving error handling during uploads.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bd0a9776faa8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.