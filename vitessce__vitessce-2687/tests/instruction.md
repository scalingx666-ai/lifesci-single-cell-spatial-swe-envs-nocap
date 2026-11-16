# Issue

**Title:** Tkakar/fix stuck kernel issue

## Description

The async computation worker was getting created on every cell call that was visualizing Neuroglancer view in the widget. This PR terminates the worker on every unmount.
Fixes
<!-- For other PRs without open issue -->
#### Background
<!-- For all the PRs -->
#### Change List
-
#### Checklist
 - [ ] Have tested PR with one or more demo configurations
 - [ ] Documentation added, updated, or not applicable
 - [ ] New subpackage(s) manually published to NPM and trusted publishing enabled, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `138e8c4ce436`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.