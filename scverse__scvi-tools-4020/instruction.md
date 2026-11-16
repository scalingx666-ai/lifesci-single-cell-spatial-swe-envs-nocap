# Issue

**Title:** feat: Extract some methods of DRVI for easier extention + code improvement

## Description

Dear scvi-tools team,

This PR builds on #4019 (which adds FCLayers `residual` + `forward(**kwargs)`).

The goal here is to extract methods and organize code chunks so that extensions (which may be contributed back to scvi-tools after becoming stable and wanted by users) are possible without repeating large chunks of code. One example is random reconstruction of genes in decoder where users are allowed to reconstruct 20% of genes in a single pass. Implementing such a feature requires big changes if **kwargs here are not extracted.

Specifically, we break `DRVIModule`, `DecoderDRVI`, `SplitFCLayers` and the interpretability mixin at the points a downstream model actually needs to override, instead of requiring a full copy of `generative`/`forward`:
  - `DRVIModule._decoder_cls` / `DecoderDRVI._fc_layers_cls`: swap in a custom decoder or per-split FC layer class
  - `DRVIModule._compute_px_r_logit`: override how the dispersion logit is resolved
  - `DecoderDRVI._apply_split`: override the latent-to-splits mapping
  - `build_gene_likelihood` (in `_distributions.py`) and `get_direct_effect_of_latent_splits` (in `_interpretability_mixin.py`). pulled out of `generative` and the interpretability mixin into standalone, reusable functions: `generative` and `DecoderDRVI.forward` also accept and thread `**kwargs`, so per-call context (e.g. an encode/decode flag) can reach a subclass's overrides without a new keyword argument.

Note 1: diff will be less once #4019 is merged.
Note 2: There is no change in model behaviour

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb89ad9769ae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.