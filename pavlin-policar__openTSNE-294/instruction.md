# Issue

**Title:** perf: threaded scipy FFT backend for the interpolation-based gradient

## Description

Once an embedding spreads out, the interpolation grid grows with it, and the FFTs become almost all of the interpolation-based (`negative_gradient_method="fft"`) gradient's cost: at 44 808 points a converged embedding needs a 1134×1134 grid, and the transforms take about 85% of the time per call. Until now they also always ran on one thread, whatever `n_jobs` said.

This is the second PR in the series splitting up the performance work on `claude/opentsne-cython-perf-69a550`. It is the base of the FFT-side changes (dropping FFTW, float32, and the grid work all build on it).

## Changes
- **scipy FFT instead of numpy FFT** (`matrix_mul_numpy.pyx`). Both wrap pocketfft, but scipy exposes its thread pool through `workers`. scipy is already a dependency; `setup.py` now requires `scipy>=1.4`, the release that added `scipy.fft`. No scipy installable on Python ≥ 3.9 is older than that.
- **Thread count plumbed through.** The four FFT entry points in `_tsne.pyx` take `num_threads` (default 1), and `kl_divergence_fft` passes `n_jobs`. The FFTW backend accepts the argument and ignores it.
- **Transform buffers are kept between calls** instead of reallocated (tens of MB at large grids). Each thread keeps its own, because the transforms release the GIL. Copies in and out are array assignments instead of elementwise loops.
- **1-D uses a real transform** (`rfft`) instead of a complex transform of real input.
- **Kernel evaluated without a function pointer.** A flag lets the kernel inline and hoists the `dof` branch, and the kernel buffer is reused.
- **Two-pass 2-D transform that skips the padding.** The forward row pass skips the all-zero rows, and the inverse skips rows that are never read. This also removes the padded input buffer.

## Measurements
M1 Pro, 8 performance cores, both branches built the same way (`build_ext --inplace`, OpenMP found).

Negative gradient on a synthetic spread-out 2-D embedding (40 clusters spanning about 120 units), best of 6:

| | master | this PR, 1 thread | this PR, 8 threads |
|---|---:|---:|---:|
| 10 000 points | 48.1 ms | 28.0 ms (1.72×) | 14.3 ms (3.36×) |
| 44 808 points | 51.2 ms | 26.9 ms (1.91×) | 16.6 ms (3.09×) |

1-D is unchanged (about 1 ms at 44 808 points; the grid there is tiny).

End to end, 40 000 points in 50 dimensions, 250 early-exaggeration and 500 standard iterations, optimization only:

| | master | this PR | |
|---|---:|---:|---:|
| `n_jobs=1` | 38.9 s | 33.4 s | 1.16× |
| `n_jobs=8` | 19.4 s | 13.3 s | 1.45× |

The end-to-end gain is smaller than the per-call one because the positive gradient is now a large share of each iteration; a separate PR speeds that up.

## Correctness
On the same inputs, the gradient and normalization agree with master to within 1e-12 relative (2-D and 1-D, both sizes), and are bit-identical with and without the per-thread buffers. Final KL after 750 iterations: 3.1092 on master against 3.1088 / 3.1096 here.

## Tests
New: `TestFFTGradientConcurrentThreads` in `tests/test_correctness.py`. It runs the 1-D and 2-D FFT gradients from six threads at once, on embeddings with different grid sizes and both `dof=1` and `dof=0.7`, and checks every result against the serial one. With module-level buffers instead of per-thread ones, both tests fail on all of 5 runs (2-D results off by up to 15 000× relative); with this PR they pass. They take about 3 s.

`pytest tests`: 177 passed, 48 skipped, 1 failed. The failure is `test_affinities.py::TestGenericAffinity::test_call_with_custom_metric_with_unsupported_knn`, which needs `hnswlib`. That was not installed, and the failure is unrelated to this change.

## Notes for review
- The kept buffers live in `threading.local`: per thread, one set of transform buffers for the last grid size and one kernel buffer per kernel. They are freed when the thread exits. A thread pool keeps one set per worker that has run an FFT gradient.
- The FFTW backend is left in place here. A follow-up PR removes it: with these changes, scipy is faster both serially and threaded.

##### Includes
- [X] Code changes
- [X] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ba55cd347298`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.