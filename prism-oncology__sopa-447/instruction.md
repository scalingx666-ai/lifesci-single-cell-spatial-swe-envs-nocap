# Issue

**Title:** feat: add InstanSeg segmentation method

## Description

Adds [InstanSeg](https://github.com/instanseg/instanseg) as a staining-based segmentation method, alongside Cellpose and StarDist.

## What's included

- `sopa.segmentation.instanseg` / `instanseg_patch`, built on the existing `custom_staining_based` machinery so it shares patching, CLAHE/gaussian preprocessing, conflict resolution and caching with the other staining methods. `instanseg_patch` returns a callable mapping a `(C, Y, X)` patch to a `(Y, X)` label mask.
- `load_instanseg_model`, following the `load_cellpose_model` / `load_stardist_model` convention introduced in #445.
- CLI: `sopa segmentation instanseg`, `sopa resolve instanseg`, and `sopa download instanseg`.
- Snakemake: `rules/instanseg.smk`, registration in `STAINING_BASED_METHODS`, and `config/toy/instanseg.yaml`.
- New optional extra: `pip install 'sopa[instanseg]'`.

`sopa download instanseg` delegates to InstanSeg's own `download_model`, which resolves URLs from the model index bundled in the installed package — no download URLs are hardcoded in sopa. `--model-dir` sets `INSTANSEG_BIOIMAGEIO_PATH`, mirroring how the cellpose and stardist commands set their respective env vars.

## Two things worth reviewing

**1. `pixel_size` is effectively mandatory.** InstanSeg models are trained at a fixed resolution (0.5 µm/px for `fluorescence_nuclei_and_cells`). When the objects are far from that scale the model returns *no cell at all* rather than degrading gracefully. Measured on the toy dataset (144 cells, nuclei ~38px wide):

| `pixel_size` | nuclei at model scale | cells found |
|---|---|---|
| unset | 38 px | **0** |
| 0.15 | 11 px | 133 |
| 0.2 | 15 px | 132 |
| 0.25 | 19 px | 131 |
| 0.3 | 23 px | 126 |
| 0.4 | 30 px | **0** |

It is a cliff, not a gradient. This is documented in the docstring, the admonition and the CLI help, and is why the toy config sets `pixel_size: 0.25` with an explanatory comment.

**2. The extra changes the resolved torch version.** Adding `instanseg-torch` moves uv's resolution from torch 2.13.0 (CUDA 13) to **torch 2.10.0 (CUDA 12)**. Verified by locking with and without the extra against the same base: without it the lock reproduces 2.13.0/cu13 exactly. `instanseg-torch` itself only declares `torch>=2.0.0`, so this comes out of the wider resolution rather than an explicit cap. Since the lock records one version per package, this also affects the `wsi` extra, which depends on torch. Happy to pin or restructure if you would rather not move the CUDA stack.

## Verification

- `pytest -m 'not long and not wsi'` — 58 passed, 7 deselected.
- `ruff check` and `ruff format --check` clean.
- Snakemake dry-run of `config/toy/instanseg.yaml` resolves the full DAG.
- End-to-end on the toy dataset: 123 boundaries produced, patch conflicts resolved, aggregation clean.
- Wrapper checked against real fluorescence microscopy (skimage `cells3d`): 29–48 cells, correct mask shape and dtype.
- Verified the `(1, 1, H, W)` output contract across 1-, 2- and 4-channel input and all axis orderings.

No unit test is added, consistent with the existing stardist integration, which also has none — the method requires downloading model weights at runtime.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2911ad87aa94`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.