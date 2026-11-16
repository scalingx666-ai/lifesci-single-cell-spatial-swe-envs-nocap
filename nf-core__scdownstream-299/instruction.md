# Issue

**Title:** Warn when reference models are used with per-label integration

## Description

## Summary
- Log a warning in `SUB_INTEGRATE` when `integrate_per_label` is enabled together with a reference model (`scvi_model`, `scanvi_model`, `scimilarity_model`, or `symphony_reference`), since query mapping bypasses per-group training and can yield identical embeddings across label groups.
- Validate `integrate_per_label_whitelist` against `obs[split_col]` via nf-anndata before `SPLITCOL`, instead of relying on post-split subset filenames.

## Test plan
- [x] `nf-test test --profile +apptainer subworkflows/local/sub_integrate/tests/main.nf.test`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dfc1482d9ece`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.