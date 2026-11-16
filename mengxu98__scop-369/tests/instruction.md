# Issue

**Title:** Add RunIntegrationBenchmark and IntegrationBenchmarkPlot

## Description

<!-- CURSOR_AGENT_PR_BODY_BEGIN -->
## Summary

`RunIntegrationBenchmark()` now returns a **Seurat** object. Tables live in `srt@tools$IntegrationBenchmark` and examples print them with `thisplot::print_colored_table()`.

`IntegrationBenchmarkPlot()` takes that Seurat object. LISI comparison is a **box** plot (per-cell distributions), not bars. `LISIPlot()` is removed; use `IntegrationBenchmarkPlot(plot_type = "box")`.

`RunBenchmark()` / `BenchmarkPlot()` are unchanged. They evaluate **spatial domain clustering** (BayesSpace / BANKSY / SmoothClust vs a gold standard), not scRNA batch integration.

## Usage

```r
srt <- RunIntegrationBenchmark(
  srt, batch = "tech", celltype = "celltype",
  methods = c("Uncorrected", "Harmony")
)
thisplot::print_colored_table(
  srt@tools$IntegrationBenchmark$summary,
  by = "row", palette = "Chinese"
)
thisplot::print_colored_table(
  srt@tools$IntegrationBenchmark$metrics,
  by = "col", palette = "Paired"
)
IntegrationBenchmarkPlot(srt)                 # box, heatmap, scatter, umap
IntegrationBenchmarkPlot(srt, plot_type = "box")
```

## Demo (`panc8_sub`, 1600 cells)

Harmony vs Uncorrected:

| method | overall | bio | batch | iLISI | cLISI | ARI | NMI |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Uncorrected | 0.662 | 0.764 | 0.510 | 0.065 | 0.994 | 0.488 | 0.679 |
| Harmony | 0.747 | 0.848 | 0.595 | 0.312 | 0.986 | 0.828 | 0.815 |

[LISI boxplots](https://cursor.com/agents/bc-01a00f3d-19cd-7d32-b63e-ce70fd657503/artifacts?path=%2Fopt%2Fcursor%2Fartifacts%2Fintegration-benchmark%2Fbox.png)
[Scaled metric heatmap](https://cursor.com/agents/bc-01a00f3d-19cd-7d32-b63e-ce70fd657503/artifacts?path=%2Fopt%2Fcursor%2Fartifacts%2Fintegration-benchmark%2Fheatmap.png)
[Bio vs batch scatter](https://cursor.com/agents/bc-01a00f3d-19cd-7d32-b63e-ce70fd657503/artifacts?path=%2Fopt%2Fcursor%2Fartifacts%2Fintegration-benchmark%2Fscatter.png)
[UMAP batch and cell type](https://cursor.com/agents/bc-01a00f3d-19cd-7d32-b63e-ce70fd657503/artifacts?path=%2Fopt%2Fcursor%2Fartifacts%2Fintegration-benchmark%2Fumap.png)

## Tests

`test-integration-benchmark.R` 28 passed; `test-lisi-controls.R` 8 passed.

<sub>To show artifacts inline, <a href="https://cursor.com/dashboard/cloud-agents#my-pull-requests">enable</a> in settings.</sub>
<!-- CURSOR_AGENT_PR_BODY_END -->

<div><a href="https://cursor.com/agents/bc-01a00f3d-19cd-7d32-b63e-ce70fd657503?cursor_ref=pr_footer&cursor_cta=open_in_web"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-web-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-web-light.png"><img alt="Open in Web" width="114" height="28" src="https://cursor.com/assets/images/open-in-web-dark.png"></picture></a>&nbsp;<a href="https://cursor.com/background-agent?bcId=bc-01a00f3d-19cd-7d32-b63e-ce70fd657503&cursor_ref=pr_footer&cursor_cta=open_in_cursor"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-cursor-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-cursor-light.png"><img alt="Open in Cursor" width="131" height="28" src="https://cursor.com/assets/images/open-in-cursor-dark.png"></picture></a>&nbsp;</div>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3940238868d0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.