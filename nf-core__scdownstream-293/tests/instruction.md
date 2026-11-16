# Issue

**Title:** Centralize pipeline nf-test analysis plans and enable LIANA

## Description

## Summary
- Rename `tests/analysis_plan_extension.csv` to `tests/analysis_plan.csv` and enable LIANA (`paga,liana,de`) for the shared `scvi/global/0.5` plan row
- Wire the shared plan into `tests/nextflow.config` so relevant pipeline nf-tests use it by default
- Add `tests/analysis_plan_sub.csv` and switch the subclustering test to `scvi` with a per-label plan so Leiden/Entropy still run
- Regenerate affected pipeline test snapshots

## Test plan
- [x] `nftu` on `tests/default.nf.test`, `tests/main_pipeline_build.nf.test`, `tests/main_pipeline_extend.nf.test`, `tests/main_pipeline_reference_mapping.nf.test`, `tests/main_pipeline_sub.nf.test`
- [x] CI nf-test pipeline checks pass

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b841d4ff1e87`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.