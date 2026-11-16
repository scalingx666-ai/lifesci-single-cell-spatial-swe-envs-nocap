# Issue

**Title:** Vvalidate input samplesheet for `expected_cells` and `seq_center`

## Description

.

The pipeline now checks `expected_cells` and `seq_center` across grouped rows for the same sample. If the values differ, the pipeline stops and identifies the sample as in [nf-core/rnaseq](https://github.com/nf-core/rnaseq/blob/48cc4b4d016fc9e64b51a20d1cb442a67cef7bcf/subworkflows/local/utils_nfcore_rnaseq_pipeline/main.nf#L200-L204).

Previously, the pipeline used the values from the first row and ignored values from later rows.

The added nf-tests cover matching values, conflicting values, and missing optional values.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bedd1da45ee4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.