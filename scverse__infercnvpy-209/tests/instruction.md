# Issue

**Title:** perf: twice as fast tl.infercnv (parallel reference means, fused band and CSR assembly, zero-baseline smoothing)

## Description

Summary: This PR makes `tl.infercnv` about twice as fast and leaner in memory, in memory as well as for dask and backed input. On the 10x Atera data (16 cores), 661k cells now take 5.4 s instead of 11.5 s, and 154k cells read lazily with dask take 7.6 s instead of 15 to 19 s. The output is unchanged, apart from 26 of 28.3 million kept values at the edge of the noise band (explained below).

Changes:
- Reference means:
  - They are now computed by a parallel numba kernel that sums the reference cells per category in float64.
  - Before, this step ran serially and took 11.5 s of the 22 s at 661k cells; it now takes 0.1 s.
  - For lazy input, blocks without reference cells are no longer read.
- Noise band and result:
  - The noise band is computed in one kernel call over the reference rows, without copying them and without writing output.
  - The main kernel counts the kept values itself, and all blocks are written into one CSR result whose arrays grow in place, so the `sp.vstack` that doubled memory is gone.
  - For a dense input matrix, the result is allocated at full size and shrunk at the end, with a fallback to growing if the allocation fails.
- Sparse cells: a cell with few stored values starts from the window sums of the zero baseline, computed once, and only its stored values add their difference to the windows that contain them. This is the approach of #192, done inside our kernel. Denser cells keep the prefix sums. At 5 % density this cuts the kernel time by 26 %.
- Lazy and backed input: blocks are read ahead in background threads (2 for backed, 4 for dask), so reading overlaps with computing.
- The check that a CSR matrix has sorted indices without duplicates is now a parallel kernel instead of scipy's serial check.

Results: Every change is bitwise identical to the one before it, except the reference means. They are now summed in float64 instead of scipy's float32 mean, which flips 26 of 28.3M kept values at the band edge at 154k cells and 192 of 130M at 661k. In-memory results now match the dask path exactly; before, the two differed by exactly these values.

Benchmark (HMGU cluster, 16 CPUs on 8 physical cores, all three versions in the same job; "memory" is the growth over the loaded data):

| | main | this PR | #192 |
|---|---|---|---|
| 154k cells, in memory | 3.0 to 3.2 s, +0.7 GB | 1.6 to 1.7 s, +0.55 GB | 8.0 s, +10.9 GB |
| 661k cells, in memory | 11.0 to 12.2 s, +2.1 GB | 5.3 to 5.5 s, +1.1 GB | 11.3 to 11.9 s, +4.2 GB |
| 154k cells, dask | 15 to 19 s | 7.5 to 7.7 s | |
| 154k cells, backed | 12.8 to 13.0 s | 6.1 s | |
| 661k cells, dask | 36 to 47 s | 21 s | |

The ratio of CPU time to wall time rose from about 8 to about 13, which is close to the limit of 8 physical cores with hyperthreading.

Testing: The numpy-reference kernel tests pass unchanged and now cover both the prefix-sum and the zero-baseline path. A new test covers the CSR assembly with and without the preallocated arrays. `test_reads_each_block_once_per_pass` is adapted, because the reference pass now reads only blocks that contain reference cells. The full suite passes on the cluster (333 passed, 12 skipped), and so do prek and mypy.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b3f3db262413`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.