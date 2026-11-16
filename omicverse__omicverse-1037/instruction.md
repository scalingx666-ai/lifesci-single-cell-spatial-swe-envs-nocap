# Issue

**Title:** storage='disk' GPU mode: fix corrupted pinned copies; 7x faster gzip reads

## Description

(merged, not released).

## Bug (correctness)
GPU blocks are copied through a reused per-thread pinned buffer and `cupy.ndarray.set()` from pinned memory is asynchronous. When the GPU queue was busy, the buffer was refilled before the copy ran: on the uncompressed SEA-AD file 2–6% of the non-zeros were wrong per pass, different each time (master: three passes gave column sums 33.5e9 / 34.7e9 / 34.5e9 instead of 35.6e9). Small test files fit in one piece, so the tests did not see it. Each copy now waits on its stream.
- `test_staging_copy_waits_for_the_device` queues a ~0.2 s busy kernel ahead of the copy and refills the buffer immediately; fails without the wait.
- `test_gpu_blocks_exact_through_pinned_buffer`: blocks split into many pieces equal the file.

## Speed
Compressed/chunked h5ad files are decoded by anndataoom-fast `Dataset.read_into` (new in 0.1.4; older versions fall back to `read`) straight into the pinned buffer in the GPU dtype (indices as int32), with cpus/workers decoder threads per block. SEA-AD public release (gzip, 7.6B nnz): **60 s → 8.7 s per pass**; sums and nnz exact on three repeated passes. Uncompressed: 3.3 s per pass, exact.

SEA-AD full Fig. 4 workflow with the fix (uncompressed, one H100): 71 s, 5 GB host memory; QC/HVG identical to an exact numpy recomputation.

## Tests
GPU tests run on an H100 (19 passed); CPU: 15 passed, 3 GPU skipped.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0cca13315c09`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.