# Issue

**Title:** Update DESCRIPTION

## Description

I was getting the following error when running devtools::install_github().

'Error in read.dcf(path) : 
  Line starting 'which real cells pre ...' is malformed!'

reformatting the DESCRIPTION fixed the error.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f39e9cab90f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.