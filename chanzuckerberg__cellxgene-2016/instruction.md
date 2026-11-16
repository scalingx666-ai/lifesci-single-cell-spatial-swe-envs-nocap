# Issue

**Title:** P value and Log fold change not showing up for all DE results

## Description

The HistogramFooter needs to distinguish between an undefined
value and a value of 0.  If the pvalAdj was 0, then the logFolChange
was previously not showing up.

 #1888

#### Reviewers
**Functional:** @seve 

**Readability:**

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `db559467a2e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.