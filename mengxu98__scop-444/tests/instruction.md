# Issue

**Title:** fix(db): keep nested MSigDB collections

## Description

## Summary
- Keep nested MSigDB collections instead of truncating them at the first colon, so names such as `MSigDB_M2_CGP` and `MSigDB_M2_CP` select those subsets.
- Parent names such as `MSigDB_M2` still include every nested collection, and colon forms such as `MSigDB_M2:CGP` are accepted.
- An unknown MSigDB name now reports the available collections instead of failing in `complete.cases()`. .

## Test plan
- [x] Unit tests cover prefix expansion, colon normalization, parent/sibling subsetting, the missing-name error, and colon aliases.
- [ ] `FeatureHeatmap(..., db = "MSigDB_M2_CGP", species = "Mus_musculus")` completes enrichment.
- [ ] `db = "MSigDB_M2:CP:BIOCARTA"` selects the same sets as `MSigDB_M2_CP_BIOCARTA`.
- [ ] An unknown name such as `MSigDB_M2_NOPE` reports the available MSigDB databases.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e8acc8984a88`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.