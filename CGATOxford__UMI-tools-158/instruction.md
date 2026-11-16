# Issue

**Title:** {ts} add expect cells option

## Description

Introduces the `--expect-cells` option for `whitelist` - as per the [CellRanger pipeline](https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/using/count)

This is a half way house between full automation and the user defining the exact number of cells present. Should allow the user obtain an automatic estimate of the number of true cell barcodes with some prior information about the upper limit on how many cells have been sequenced. Use of this options assumes the user has at least a reasonable estimate of the number of cells as discussed [here](https://assets.contentful.com/an68im79xiti/57MmukfLzqI4WMeyKQMqom/557f2d3119e7cd7bb819a22b28118925/CG000091_10x_Technical_Note_Guidelines_on_Accurate_Target_Cell_Count.pdf) and that the capture rate exceeds 10% (reasonable assumption for 10X and indrop, not for dropseq).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f5fb2ca36062`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.