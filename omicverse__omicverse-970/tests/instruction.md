# Issue

**Title:** fix(space): align Visium coordinates, libraries and image transforms

## Description

## Summary

Preserve barcode identity when reading legacy Visium position files, and read named row/column fields consistently as x=image column, y=image row. Keep selected-library observations and all image resolutions with known scale factors aligned during cropping and rotation.

Make library selection explicit for multi-library data, preserve legacy crop and manual-offset defaults, and support explicit XY cropping and coordinate-unit translation. Use existing NumPy and Pillow dependencies for the phase-correlation path, and convert detected offsets using the actual rendered axes size rather than PNG dimensions that include padding.

The change is limited to the Visium reader, spatial coordinate tools and their two regression test files. Unrelated API exports, segmentation return values, bin2cell changes and the standalone migration document have been removed.

## Compatibility

Standard modern Visium coordinates remain unchanged; the old field renaming could cancel its axis swap. Cropping and rotation return copies. Images without a known scale mapping are removed only from the output copy, with serializable removal metadata. Auto mapping remains an experimental image-correlation heuristic. Cropping with scale other than 1 remains unsupported.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41531a627523`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.