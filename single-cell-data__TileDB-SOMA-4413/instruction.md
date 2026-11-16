# Issue

**Title:** [python] Clamp `extent` using max domain

## Description

**Issue and/or context:** [SOMA-416](https://linear.app/tiledb/issue/SOMA-416/python-dataframe-dimension-extent-set-incorrectly-when-domain-is-small)

**Changes:**
This PR uses max domain to clamp the dimension extent.

**Notes for Reviewer:**
Before the introduction of current domain the user specified domain was the max domain and the extend couldn't be larger that the domain. With the introduction of current domain the max domain is now set based on the datatype limits and the user specified domain in now the current domain.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `08facd4f2cf4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.