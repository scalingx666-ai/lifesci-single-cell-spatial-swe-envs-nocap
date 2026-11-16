# Issue

**Title:** Fix final rowgroup issue

## Description

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->
Related to #2637 , but a different issue: there was an off-by-one error affecting the final tile in the bottom-right-most corner. During the binary searching, the row group with index `numRowGroups` was being requested, but the final row group has inded `numRowGroups - 1`.
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7f4f10329d5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.