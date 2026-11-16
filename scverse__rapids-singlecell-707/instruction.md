# Issue

**Title:** Use cibuildwheel supported prebuilt CUDA images

## Description

Switch wheel builds to prebuilt `quay.io/manylinux_cuda` CUDA images, which cibuildwheel now documents as a way to build CUDA wheels on Linux ([docs](https://cibuildwheel.pypa.io/en/stable/faq/#building-wheels-with-cuda-on-linux)). The 12.2 and 13.0 images aren't listed there yet since they were only just published; the docs currently show 12.9 and 13.1.

This drops the in-repo per-version Dockerfiles and the remaining CUDA libraries rapids-singlecell links (cusolver, cusparse, nvJitLink) are installed via `CIBW_BEFORE_ALL`.

The images use the :latest tag but they can be pinned to a date tag (e.g. 2026.06.30-1) for reproducibility.

Validated locally by building cp312 wheels for both CUDA 12.2 and 13.0 on x86_64 and aarch64 against the published images with the full cibuildwheel pipeline.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6072e3636c9a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.