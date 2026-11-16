# Issue

**Title:** fix: unit tests and reenable running

## Description

#### Reviewers
**Functional:**  @tihuan 

---

A bump in our jest version began running our unit tests in a node environment rather than a browser.  This PR adds SSR checks in various places in order to not make attempts to call window where there is none present.  Also re-enables unit tests on the push_tests workflow.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `01013bcf04d6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.