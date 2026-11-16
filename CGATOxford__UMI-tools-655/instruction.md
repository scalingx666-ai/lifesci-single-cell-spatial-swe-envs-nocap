# Issue

**Title:** Update testing suite to pytest

## Description

In running tests for PR #654, I ran into an issue with testing on my python3.11 platform. The nose package itself was running into import errors, and on further digging does not seem to be maintained any longer.

So I've lightly rewritten tests/test_style.py and tests/test_umi_tools.py to use pytest. 

The tests now run for python3.11, so I expanded the range of Python versions in GitHub actions. Unfortunately, `umi_tools` doesn't compile under python3.12, which I think is a known issue #627.

Also, not all the tests run successfully, which I guess is related to the non-deterministic issue #362 and PRs #550, #98.

This may not be the kind of contribution you're looking for, but I ended up doing the work so I thought I'd hand it over 😄

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0a037ba35562`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.