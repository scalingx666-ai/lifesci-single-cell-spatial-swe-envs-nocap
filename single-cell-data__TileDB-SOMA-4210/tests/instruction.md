# Issue

**Title:** [python] Document supported workflows for registration functions

## Description

**Issue and/or context:** SOMA-275

**Changes:** Update `register_h5ads()` docstrings to document the two supported append-mode workflows. I also reworded some of the narrative text for clarity.

**Notes for Reviewer:** This also restructures some of the additional narrative text to use indentation rather than underlines to separate sections, which aligns with Google style docstrings.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5f20f84badf7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.