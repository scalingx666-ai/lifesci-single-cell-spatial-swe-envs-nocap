# Issue

**Title:** fix: restore SCTransform fast path and support covariate regression on it

## Description

## Summary

- **Fix a fatal scope bug in the fast path**: commit 642f7f5ef rewrote the residual clip step as `rv$y <- { rv <- rv$y; ... }`. Braces do not create a new scope in R, so this overwrote the whole result list with an empty matrix and every default fast-path call failed at `model_str`. The clip now applies to the local residual before assignment.
- **Delegate truly unsupported combinations to Seurat** instead of erroring out: `conserve.memory`, `reference.SCT.model`, `residual.features`, `vst.flavor = "v1"`, non-default `do.scale`/`do.center`/`return.only.var.genes`, etc.
- **Support covariate regression on the fast path**: `vars.to.regress` (from cell metadata) and arbitrary `latent.data` are removed from the centered residuals with a single post-VST OLS residualization (`stats::lm.fit`, one fit across all genes), matching Seurat's regression semantics — no changes to the C++ kernels were needed because Seurat never feeds these variables into the NB model either. Numeric and factor covariates are supported; regressors are validated for missing values / rowname alignment and recorded in the stored model arguments as `sct.latent.vars`.

## Validation

- Default-path output is **bit-identical** to a pre-change baseline snapshot (`all.equal(..., tolerance = 1e-12)`.
- With `vars.to.regress = "percent.mt"`: max abs difference vs Seurat's native `SCTransform.default` is **8.7e-15** on a scale.data matrix of magnitude ~2.35; row-centering residual is ~1e-17.
- New tests in `tests/testthat/test-sctransform.R` cover default path, continuous/factor regression, `latent.data`, and delegation; all pass, plus the existing choir tests that exercise SCTransform internally (94 assertions) stay green.

Users hitting `SCTransform.Seurat received unsupported arguments...` can now run their original calls unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f909f063733`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.