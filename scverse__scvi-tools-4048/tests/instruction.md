# Issue

**Title:** fix(cytovi): DE test mode, DA stability/alignment, posterior scale, supplied AnnData

## Description

- differential_expression: always forward `test_mode` to `_de_core`, not only when `lfc_clipping=True` (#4037)
- log_median: compute log(median(exp(x))) in log space to avoid underflow/overflow producing non-finite DA scores (#4040)
- get_aggregated_posterior: use the standard deviation (sqrt of the returned variance) as the Normal/Student-t component scale (#4034)
- get_aggregated_posterior / get_sample_logprobs: use the supplied AnnData for default indices and query latents instead of the training AnnData (#4035)
- differential_abundance: keep cell names in the result index, align conditions to sample columns by sample id, support groupby equal to the sample key, and raise on invalid sample/condition designs (#4036)

Adds regression unit tests for each fix and changelog entries.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fe145e9c2842`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.