# Issue

**Title:** Strip meta.physicalSizes rather than invert

## Description

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->

This is a PR into the branch for #2551 . The effect should be the same, kind of a matter of style/preference. Here, the code strips the `meta.physicalSizes` metadata when we can assume the modelMatrix already accounts for the physical sizing, rather than un-applying the matrix operations before viv re-applys them


<!-- For other PRs without open issue -->
#### Background
<!-- For all the PRs -->
#### Change List
-
#### Checklist
 - [ ] Have tested PR with one or more demo configurations
 - [ ] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1f4b0e240ca9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.