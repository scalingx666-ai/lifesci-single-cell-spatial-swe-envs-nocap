# Issue

**Title:** NickAkhmetov/Add slider controls to numeric legends

## Description

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->

<!-- For other PRs without open issue -->
#### Background
This PR adds slider controls to the `legend` package and updates the legend package to use TypeScript.

The min/max values on numeric legends now allow users to click and drag/use keyboard controls to set the min/max values for the legend.

#### Change List
- Add legend controls for slider.
- Convert `legend` package to native TS.

#### Checklist
 - [x] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable



https://github.com/user-attachments/assets/b107af85-5e25-46d4-9fbd-22578e3be88e

https://github.com/user-attachments/assets/4fe13d2d-2716-40d6-bbc9-1a3a04a2008c

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a1e4ffddb5b7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.