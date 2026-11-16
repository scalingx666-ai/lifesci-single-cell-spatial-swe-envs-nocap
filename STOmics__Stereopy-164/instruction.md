# Issue

**Title:** Work brach - added .obs['cell_communities'] to return data and fixed bugs

## Description

stereopy exp data and ms data now have  _ann_data.obs['cell_communities'] with CCD labels.

Fix for bug with empty tissue creating exceptions for table plots.
Fixed the bug with missing boxplots.
Accepted suggestions for minor improvements.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `63b8390221dc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.