# Issue

**Title:** perf(single): 24% faster scTenifoldKnk perturb backend (KO/KD/OE bench)

## Description

## TL;DR

- This PR makes `ov.single.perturb(..., backend="sctenifoldknk")` faster in `omicverse/single/_perturb.py`.
- It builds the GRN graphs and the result tables in batches instead of one edge or one node at a time.
- Median wall time on one CPU core for two passes of the KO/KD/OE cases (160 genes): 84.0 ms -> 63.6 ms, 24% faster.
- `pytest tests/single/test_perturb.py tests/pl/test_ccc_plots.py tests/utils/test_ovagent_tool_runtime.py tests/pl/test_generic_plots.py` gives 442 passed, 51 skipped, the same as on `master`.

## What & Why

Before, the backend did much work in Python loops. `_tensor_to_graph` added each node and each edge with a separate `add_edge` call. `_delta_from_grn` ran one `in_edges(g)` query per gene. `_diff_grn` sorted all `(source, target)` tuples in one large sort. `_run_sctenifoldknk` also sliced `adata[:, shared]` and read the expression matrix a second time.

Now the code does the same work in fewer steps:

- `_tensor_to_graph` removes the diagonal with a numpy mask and calls `add_nodes_from` and `add_weighted_edges_from` once.
- `_delta_from_grn` sums the in-edge weights of each node from `graph.pred` and builds the table from columns.
- `_diff_grn` sorts the sources, then sorts the targets of each source. This gives the same row order as one sort of all pairs.
- `_apply_perturbation_to_graph` writes the new weight into the edge data dict that it already has.
- `_run_sctenifoldknk` converts the WT and KO tensors to arrays once. It reuses the expression matrix and selects the shared genes with `get_indexer`.

The output stays identical. The edge order, node order, row order and summation order do not change, so all float values keep the same bits. The table dtypes also stay the same.

## Results

Median wall time of one pass over the five KO/KD/OE cases of `perturb(..., backend="sctenifoldknk")`, on one CPU core:

| Situation | Before | After | Change |
|---|---|---|---|
| 8 genes, 50 cells (test fixture size) | 8.34 ms | 7.04 ms | 16% faster |
| 160 genes, 300 cells, 6% edges | 39.0 ms | 31.8 ms | 19% faster |
| 400 genes, 500 cells, 6% edges | 205.2 ms | 157.0 ms | 23% faster |
| 400 genes, 500 cells, 0.2% edges (very sparse) | 51.9 ms | 45.3 ms | 13% faster |

Very sparse networks gain the least, because there are few edges to process. No case is slower.

## Why this is safe and easy to maintain

The change touches only the private helpers of the scTenifoldKnk backend and uses plain numpy, pandas and networkx calls. Each helper keeps one code path. Graph nodes, edges, weights, DataFrame rows and dtypes are the same as before. The existing tests in `tests/single/test_perturb.py` cover the KO, KD and OE modes and the layer and gene-order variants.

## Validation

- Benchmark: 5 cases (KO, multi-gene KO, KD with a layer, OE without GRN output, KO with reversed gene order) on 160 genes and 300 cells, two passes per sample. Before 84.0 ms, after 63.6 ms, in three separate runs (ratios 0.763, 0.757, 0.751). Each run also checked that all outputs match the unmodified code exactly.
- Tests: `python -m pytest -q tests/single/test_perturb.py tests/pl/test_ccc_plots.py tests/utils/test_ovagent_tool_runtime.py tests/pl/test_generic_plots.py` gives 442 passed, 51 skipped (same as `master`).
- Reproduce: `python -m pytest -q tests/single/test_perturb.py -k sctenifoldknk --durations=5`

## AI assistance

This PR was prepared with AI assistance from Aiden. Candidates were tracked with Weco Observe.

Weco share link: https://dashboard.weco.ai/share/U-freSfxjDpfmiC-LQ5C75sc2vP91aW4

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d94cf1da2d71`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.