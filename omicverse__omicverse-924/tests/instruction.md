# Issue

**Title:** feat(space): the arrangement layer — spatial statistics, niches, geometry and Stereo-seq

## Description

Closes the gap  points at, and the one a function-by-function comparison against squidpy 1.6.5 turned up.

`ov.space` could say **what is where** — domains, deconvolved cell types, spatially variable genes. It could not say **how the things are arranged relative to each other**, which is most of what a spatial figure actually shows. Nine of squidpy's thirteen `gr`/`tl` functions had no equivalent anywhere in omicverse.

## What is new

```
ov.space.nb     enrichment, co_occurrence, interaction_matrix, centrality,
                ripley, sepal, mask, sliding_window, var_by_distance
ov.space.niche  neighborhood, utag, cellcharter, molecular
ov.space.geom   align, align_pairwise, stack, interpolate
ov.io.spatial   read_stereoseq, bin_stereoseq
```

Existing flat names all still work; the namespaces are additions, not a rename.

## Measured, not asserted

The statistics follow squidpy's semantics deliberately: each has one correct definition, and matching a reference implementation is what makes the numbers checkable. On an identical graph over a real Visium slide:

| | agreement with squidpy 1.6.5 |
|---|---|
| `interaction_matrix` | exact |
| `nhood_enrichment` counts | exact |
| `nhood_enrichment` z | Pearson r = 0.9975 (independent permutation draws) |
| `centrality` | exact |
| `co_occurrence` | Pearson r = 1.0000 |
| `ripley` F / G / L | Pearson r = 1.0000 each |
| `sepal` | Spearman rho = 0.864 |
| `sliding_window` | ARI = 1.0000 |
| `var_by_distance` | max abs. difference 1.11e-16 |

Four needed a rewrite to get there, and each wrong version produced a plausible number that was not the statistic it claimed to be:

- **centrality** is a *group* centrality over the whole graph, not a property of each cluster's induced subgraph;
- **co_occurrence** takes its marginal from the pairs inside the radius, not from global cluster frequencies;
- **Ripley's G** measures inwards from spots *outside* the cluster, and **L** takes its intensity from all observations over the convex-hull area;
- **var_by_distance** drops the anchor's own zeros to NaN before min-max scaling.

## Issue #760, item by item

- **Molecular niche** — *already implemented*. `nmf_tissue_zones` has always been the NMF-over-cell2location-abundance method the myocardial-infarction and pulmonary-fibrosis atlases call a molecular niche. Nobody searching for niche analysis would find it under that name, so it is aliased as `niche.molecular` and documented. No new algorithm.
- **Spatial niche** — `niche.neighborhood` and `niche.utag` complete squidpy's `calculate_niche`, whose `cellcharter` arm omicverse already had.
- **Spatial ecotype** — not here. R-only upstream; delegated to a `py-spatialecotyper` port under the rebuildr protocol.
- **Stereo-seq** — `read_stereoseq` reads a GEM and bins it; `bin_stereoseq` re-aggregates in memory and refuses a size the existing bins do not nest into.
- **3-D reconstruction** — `ov.space.geom`.

## Geometry

`pySTAligner` and `CAST` align *expression* and return a shared embedding. An embedding cannot be sliced or measured in microns because it has no common coordinate frame, which is what a reconstruction needs. `geom.align` solves the fused Gromov-Wasserstein problem PASTE is built on, implemented over POT so the default path needs no extra install; `method='paste'` defers to the real package when present.

Both halves were wrong when first written and only measurement caught it. The Procrustes step returned the transpose of its rotation — 105 px of residual where the answer was 0, and a tidy-looking picture either way. And `align` carried each section forward by a mean offset, which transports translation but discards the rotation the anchor itself received, so everything past the second section drifted by 761 px on a 10,628 px tissue. Recovery of a known rotation is now exact to 1e-11 px across a four-section chain, from a terminal or a middle reference.

How far ICP can be pushed turned out not to be one number: it first fails at **60°** on a real Visium slide, **20°** on a uniform random cloud, and **10°** on a regular lattice — worst where the geometry looks most orderly, because six-fold symmetry makes nearest-point correspondences genuinely ambiguous. FGW was exact in all three at every angle to 170°, which is why it is the default. An earlier draft of that docstring quoted only the Visium number, which was the most favourable case.

## Two things found along the way

**`spatial_neighbors` gains `coord_type='grid'`.** Plain k-NN cannot know an array platform has a lattice, so a rim spot reaches across the gap to fill its quota and picks up neighbours it does not touch — degrees of 5–8 on the full 2,688-spot Visium slide where a hexagon allows 6. The cutoff is not delicate: neighbour distances there are bimodal, 138 px for the lattice and 238 px for the next ring with nothing between, so every multiplier from 1.2 to 1.72 gives the identical 14,646-edge graph, and every edge it keeps is one squidpy's grid graph also has. **Default stays `'generic'`** so existing results do not move.

**`_tools.py` gains an `__all__`.** Without it, `from ._tools import *` republished `numpy`, `os`, `matplotlib.pyplot`, `scanpy` and four matplotlib symbols as part of the spatial API — nine of `ov.space`'s sixty-four public names were other libraries' imports. Now sixty-three, all real.

## Tests

48 new tests, 90 across `tests/space`, including five direct comparisons against squidpy that skip when it is not installed. One pre-existing failure in `test_deconvolution_rctd.py` reproduces unchanged on `master` and is untouched.

Tutorials: omicverse-tutorials#TBD.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55e7501f0646`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.