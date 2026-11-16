# Issue

**Title:** [r] update website DESCRIPTION

## Description

examples weren't using loaded in %>%, even though there was a `importFrom` call.  I think the easiest way around this is just reexporting magrittr::`%>%`.  Seems like that was the strategy dplyr used as well.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f4522e297b60`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.