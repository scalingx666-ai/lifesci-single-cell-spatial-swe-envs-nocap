# Issue

**Title:** Checked correct column name

## Description

## Bug fix

* The attribute `self.steady_u` is set if `"fit_steady_u"` is a column in `adata.var`. Previously, it was checked if `"fit_steady_s"` is a column. The same is true the other way around, i.e. the attribute `steady_s` is set if `"fit_steady_s"` is a column in `adata.var`.

## Relates issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d86753457da7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.