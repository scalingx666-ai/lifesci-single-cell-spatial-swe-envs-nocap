# Issue

**Title:** [r] Fix resume-mode writes to new/empty arrays

## Description

**Issue and/or context:** [SOMA-952] When `ingest_mode = "resume"` is used and the target array is new or empty the coordinates check returns 0 causing the write to be skipped entirely.

**Changes:**  

- Added logic to handle empty coordinates in resume-mode's deduce logic within `write_soma.TsparseMatrix`.
- New "Resume-mode sparse array to new URI preserves data" test
 
**Notes for Reviewer:** This will be stacked on #4452 to add the missing test noted there.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `46426b180467`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.