# Issue

**Title:** Fix test_covariate when restricting to a segment (seg=)

## Description

`scf.tl.test_covariate(adata, group_key, seg=...)` always failed with `ValueError: array length N does not match index length M`. When `seg` was given, the expression values covered only that segment's cells, but pseudotime and groups still covered every cell.

### Changes
- Pseudotime and groups now cover the same cells as the expression values.
- Group categories with no cells in the segment are dropped, so they don't produce NaN means.
- If fewer than two groups are present, a clear `ValueError` is raised.
- Added a `seg=` call to `test_w_plots.py`.

Found while answering #59, which asks about comparing two conditions on a branching trajectory. Testing per segment, or per lineage after `tl.subset_tree`, is the way to do this on a tree.

### Testing
`pixi run test` passes. I also checked by hand: per-segment, plus per-lineage after `subset_tree` with both the amplitude and the trend test.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `973b612923a4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.