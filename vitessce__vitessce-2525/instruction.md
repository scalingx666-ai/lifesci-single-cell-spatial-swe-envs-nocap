# Issue

**Title:** NickAkhmetov/Fix build errors related to optional @react-three/xr dependency by using dynamic imports

## Description

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->
Fixes #
<!-- For other PRs without open issue -->

I ran into an issue building the portal UI due to the optional XR dependency not being actually optional in the code - this PR fixes this by lazy-loading all XR module code.

<!-- For all the PRs -->
#### Change List
-
#### Checklist
 - [x] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bdf5c9c4b2ab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.