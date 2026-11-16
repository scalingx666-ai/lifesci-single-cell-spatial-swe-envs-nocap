# Issue

**Title:** Fixing F-distribution degree of freedom bug

## Description

I rewrote the getOverdispersedGenes function from STDeconvolve in Python so I could integrate it directly into my Python package, avoiding the need to rely on the R package or run R code in the background.

During this process, I reviewed the OD Score computation in detail and identified a critical bug. After several checks, I found that the function mistakenly swaps the number of spots (cells) with the number of genes. This mix-up affects the degrees of freedom in the F-distribution calculation, leading to higher OD scores that cause fewer genes to be selected when applying a threshold.

Here’s an example of the impact:

For a dataset with 887 genes:

- With the bug: 59 genes were identified at an alpha level of 0.1.
- Without the bug (fixed): 159 genes were identified.

Similarly, at alpha = 0.05, the original method identified 46 genes, while the corrected version identified 141 genes.


For a Nanostring DSP dataset with 1,414 genes:

- With the bug: Only 1 gene was identified.
- Without the bug (fixed): 607 genes were identified.

I would like to share this fix with you for review. Please let me know if you have any feedback.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7b0e0a44eca3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.