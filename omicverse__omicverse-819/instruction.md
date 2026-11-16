# Issue

**Title:** feat(pp,pl): unified QC compute / plot / filter workflow

## Description

.

## Problem (from the issue)

omicverse computes QC metrics and filters, but **skips the visualization step**: to choose thresholds users had to hand-roll histograms (`plt.hist` + `axvline`) per metric (see the reporter's notebook). The classic scRNA QC flow is *look, then cut* — and because sample quality differs, you want to see per-sample distributions before picking cutoffs.

## What this adds — the missing 3-step workflow

```python
# 1. compute metrics, NO filtering (the "stat" step)
ov.pp.qc_metrics(adata)

# 2. inspect distributions, per sample, with threshold guide lines (the "visualize" step)
ov.pl.qc(adata, batch_key='sample',
         tresh={'mito_perc': 0.13, 'nUMIs': 800, 'detected_genes': 500})

# 3. filter (existing)
ov.pp.qc(adata, tresh={'mito_perc': 0.13, 'nUMIs': 800, 'detected_genes': 500})
```

### `ov.pp.qc_metrics` (new)
Flags mt/ribo/hb genes, runs scanpy `calculate_qc_metrics`, and adds the omicverse aliases `nUMIs` / `detected_genes` / `mito_perc` — both naming conventions available, **nothing removed**. Auto-detects the MT prefix (`MT-`/`mt-`) like `ov.pp.qc`.

### `ov.pl.qc` (new)
Histograms (default) or violins of the standard QC metrics (UMIs, genes, mito%, ribo%, hb%, doublet score — auto-detected), with:
- `batch_key=` → one curve/violin per sample (the issue's key point: per-sample quality),
- `tresh=` (same dict as `ov.pp.qc`) → dashed guide lines so you see exactly where a cutoff lands,
- `kind='hist'|'violin'`, `log='auto'` (log-scales count metrics), layout/style controls.

Returns the matplotlib `Figure`.

## Example output

`ov.pl.qc(adata, tresh={'mito_perc':0.13,'nUMIs':800,'detected_genes':500})` → per-metric panels with the chosen cutoffs drawn in red (UMIs/genes on log-x):

(UMIs · genes · mito% · ribo% · hb%, each with its threshold line)

## Tests

`tests/pp/test_qc_workflow.py` — compute-without-filter, alias consistency (`nUMIs==total_counts`, `mito_perc==pct_counts_mt/100`), explicit prefix, plot (hist + per-sample violin), and the no-metrics `ValueError`. All pass.

## Notes

- Backward compatible: `ov.pp.qc` is unchanged.
- `ov.pl.qc` (plot) is distinct from `ov.pp.qc` (filter) — different namespaces.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `928df87e50ec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.