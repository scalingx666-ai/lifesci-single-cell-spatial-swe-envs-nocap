# Issue

**Title:** Add metric QC function

## Description

Adding a function to aid/standardize the QC process of new `spe` objects based off of work in [Habenula_Visium](https://github.com/LieberInstitute/Habenula_Visium/blob/7fc73e8cb403bcaa035f2451602db3fc0f38b103/code/02_build_spe/02_exploratory_QCs.R#L188-L295), [spatial_NAc](https://github.com/LieberInstitute/spatial_NAc/blob/56c67e7c0421e6dcf71fe2db6ef2c7b62ed15e58/code/05_harmony_BayesSpace/02-compute_QC_metrics.R#L69-L128), and [Visium_SPG_AD](https://github.com/LieberInstitute/Visium_SPG_AD/blob/e13e1a3604aa2dc43d76fa6923541ef403b0b13d/code/07_spot_qc/05_qc_plots_revision.R#L89-L152).  

Utilizes `scater::isOutlier` on three metrics `log2(sum_umi)`, `log2(sum_gene)`, and `expr_chrM_ratio*100`. 
Added functionality for handling spots `in_tissue=FALSE` .

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `30a8b3a02ec9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.