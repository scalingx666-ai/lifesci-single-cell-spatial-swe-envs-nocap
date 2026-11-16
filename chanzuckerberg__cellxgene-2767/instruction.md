# Issue

**Title:** fix: Fix opacity of centroid labels

## Description

## Summary

- Fix typo in prop name: `opactity` → `opacity` when passing the opacity value to the `Label` component (line 153)
- Fix extraneous brackets in style object: `opacity: { opacity }` → `opacity` shorthand property (line 208). The original code wraps `opacity` in object literal braces `{}` inside the style object, producing an object value instead of the numeric opacity value.

## Test plan

- [ ] Verify centroid labels render with correct opacity when categories are selected/deselected
- [ ] Verify deselected centroid labels appear semi-transparent rather than invisible

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5eb302175251`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.