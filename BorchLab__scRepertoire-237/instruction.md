# Issue

**Title:** Add filterMulti in combineBCR function

## Description

Hi Nick,

Here is a pull request to add the filterMulti parameter in the combineBCR function (like in the combineTCR function) in case we want to keep and paste multiple IGH/IGLC results for the same barcode.
I had to adjust filteringMulti input (to consider both IGK and IGL as IGLC) because I had some issues with barcodes having multiple BCR results. For exemple, I had one case with 1 IGH + 1 IGK + 1IGL with the IGK and IGL having the highest number of reads. The IGK and IGL were kept and the IGH were lost.
I also modified the parseBCR function to make the paste work (inspired from the parseTCR function).

Simon

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4b607a906d34`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.