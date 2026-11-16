# Issue

**Title:** rename "geneset" to "gene set" in CLI

## Description

#### Reviewers
**Functional:** @signechambers1 

**Readability:** @MDunitz 

---

In the CLI, we want to use "gene sets", not "genesets".  This PR changes:
* the CLI params are changed
* the CSV file header is changed
* the config file names are changed
* and a bunch of misc code in the local_server backend are changed to match

Note that I did not change _all_ instances of "genesets", in particular those where only API/internals are affected.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b00496198d85`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.