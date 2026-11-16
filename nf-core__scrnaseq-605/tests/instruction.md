# Issue

**Title:** Fix cellrangermulti nf-test discovery

## Description

## Summary

Move the cellrangermulti `PIPELINE_INITIALISATION` nf-test suite into `subworkflows/local/utils_nfcore_scrnaseq_pipeline/tests/main.nf.test`, alongside the subworkflow it tests. Move the V(D)J pipeline test into `tests/main_pipeline_cellrangermulti.nf.test` and remove its standalone file. Separating the top-level test blocks ensures nf-test discovers the full pipeline suite.



## Tests

- nf-test dry-run discovered all 16 cases (5 pipeline tests and 11 initialization tests).
- All 11 initialization tests passed with `docker,test` before the final test-file relocation.
- Full pipeline tests were not run.

## PR checklist

- [x] This comment contains a description of changes (with reason).
- [x] Tests cover the reported test-discovery issue.
- [ ] Full nf-core lint and full pipeline tests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a45ac11ba806`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.