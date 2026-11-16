# Issue

**Title:** test: cover untested pp/tl paths, fixing categorical covariates in `pp.combat`

## Description

.
Adds four parametrized tests for essential paths that had no coverage: `tl.score_genes_cell_cycle`, categorical covariates in `pp.combat`, `tl.rank_genes_groups` after `log1p` with a non-natural base, and `tl.embedding_density` with `groupby`.
This is supposed to increase test coverage for major functions and not just random edge cases.

The combat test showed that categorical covariates made the design matrix singular and silently corrupted the output, so this also switches them to reference coding.
I've also asked an agent to compare the current & new implementations against the R version. We're good now with these changes.

Human reviewed by me. Co-created with Fable 5.1 & Opus 5.5 on very high effort.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ad567d9f7ca`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.