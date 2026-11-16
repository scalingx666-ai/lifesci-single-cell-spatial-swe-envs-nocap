# Issue

**Title:** Add Atera spatial data reader & loader (supersedes #10525)

## Description

From @stephenwilliams22 at #10525

> Adds support for 10x Genomics' Atera spatial assay output bundles, following the same `Read*`/`Load*` pattern as the existing Xenium/Vizgen/Nanostring readers:
>
> - `ReadAtera()` — reads an Atera output bundle's zarr-backed counts matrix, cell centroids, cell/nucleus segmentation polygons, transcript coordinates, morphology images, and run metadata. The counts matrix can be cached to disk via BPCells (auto-enabled when the package is installed), so large bundles don't need to be fully materialized in memory.
> - `LoadAtera()` — builds a Seurat object (with a FOV) from ReadAtera()'s output.
> - `LoadAteraMolecules()` — incrementally fetches transcript coordinates for additional genes into an already-loaded object, for interactive exploration without re-reading the full transcript table.
> - `LoadAteraSegmentations()` — builds segmentation polygons for only the cells present in a (possibly cropped) FOV, avoiding the cost of building polygons for every cell in whole-tissue bundles up front.
> - `LoadAteraCodewords()` — loads codeword/probe metadata for requested genes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8a54daf7d750`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.