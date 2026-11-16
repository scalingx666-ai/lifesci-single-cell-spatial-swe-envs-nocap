# Issue

**Title:** feat: SCENICPlusPlot and shared SCENIC/SCENIC+ network views

## Description

<!-- CURSOR_AGENT_PR_BODY_BEGIN -->
## Summary

Single-commit replacement of #360. `SCENICPlusPlot()` is a thin wrapper around `SCENICPlot()`. Network, eGRN, and coverage views share one code path for SCENIC (`adjacency`) and SCENIC+ (`tf_gene` / `triplets`).

Dropped unused fallbacks: extra AUC/region-AUC slot names, column-name guessing, triplets-to-adjacency synthesis, `regulons` table parsing, unused igraph layouts, and unused helper wrappers.

```r
SCENICPlot(srt, group.by = "CellType", plot_type = "network_graph",
           features = example_tfs, max_targets = 12, label_nodes = "all")
SCENICPlusPlot(srt, group.by = "CellType", plot_type = "egrn",
               features = example_tfs, max_targets = 10)
```

## Preview

[eGRN with Chinese palette](https://cursor.com/agents/bc-01a00f3d-19cd-7d32-b63e-ce70fd657503/artifacts?path=%2Fopt%2Fcursor%2Fartifacts%2Fscenic-plots%2F42_egrn_chinese_palette.png)

[network_graph with Chinese palette](https://cursor.com/agents/bc-01a00f3d-19cd-7d32-b63e-ce70fd657503/artifacts?path=%2Fopt%2Fcursor%2Fartifacts%2Fscenic-plots%2F43_network_graph_chinese.png)

[Star panels with cell-type titles](https://cursor.com/agents/bc-01a00f3d-19cd-7d32-b63e-ce70fd657503/artifacts?path=%2Fopt%2Fcursor%2Fartifacts%2Fscenic-plots%2F44_star_panels_celltype.png)

## Test plan

- [x] `tests/testthat/test-scenic-plot.R` — 95 passed, 0 warnings.
- [ ] `R CMD check` / CI

<sub>To show artifacts inline, <a href="https://cursor.com/dashboard/cloud-agents#my-pull-requests">enable</a> in settings.</sub>
<!-- CURSOR_AGENT_PR_BODY_END -->

<div><a href="https://cursor.com/agents/bc-01a00f3d-19cd-7d32-b63e-ce70fd657503?cursor_ref=pr_footer&cursor_cta=open_in_web"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-web-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-web-light.png"><img alt="Open in Web" width="114" height="28" src="https://cursor.com/assets/images/open-in-web-dark.png"></picture></a>&nbsp;<a href="https://cursor.com/background-agent?bcId=bc-01a00f3d-19cd-7d32-b63e-ce70fd657503&cursor_ref=pr_footer&cursor_cta=open_in_cursor"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-cursor-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-cursor-light.png"><img alt="Open in Cursor" width="131" height="28" src="https://cursor.com/assets/images/open-in-cursor-dark.png"></picture></a>&nbsp;</div>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `38ef0c21b12a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.