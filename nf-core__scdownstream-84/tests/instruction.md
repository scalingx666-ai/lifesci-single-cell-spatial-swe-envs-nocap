# Issue

**Title:** Implement meta.expected_cells (cellbender)

## Description

This PR allows users to specify cellbender --expected-cells parameter at the sample sheet. Although this is not required, this parameter and can be optimized for each sample to improve cell classification.

## PR checklist

- [X] Code lints
- [X] Test suite passes (`nextflow run . -profile test,singularity --outdir <OUTDIR>`).
- [X] Check for unexpected warnings in debug mode (`nextflow run . -profile debug,test,docker --outdir <OUTDIR>`). Note that the multiqc process is failing, but is unrelated (#83).
- [X] Usage Documentation in `docs/usage.md` is updated.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `61d0879393c3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.