# Issue

**Title:** Fix Bug in IntegrateEmbeddings when Ref is specified

## Description

Dear developpers,
I noticed that if I want to use IntegrateEmbeddings but I specify `dims.to.integrate` and `reference` I get an error:
```txt
Error in dimnames(x) <- dn : 
  length of 'dimnames' [2] not equal to array extent
```
I could find the origin of the problem. I also so that there was a similar commit:  but unfortunately only the case where reference was not specified was fixed.

You find here the fix for the case where `reference` is specified.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2756b40ebe0a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.