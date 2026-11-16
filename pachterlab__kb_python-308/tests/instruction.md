# Issue

**Title:** High-performance scaling optimizations for large-scale datasets

## Description

This PR introduces critical algorithmic and I/O optimizations to the kb_python core processing paths. By replacing sequential Python loops with vectorized operations and implementing memory-safe streaming, these changes enable the tool to scale gracefully to multi-million cell datasets.

 Optimizations:
   - collapse_anndata (Vectorized): Replaced manual sparse column loops with a single sparse matrix-matrix multiplication (X @ S).
       - Performance: Achieved a ~2900x speedup on a 100k sample and reduced full-scale (6.7M cells) processing time from ~1 hour to 3.4 seconds.
   - do_sum_matrices (1-Pass Merge): Switched to a single-pass streaming merge with a temporary body file.
       -  Performance: Improved runtime by 1.72x while maintaining O(1) memory safety.
       -  Integrity: Uses strict integer arithmetic when processing count matrices to ensure bit-exact precision (addressing float rounding risks).
   - generate_kite_fasta (KITE Ref Gen): Optimized collision detection from $O(N^2)$ to $O(N)$ using dictionary-based lookups.
       * Performance: Reduced runtime for 10,000 features from ~80s to ~3.5s.
   - validate_mtx: Replaced full-file loading with header-only inspection using scipy.io.mminfo.
       * Performance: Reduced validation time by ~1800x, turning a linear file read into a constant-time check.

  Dataset Used for Validation:
  All performance metrics and parity checks were conducted using the following real-world dataset:
   * Source: 10x Genomics PBMC 10k (Chromium v3)
   * Matrix: Raw feature-barcode matrix (contains all 6.7M+ detected barcodes)
   * Dimensions: 6,794,880 barcodes x 33,538 features
   * URL: 10x PBMC 10k v3 Raw Dataset
     (https://cf.10xgenomics.com/samples/cell-exp/3.0.0/pbmc_10k_v3/pbmc_10k_v3_raw_feature_bc_matrix.tar.gz)

  Scientific Parity & Compliance:
   * Numerical Parity: Confirmed exact scientific parity ((X_old != X_new).nnz == 0) across all optimized paths using the 6.7M cell dataset.
   * MatrixMarket Compliance: Body lines are explicitly formatted as integers when multimapping is disabled, ensuring strict compliance with the .mtx format.
   * Regression Suite: All existing tests pass. Added new regression tests for do_sum_matrices covering integer formatting and complex sparse overlapping merges.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0391b45f744f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.