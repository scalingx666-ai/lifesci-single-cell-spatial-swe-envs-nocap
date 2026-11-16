# Issue

**Title:** NickAkhmetov/Fix #2276 - Guard against WebGL context loss while loading volume data

## Description

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->

<!-- For other PRs without open issue -->
#### Background
I tested this out locally with `s-a-lsp1` and `s-a-kingsnake`. 

#### Change List
- Added graceful handling for WebGL context loss during volume data loading
#### Checklist
 - [x] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `902fc5f5902d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.