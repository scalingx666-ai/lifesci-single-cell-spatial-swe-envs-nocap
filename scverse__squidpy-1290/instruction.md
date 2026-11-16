# Issue

**Title:** docs: correct img_res_key references in spatial plotting

## Description

## Description

Correct three docstring references from `img_key` to `img_res_key` in spatial plotting documentation, including the shared `scale_factor` description, to match the existing API.

## How has this been tested?

- Passed pre-commit checks for both changed files.
- Built the complete documentation with Sphinx warnings treated as errors (`-W`); zero warnings.
- Verified the generated `spatial_scatter` and `spatial_segment` API pages and their parameter signatures.

## Closes

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `25eacd2beb83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.