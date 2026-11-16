# Issue

**Title:** Ia/insertion radix sorting

## Description

# Description
Previously we added a change for `InsertionIterator` to use a priority queue, as we were experiencing memory errors with the original vector + radixsort method.  However, the priority queue solution is slower, so we planned to bring back the vector +radixsort solution once we determined the problem.



# Tests
- Ran tests in `test-atac_utils.R` which already had tests for writing bedfiles.  
- Used `r/tests/real_data/ArchR_insertions.R` which compares against insertion writing in ArchR, and results remained as we expected.  
- Ran and profiled using a filtered PBMC dataset of 2600 cells

# Details
The problem ended up being pretty simple--just a mistake in the direction of arrows for a conditional within buffer resizing.  Even without resizing within the `nextChr()` call, the iterator still functions at datasets of at least 2600 cells, which indicates that the solution now works.  Memory profiling indicates that usage never spiked beyond 1 GB.  

I also increased the amount of comments so it is a little easier to see the thought process on how loading fragments works

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd37b9d7dbe3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.