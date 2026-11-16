# Issue

**Title:** massively sped up `combineTCR` with Rcpp

## Description

`combineTCR` is one of the most important functions but it's kinda slow, running originally in ~ 24 seconds for `contig_list` on my device. I used the `profvis` profiling library to see the speed bottlenecks, and see that `.parseTCR` is the main time consumer. Looking deeper into the function, this PR solves one of them - finding the indicies of barcodes of `Con.df$barcode`  of length  `N` that are in `data2$barcode` of length `M`, by constructing a barcode index in `O(N+M)` time in Rcpp. This has cut the runtime down to ~17 seconds. I'm working on fully re-implementing `.parseTCR` in Rcpp atm to see if theres another time increase.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3adf21d5f19e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.