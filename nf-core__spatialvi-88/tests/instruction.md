# Issue

**Title:** Add quality control metrics as MultiQC custom content

## Description

This PR adds the quality controls metrics from the report to MultiQC as custom content. Additionally, the way the metrics are presented in the report are harmonised to be shown in a more similar manner.

This is related to #40.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a353aaec2c25`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.