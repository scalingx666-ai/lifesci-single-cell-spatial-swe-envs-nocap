# Issue

**Title:** Move comparison subpackage within monorepo

## Description

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->
Fixes #
<!-- For other PRs without open issue -->
#### Background

Our changeset-publish script filters to things inside `packages/`  https://github.com/vitessce/vitessce/blob/ec88124a51cbd2d7eb931960f8c2dc5fa25efd34/scripts/changeset-publish.sh#L23
<!-- For all the PRs -->
#### Change List
-
#### Checklist
 - [ ] Have tested PR with one or more demo configurations
 - [ ] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ec88124a51cb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.