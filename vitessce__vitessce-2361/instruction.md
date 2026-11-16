# Issue

**Title:** added debug option to see requested LOD (3) and loaded LOD (4)

## Description

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->
Fixes #  
Added debug info into the shader code in Spatial Accelerated View
#### Background
Change u_renderstyle in the shader to 3 or 4 for the respective debug view
#### Change List
- Added two additional rendersyles
#### Checklist
 - [x] Have tested PR with one or more demo configurations
 - [ ] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `16c7aea880b3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.