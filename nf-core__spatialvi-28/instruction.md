# Issue

**Title:** Use new multi-platform Docker image

## Description

This PR contains a new multi-platform Docker image that works on both AMD64 and ARM64. It is a multi-stage image originating from `jdutant/quarto-minimal` (a minimal ubuntu-based installation of Quarto without pandoc, so only works for HTML reports) and `condaforge/mambaforge` (with Conda and Mamba installed). The image is also optimised in terms of size - compare the old size of 3.37 GB versus the new 1.33 GB.

The image is used for all three Quarto reports, _i.e._ modules `ST_QC_AND_NORMALISATION`, `ST_CLUSTERING` and `ST_SPATIAL_DE`, even though the first two requires a less complicated environment; they do not require `SpatialDE` and `leidenalg` used by the last one. The difference in image size is just 10 MB, though, so I thought it better that all three modules use the same image, so that the user would get just one 1.33 GB image instead of 1.32 + 1.33 GB, even if that could be argue to be more conceptually beautiful.

One problem that remains is that we can't really use a `conda` directive for the report modules, given that they need Quarto. We'll have to think about it.

I also looked into using mulled containers for this (https://github.com/BioContainers/multi-package-containers), but they do not seem to build multi-platform images as far as I can tell. If they change that in the future (or if I've missed something) we should be able to use `jdutant/quarto-minimal` (or an equivalent) as a base and build a mulled container from that, removing the need to keep a `Dockerfile` and an `environment.yml` in the repo. This would, however, not work for `SpatialDE`, as it is not installable directly using Conda (we have to use `pip` from within Conda); mulled containers only work for packages part of Bioconda.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dc5afd9790d3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.