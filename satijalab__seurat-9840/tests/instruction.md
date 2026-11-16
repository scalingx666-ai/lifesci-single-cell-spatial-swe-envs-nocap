# Issue

**Title:** Fix PseudobulkExpression to forward NormalizeData args

## Description

Big thanks to @mhkowalski for the fix

---
As reported in  we don't actually pass the `margin` or `scale.factor` arguments to `NormalizeData` in the single assay case. 

This is a minor fix. While I was there, I also added some test coverage for `AggregateExpression`, which ensures that 

1. We sum counts correctly
2. We return correctly return normalized data (with parameter options) in the single and multi-assay case.
3. We return an object with `group.by` variables correctly added to the meta.data
4. We pass arguments correctly to `CreateSeuratObject` using `...`. 
---

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `14c7424edc83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.