# Issue

**Title:** Fix reading tiffs

## Description

### Types of changes
<!--- What types of changes are introduced? Put an `x` in all applicable boxes: -->
- [x] Bug fix (non-breaking change which fixes an issue)
- [ ] Breaking change (change that would cause existing functionality to not work as before)
- [ ] New feature (non-breaking change which adds functionality)

### Description
<!--- What does this PR achieve? -->
Fix loading `TIFFs`: problem was that `tifffile.imread` returned `(y, x, z)`, whereas we expected `(z, y, x)` + reshape from
the former into latter caused the artifacts in #389 .
Also fixes passing explicit dimnames to 3D arrays when loading from files.
TODO: fix linting

In the future, switch to e.g. `dask_image.read` for either TIFFs only or for all image types once `pims` (backend for their IO) allows lazy loading if JPEGs.
Also, consider (in the future) refactoring our IO to some `Dimension` class (will be very useful/almost necessary) when adding new dimension to `ImageContainer`.

### How has this been tested?
<!--- Describe how you've tested your changes: -->
TODO: 2 tests 
1. one that tests setting `dims` explicitly for 3D image on disk
2. one that tries to load a `.tifffile` similar to the one in #389 

### Closes
<!--- If applicable, add `closes #XXXX` below to auto-close the issue related to this PR: -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d66375a1b126`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.