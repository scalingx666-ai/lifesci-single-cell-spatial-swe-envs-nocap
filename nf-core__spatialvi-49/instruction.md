# Issue

**Title:** Add non-ARM64 Conda profile for report modules

## Description

<!--
# nf-core/spatialtranscriptomics pull request

Many thanks for contributing to nf-core/spatialtranscriptomics!

Please fill in the appropriate checklist below (delete whatever is not relevant).
These are the most common things requested on pull requests (PRs).

Remember that PRs should be made against the dev branch, unless you're preparing a pipeline release.

Learn more about contributing: [CONTRIBUTING.md](https://github.com/nf-core/spatialtranscriptomics/tree/master/.github/CONTRIBUTING.md)
-->

This PR adds the missing Conda environment specifications for the report modules, which currently only work on non-ARM64 architectures. This is due to an issue with Quarto and Pandoc: Quarto `1.2` in Conda has issues with file paths that are resolved in `1.3`, but `1.3` requires a Pandoc version that is not available on ARM64. This PR thus only solves adds usability of the `conda` profile for downstream analyses on non-ARM64 systems, but containers still work fine for ARM64 as well.

## PR checklist

- [x] This comment contains a description of changes (with reason).
- [x] Make sure your code lints (`nf-core lint`).
- [x] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [x] Usage Documentation in `docs/usage.md` is updated.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1642b1c61dfd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.