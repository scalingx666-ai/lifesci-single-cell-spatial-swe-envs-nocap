# Issue

**Title:** Tkakar/fix 2648 add detailed ng view

## Description

Adds two types of detail views for Neuroglancer.

1. Shows a hovered mesh from the primary view. Uses a prop `detailMode` to serve as detail view.
2. Shows a zoomed in view of the same primary view. Uses a prop `cameraZoomFactor` in the config, that can be provided via LayerController as well in the future.

<img width="1154" height="531" alt="Screenshot 2026-10-09 at 12 08 26 PM" src="https://github.com/user-attachments/assets/ad70a2b6-5897-4c0f-9a12-89ac0e0ed6c3" />
<img width="1084" height="585" alt="Screenshot 2026-10-09 at 12 11 06 PM" src="https://github.com/user-attachments/assets/f7ffe56b-5015-4968-bcee-0175f1657b31" />


 
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `35e174c138f1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.