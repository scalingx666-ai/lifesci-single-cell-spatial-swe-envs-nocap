# Issue

**Title:** Improve GPU Hamming distance computation

## Description

## Summary

This PR improves the GPU implementation of the Hamming distance metric by making the computation more memory-flexible and better suited for large datasets. The main change is that GPU Hamming computations can now be split into both row and column blocks. This replaces the previous single `gpu_n_blocks` parameter with `gpu_col_blocks` and the new `gpu_row_blocks` parameter.

Before, the result matrix was split only into column blocks using `gpu_n_blocks`, while `gpu_block_width` controlled how much GPU memory was reserved for result values below the cutoff. This already assumed a certain level of sparsity to avoid reserving unnecessary amounts of memory. For larger datasets, it was difficult to choose parameters that kept the number of blocks low enough for good performance while still fitting into GPU memory. Therefore, `gpu_row_blocks` was introduced to also split the result matrix along the row dimension. This makes it possible to adjust the block size so that each block fits into GPU memory for larger input sizes.

In first tests, the new GPU Hamming distance metric can run the largest full TCR dataset I currently have access to, containing around 8 million cells, in about 2 minutes on an NVIDIA A30 GPU. The same computation took around 35 minutes with the CPU Hamming implementation using 64 CPUs. Since this dataset is still too small for extensive stress testing, I also tested the `GPUHammingDistanceCalculator` directly with 25 million synthetically generated unique CDR3 sequences, which took around 30 minutes on an NVIDIA A30 GPU.

## Main changes

- Add row and column block splitting for GPU Hamming distance computation.
- Sort sequences within each row and column block by sequence length to group similar-length sequences for GPU computation.
- Skip unnecessary computations for symmetric distance matrices.
- Add better validation for GPU Hamming parameters.
- Update documentation for the GPU Hamming block parameters.
- Add tests for different block configurations.

## API change

`gpu_n_blocks` has been replaced by `gpu_col_blocks`. A new parameter, `gpu_row_blocks`, has been added.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `26d80f72018a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.