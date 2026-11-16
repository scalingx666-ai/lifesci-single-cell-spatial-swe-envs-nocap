# Issue

**Title:** Use FFTW3 implementation if available

## Description

##### Issue
.


##### Description of changes
Separate out FFT accelerated matrix multiplication functions and compile against FFTW if available.

Interestingly enough, FFTW actually isn't much faster than numpy's FFT module.

There may be some room for improvement still because apparently FFTW supports multithreaded FFT, unlike numpy. But so far, I've been unable to get that working. It would be nice to use openmp, since we're already using it when compiling cython's parallel module. See FFTW [docs](http://www.fftw.org/fftw3_doc/Multi_002dthreaded-FFTW.html#Multi_002dthreaded-FFTW). We would likely use conda's [FFTW package](https://anaconda.org/conda-forge/fftw) but that doesn't seem to be compiled with the `--enable-openmp` flags, so that may be an issue.

The main impact on performance is the presence/abscence of Intel's MKL library. Optimization runs ~2x slower without mkl, regardless of FFT library.

##### Includes
- [X] Code changes
- [ ] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4aae1a9f7772`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.