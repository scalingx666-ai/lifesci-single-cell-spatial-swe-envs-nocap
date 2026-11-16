# Issue

**Title:** NickAkhmetov/Display loading indicator for Neuroglancer view while meshes are loading

## Description

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->

<!-- For other PRs without open issue -->
#### Background
<!-- For all the PRs -->
#### Change List
- Display circular loading indicator while neuroglancer data is being loaded.
#### Checklist
 - [x] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable

Note: I'm having trouble testing this functionality/developing it further; Neuroglancer is (somehow) causing my computer to kernel panic in both Firefox and Chromium. I got the circular loader to show up until the point where the x/y/z axis indicators.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e4e694df70e7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.