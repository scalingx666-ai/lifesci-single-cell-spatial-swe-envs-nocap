# Issue

**Title:** Rename RunBenchmark to RunSpatialBenchmark

## Description

<!-- CURSOR_AGENT_PR_BODY_BEGIN -->
## Summary

Rename spatial domain clustering benchmark APIs, remove the old names, and finish documentation cleanup.

- `RunBenchmark()` → **`RunSpatialBenchmark()`**
- `BenchmarkPlot()` → **`SpatialBenchmarkPlot()`**
- Old names are **removed** (not aliases).

scRNA integration evaluation: `RunIntegrationBenchmark()` / `IntegrationBenchmarkPlot()`.

## Documentation (item 1)

- Fixed 0.9.0 NEWS to reference `RunSpatialBenchmark()` / `SpatialBenchmarkPlot()`.
- Added pkgdown **Benchmark** reference section with all four APIs.
- Added articles:
  - `integration-benchmark-workflow`
  - `spatial-benchmark-workflow`

## Usage

```r
bench <- RunSpatialBenchmark(srt, gold_standard = "gold_domain")
SpatialBenchmarkPlot(data = bench)

srt <- RunIntegrationBenchmark(srt, batch = "tech", celltype = "celltype")
thisplot::print_colored_table(srt@tools$IntegrationBenchmark$summary, by = "row")
IntegrationBenchmarkPlot(srt)
```
<!-- CURSOR_AGENT_PR_BODY_END -->

<div><a href="https://cursor.com/agents/bc-01a00f3d-19cd-7d32-b63e-ce70fd657503?cursor_ref=pr_footer&cursor_cta=open_in_web"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-web-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-web-light.png"><img alt="Open in Web" width="114" height="28" src="https://cursor.com/assets/images/open-in-web-dark.png"></picture></a>&nbsp;<a href="https://cursor.com/background-agent?bcId=bc-01a00f3d-19cd-7d32-b63e-ce70fd657503&cursor_ref=pr_footer&cursor_cta=open_in_cursor"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-cursor-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-cursor-light.png"><img alt="Open in Cursor" width="131" height="28" src="https://cursor.com/assets/images/open-in-cursor-dark.png"></picture></a>&nbsp;</div>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ecb429c787d0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.