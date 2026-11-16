# Issue

**Title:** [c++] Fix enumeration value check for MacOS builds

## Description

**Issue and/or context:** 

**Changes:**
Use the `std::string_view` overload to check if value is present in an enumeration because of missing type definition after Xcode 16.3

**Notes for Reviewer:**

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1cfead07aa30`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.