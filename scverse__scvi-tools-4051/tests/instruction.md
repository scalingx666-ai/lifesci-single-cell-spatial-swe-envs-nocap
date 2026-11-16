# Issue

**Title:** fix: SCANVI registry, NB mixture sampling/theta2, MULTIVI protein covariates

## Description

- SCANVI.from_scvi_model now honors the `registry` argument instead of always using the scVI model's registry, fixing the datamodule (adata=None) workflow (#4026).
  - NegativeBinomialMixture.sample draws the mixture component per sample in `sample_shape` rather than reusing one draw per batch element (#4027).
  - NegativeBinomialMixture stores `theta2` as a broadcast tensor instead of a tuple, so `sample` and `log_prob` work when it is passed; fix its docstring (#4028).
  - MULTIVI's protein decoder (DecoderADT) now forwards `deep_inject_covariates` to its hidden FCLayers instead of always injecting covariates (#4025). This changes the default protein decoder architecture: previously saved MULTIVI models with protein data will not load.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `86251eb6cd13`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.