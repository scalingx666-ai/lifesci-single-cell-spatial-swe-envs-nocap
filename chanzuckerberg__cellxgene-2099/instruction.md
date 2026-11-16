# Issue

**Title:** gene sets summary route

## Description

Back end route implementing gene set summary calculation.  Also includes:
* refactored the error checking logic for gene sets so that anything returned by read_genesets() will be valid, and anything provided to write_genesets() will be validated prior to write (this removes the need for users of the IO tier to separately coordinate error checking)
* test cases for the new route
* slightly improved test cases for the GET /genesets route

 

#### Reviewers
**Functional:** @MDunitz 

**Readability:** @maniarathi

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d3d9237e722`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.