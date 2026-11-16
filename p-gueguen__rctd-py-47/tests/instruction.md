# Issue

**Title:** feat: scverse-style rctd.pp.reference / rctd.tl.deconvolve (layer, key_added)

## Description

Adds a scverse-style layer on top of `rctd.deconvolve` (0.4.2): functions in `rctd.pp` / `rctd.tl`, AnnData in, results written into the AnnData.

```python
import rctd

ref = rctd.pp.reference(ref_adata, cell_type_key="cell_type", layer="counts")
rctd.tl.deconvolve(spatial, ref, mode="doublet", layer="counts", key_added="dbl")
rctd.tl.deconvolve(spatial, ref, mode="full", layer="counts", key_added="full")
```

- `rctd.pp.reference(adata, cell_type_key, *, layer, cell_min, n_max_cells, min_UMI)` returns the existing `Reference`.
- `rctd.tl.deconvolve` **is** `rctd.deconvolve`. It also accepts the reference AnnData directly (`cell_type_key`).
- New keyword-only arguments after `copy`:
  - `layer=` reads the spatial counts from `adata.layers[layer]`;
  - `key_added=` sets the prefix of every key, default `"rctd"`.
- A re-run replaces only the keys of its own prefix.
- No `pl` and no change to the CLI.

## Parity with 0.4.2

Defaults write the same keys and values as 0.4.2, and positional calls from 0.4.2 still work.

Tested on Xenium liver (15,931 cells, 45 types) on an L40S at batch 10000, in doublet and full mode, against tag v0.4.2. Each slot was compared (obs, obsm, uns), and every output was identical:
- `rctd run`;
- `deconvolve` with a `Reference`;
- `tl.deconvolve` with the reference AnnData;
- `layer="counts"` on log-normalised `X`;
- `key_added`.

A positive control (doublet vs full) shows the comparison detects differences.

## Tests

- `tests/test_anndata.py`: +7 tests covering the AnnData reference, `pp.reference`, `layer` with a positive control, `key_added` coexistence and re-runs in another mode, the exact 0.4.2 key set, and errors.
- Full CPU suite: 210 passed.
- ruff passes.
- `sphinx-build -W -n` passes.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `233582bd9f91`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.