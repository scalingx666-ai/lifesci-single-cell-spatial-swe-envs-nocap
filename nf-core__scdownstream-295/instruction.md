# Issue

**Title:** Add fast scib-metrics benchmarking options for large datasets

## Description

## Summary
- Add pipeline parameters for optional stratified subsampling (`scib_max_cells`, `scib_subsample_strategy`, `scib_subsample_seed`) and metric profiles (`scib_metric_profile`: `fast`/`full`).
- Pass scib tuning options as explicit process inputs to `SCIBMETRICS_BENCHMARK` (not via `modules.config` ext fields).
- Implement subsampling, fast metric selection, and parallel neighbor search (`n_jobs=task.cpus`) in `SCIBMETRICS_BENCHMARK`.
- Publish `{method}_benchmark_info.json` and document subsampling/profile settings in MultiQC table descriptions.

## Defaults
- `scib_metric_profile=fast` for routine pipeline runs (disables isolated labels, k-means NMI/ARI, and PCR comparison; skips count-matrix rebuild).
- No subsampling unless `--scib_max_cells` is set (recommended ~50k–100k for very large objects).
- Use `--scib_metric_profile full` for publication-style benchmarking comparable to default scib-metrics.

## Test plan
- [ ] Run module test: `nf-test test modules/local/scibmetrics/benchmark/tests/main.nf.test`
- [ ] Run pipeline with `-profile test --scib true` and verify `combine/integrate/scib_metrics/*_benchmark_info.json` and MultiQC scib-metrics table
- [ ] On a large integrated object, compare runtime and method ranking between `--scib_metric_profile fast` and `full`, with and without `--scib_max_cells 100000`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e63ea286a745`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.