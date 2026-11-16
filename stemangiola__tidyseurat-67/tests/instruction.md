# Issue

**Title:** Increase unit test coverage

## Description

I created additional unit tests for the dplyr, tidyr and pillar adapters, and the `get_abundance` utilities. 

This brings tidyseurat test coverage to 78.64%, as calculated by dev_tools::test_coverage(). This still seems a bit low, but the remaining untested code does not seem amenable to testing. For example, plotting functions.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `823c3c52a922`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.