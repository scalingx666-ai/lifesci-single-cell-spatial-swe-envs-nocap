# Issue

**Title:** [c++] Implement buffer resize and resubmission for read queries

## Description

**Issue and/or context:** [SOMA 796](https://linear.app/tiledb/issue/SOMA-796/check-query-incomplete-status-reason-and-cancel-if-not-completing)

**Changes:**
This PR introduces the following changes:
- Enable read buffer resize in case the read query returns zero results due to insufficient buffer size. Adds a retry limit for up to 3 times except for incomplete queries which return data.
- Refactor different memory allocation scheme selection to make `ArrayBuffers` generic.
- Extend the `ColumnBuffer` public API to report maximum capacity for reads

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `68cf78d111c9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.