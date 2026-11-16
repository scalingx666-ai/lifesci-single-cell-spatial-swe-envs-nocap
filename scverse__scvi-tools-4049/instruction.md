# Issue

**Title:** perf: remove per-minibatch overhead in data loading and inference

## Description

Trimmed port of #4017, plus the crash fix from #4018. Outputs are
  bit-identical before and after.

  - AnnTorchDataset: convert registered covariate DataFrames to NumPy once when data is first materialised, instead of .iloc-slicing every minibatch.
  - auto_move_data / BaseModuleClass.device: read the device from the first parameter instead of building a set over all parameters on every call.
  - get_likelihood_parameters: concatenate the zinb dropout once after the loop instead of on every batch (was quadratic in the number of cells).
  - scrna_raw_counts_properties: convert the COO result of multiply() back to CSR before taking column means.
  - get_normalized_expression(n_samples_overall=..., return_numpy=False): fix the shape-mismatch crash by indexing the returned DataFrame with the resampled cells (RNASeqMixin, CYTOVI, MRVI).

  Benchmark (20k cells x 1200 genes, zinb, covariates, CPU, median of 3):
  differential_expression(mode="change") -45%, one pair -32%,
  get_likelihood_parameters -84%, get_latent_representation -34%,
  get_normalized_expression -20%, training epoch -5.5%.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c2251448185c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.