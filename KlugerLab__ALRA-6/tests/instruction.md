# Issue

**Title:** Switching to quantiles and adding support for intel MKL implementation of SVD

## Description

-Added a flag `use.mkl` for users who have installed [rpca-mkl](https://github.com/KlugerLab/rpca-mkl), resulting in dramatic speedups over the default [rpca](https://www.rdocumentation.org/packages/rsvd/versions/1.0.1/topics/rpca)-based version. 
-When choosing `k`, we no longer use the the normal distribution to approximate the distribution of spacings and compute p-values. Instead, we set `k` to correspond to the largest spacing that is more than 6 standard deviations from the "noise" singular value spacings. This leads to effectively the same choice of `k` as the original version, but does not make the normality assumption (that is not true).
-Instead of thresholding based on the most negative value of each gene, we threshold based on the 0.001 quantile, which is more robust to outliers. By setting the quantile probability to 0, you will restore the original behavior of thresholding by the most negative value.
-Fixed bug which introduced NAs during the scaling process for some datasets

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55a95cc54022`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.