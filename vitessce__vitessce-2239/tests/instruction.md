# Issue

**Title:** fix the link controller overwriting the link id from config

## Description

Fix that the Link controller doesn't request a new ID when getting it from the Config

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->
Fixes #
<!-- For other PRs without open issue -->
#### Background
<!-- For all the PRs -->
#### Change List
- Link Controller adding a "else" that the ID is not overwritten when getting it from the config
- Using custom spacing for the example with Sanjays data in sanjay-2024
#### Checklist
 - [ ] Have tested PR with one or more demo configurations
 - [ ] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a548b3b0efd0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.