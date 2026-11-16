# Issue

**Title:** [python] Store array references until submit write

## Description

**Issue and/or context:**
#4311 aims to provide a zero copy write path but at the python side when setting individual columns with data the user can pass temporary objects which forces to always copy the data on that code path to avoid segfaults

**Changes:**
This PR stores the references of the object used to set individual columns until the query is submitted and disable memory copy from that code path.

**Notes for Reviewer:**

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b8a91dd6b5e5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.