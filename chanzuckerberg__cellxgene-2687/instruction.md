# Issue

**Title:** fix: snakecase to kebab for diffexp-may-be-slow

## Description

The variable diffexp_may_be_slow is set within the python server and used within the javascript client as another variable diffexp-may-be-slow. This PR fixes this divergence and uses a single variable name. The introduced changes have been tested locally and indeed fix the issue that the warning when hovering the DEG button was not shown previously with large datasets.

Original PR: 

All credit goes to: @moritzschaefer 🙏

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7bf5add6efe9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.