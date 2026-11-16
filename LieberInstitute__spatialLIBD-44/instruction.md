# Issue

**Title:** In gene_set_enrichment use alternative greater

## Description

While using `gene_set_enrichment` @sparthib noticed she had a significant result for a layer enrichment/gene-set pair with an OR = 0.  The gene list she was using had no overlapping genes with genes enriched for in WM, so the OR=0, but the pval < 0.05. Currently the `fisher.test` is using the default `alternative = "two.sided"` so any OR != 1 can be significant so this result is technically correct but I think deviates from described use of this function, where we are looking for where gene sets are enriched or over represented in the models significant genes, where the OR > 1. I propose we change to using `fisher.test(alternative = "greater")` to avoid detecting OR < 1. 

I also included a warning message for genes sets with n < 25 as in practice we thought they had too little power for good results.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `48bd1dd2ee84`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.