# Issue

**Title:** Fixing the filter sizes

## Description

Hi,
just came across two bugs in the `_running_mean()` function:
1. the size of the filter (`pyramid`) is off by one (`len(pyramid) == window_size-1`. Not a big deal, but slightly inconsistent.
2. as mentioned by #37, due to the way `np.convolve()` works, if the filtersize is bigger than the number of genes, it flips filter and signal, and the result doesn't mean much

1. is an easy fix
2. Two options: either skip the chromosome entirely if there's not enough genes. Or, make the filter smaller, essentially the chromosome yields a single convolution result (all genes on the chromosome go into the convolution). I opted for 2), especially for larger filter sizes, you'd loose alot of data when doing 1)

Thanks for putting together this nice package!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `978fdfd70757`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.