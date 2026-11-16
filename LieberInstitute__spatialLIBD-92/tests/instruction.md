# Issue

**Title:** Check var_registration is syntactically valid  in spatial registration functions

## Description

Add grepl test ([regex source](https://stackoverflow.com/questions/8396577/check-if-character-value-is-a-valid-r-object-name)) for `var_registration` to be syntactically valid. If not, use `makes.names()` to correct to syntactically valid names instead and warn user of the change. Also warn if variable is numeric, and convert to syntactically valid names w/ `make.names()` . 
 
Addresses issues #72 and #48.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4359ed639f75`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.