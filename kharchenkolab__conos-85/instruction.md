# Issue

**Title:** changes to getPerCellTypeDE

## Description

* Changes as described here: 

Refers to this issue: 

* Checks that the count data are integers. If not, DESeq will often throw the error `"some values in assay are not integers"`. My solution is to explicitly check that the counts are whole numbers---if not, throw an error asking the user to fix it. 
* Add the flag `remove.na` (default TRUE) which removes NAs from the DEseq results

* Also updates documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1561dcfdbce4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.