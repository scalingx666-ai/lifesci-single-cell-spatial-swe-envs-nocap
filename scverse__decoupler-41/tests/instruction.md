# Issue

**Title:** [WIP] Add lead_genes and n_genes to enrichment results

## Description

This PR aims to add a util method that could be used by most of the enrichment analysis methods here at the end to optionally melt and annotate the enrichment results with lead genes and the total number of genes in each enriched gene set.

This is loosely based on some manual work I was doing with the outputs of ORA, which I think it should be applicable to other enrichment methods. Feel free to disregard if you had something in the making (with hopefully all these fields :-) ).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `196716ea8e77`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.