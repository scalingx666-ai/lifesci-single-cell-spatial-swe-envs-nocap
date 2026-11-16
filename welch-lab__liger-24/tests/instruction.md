# Issue

**Title:** New plotting options and minor changes

## Description

* Add plot.log2 option to kSuggestion function
* Add do.plot option to selectGenes and calc_dataset_specificity
* Allow run_tSNE even if quantile alignment not done
* Allow plotByDatasetAndClusters even if no clusters set
* Increment rand.seed for each consecutive rep of optimizeALS
* Allow kl_divergence_uniform to tkae object or H matrices
* Make do.plot=F default in get_factor_markers
* Fix gene labeling in gene.plot

The space removal makes the second commit look very messy!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c61003d55a8d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.