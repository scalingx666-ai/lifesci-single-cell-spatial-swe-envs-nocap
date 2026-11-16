# Issue

**Title:** feat(space/seg): pluggable cell segmentation backends + seam-free tiling (fixes bin2cell tile-overlap bug)

## Description

## Summary

Adds **`ov.space.seg`**, one API for the image- and transcript-based segmentation methods benchmarked in Martínez-de-Morentin et al., *Nature Methods* 2026 ("Benchmarking segmentation methods for spatial transcriptomics"). It also fixes a seam bug in the existing Visium HD tiled segmentation.

| function | what it does |
|---|---|
| `seg.methods()` | backend table: input type, deps, GPU, installed?, reference |
| `seg.segment(image, method=...)` | tiled, globally normalised instance segmentation → dense or sparse labels |
| `seg.segment_transcripts(tx, method="baysor")` | Baysor CLI wrapper, optional image-label prior |
| `seg.assign_transcripts` / `seg.aggregate` | molecules → cell ids → cells × genes AnnData with WKT outlines (pixel size, offset or 3×3 affine) |
| `seg.evaluate` / `seg.compare` | reference-free CellSPA metrics (yield, % assigned, tx/genes per cell, 8 morphology descriptors) and a min-max ranked table |
| `seg.load_image`, `seg.expand_labels`, `seg.segment_tiled` | helpers |

**Image backends:** `watershed` (Spateo-style, no extra deps), `cellpose` (v2, v3 with `restore_type="denoise_cyto3"` as in the paper, v4 `cpsam`), `stardist` (fluo / H&E), `sam` (ViT-H, 0.88 / 0.95 as in the paper), `sam2` (`facebook/sam2-hiera-large`), `micro_sam` (`vit_b_lm`), `cellsam`. Fluorescence and H&E inputs are both supported. For single-channel models on H&E, the haematoxylin channel is used.

## Bug fix: tile seams in `bin2cell.cellseg`

On master, overlapping tiles produce duplicate COO entries that `csr_matrix` **sums**, so cells on tile borders get label ids that are sums of two labels. On a synthetic 900-cell grid, 171 cells were corrupted. The new tiling engine runs each tile with a context margin and keeps each object only in the tile that owns its centroid; contested pixels keep the first writer. `bin2cell.cellseg` and `visium_10x_hd_cellpose_he/gex` now route through it, so the fix applies to them, and they gain `method="stardist"`. Regression test: `test_bin2cell_cellseg_has_no_seam_artifacts`.

## Other changes
- New extra `pip install 'omicverse[seg]'` (cellpose, segment-anything, sam2 on py≥3.10, huggingface_hub, shapely). StarDist, micro-SAM (conda-forge), CellSAM (git) and Baysor (Julia) stay opt-in; a missing dependency raises the usual `build_optional_dependency_error` with the install hint.
- SAM / SAM 2 skip Apple MPS when choosing a device automatically, because their mask generator needs float64.
- `visium_10x_hd_cellpose_*` docstrings and registry examples fixed: they modify `adata` in place and return `None`.
- `spatial-tutorials` skill: fixed the same `adata = ...cellpose_he(...)` mistake and documented `ov.space.seg`.

## Validation
- `tests/space/test_seg.py`: 17 tests, passing locally on py3.11. They use real skimage/scipy maths and fake model modules, so CI needs no weights or GPU.
- Real models on scikit-image sample images (CPU/MPS):

| run | cells |
|---|---|
| watershed, fluo nuclei | 253 |
| Cellpose 4 cpsam, fluo | 330 (tiled 256 px: 330) |
| StarDist fluo | 317; 256 px tiles match untiled 100% at IoU ≥ 0.5, both directions |
| Cellpose 3 cyto3 | 188; with `denoise_cyto3`: 223; nuclei: 325 |

- **Not yet validated with real weights:** SAM, SAM 2, micro-SAM, CellSAM, and a real Baysor binary. These need a CUDA box; I'll follow up once the GPU runner is available.

## Test plan
- [ ] CI green on py3.10 / 3.11 / 3.12
- [ ] SAM / SAM2 / micro-SAM on a CUDA GPU
- [ ] Baysor on a Xenium tile

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8df15aae1f3e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.