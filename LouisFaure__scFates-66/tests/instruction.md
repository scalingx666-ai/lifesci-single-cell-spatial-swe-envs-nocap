# Issue

**Title:** Fix tl.root tips_only with negative values; update GPU install docs

## Description

Part of the docs follow-up for #52.

### `tl.root` with `tips_only=True` could select a node that isn't a tip
To exclude non-tip nodes, `tl.root` set their score to `0` and took the maximum. With negative values, such as Palantir's log2 expression, `0` beats every tip, so a non-tip node (node 0) was selected. Found while switching the bone marrow tutorial to `scf.tl.root(adata, "CD34", tips_only=True)`: on that tree, all four tip averages are negative, so it returned node 0 instead of tip 163.

Non-tip nodes are now set to NaN, and the root is picked with `idxmax`/`idxmin`, which skip NaN. That also handles nodes with no cells.

I added a regression test: negated pseudotime (negative everywhere) with `tips_only=True` must select the current root tip. It fails on master (selects node 0 instead of 43) and passes with this fix.

### GPU install instructions (`installation.rst`)
The previous recipe used cuML 21.12, Python 3.8, CUDA 11.0 and elpigraph installed from git. It's replaced by a single pip command for CUDA 12, plus a link to the rapids-singlecell install guide:

```
pip install --extra-index-url=https://pypi.nvidia.com scFates "rapids-singlecell-cu12[rapids]"
```

The `rapids` extra of rapids-singlecell installs CuPy, cuDF, cuML, cuGraph and cuVS at matching versions. rapids-singlecell itself is needed by the GPU path of `tl.cluster` (#67). `tl.curve` and `tl.circle` are added to the list of GPU-capable functions.

**Tested on an NVIDIA RTX 5070 (CUDA 12, WSL):** the command above, run with pip in a fresh Python 3.12 environment, installs RAPIDS 26.10 and CuPy 14.2. Every listed function runs with `device="gpu"` and matches its `device="cpu"` result:

| Function | GPU vs CPU |
|---|---|
| `pp.filter_cells` | same outliers |
| `pp.batch_correct` | max difference 1e-5 |
| `pp.diffusion` | same leading components (\|r\| ≥ 0.998) |
| `tl.tree` (ppt) | principal points within 2e-10 |
| `tl.tree` (epg), `tl.curve`, `tl.circle` | identical |
| `tl.cluster` | identical clusters (ARI = 1) |

`tl.cluster` on GPU, and `pp.batch_correct` on CPU (as the reference), only work with the fixes in #67, so #67 should be merged together with this PR.

### Tutorials
The tutorial notebooks live in `LouisFaure/scFates_notebooks`, so their changes are in a separate PR there. The bone marrow tutorial's new automatic root call depends on this `tl.root` fix, so that PR should merge after a release that includes it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `42fe1151361d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.