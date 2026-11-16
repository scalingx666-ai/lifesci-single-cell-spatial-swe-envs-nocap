# Issue

**Title:** Tkakar/fix-issue-1893-and-1891

## Description

This PR adds error messages on the views when the image file is not pyramidal or when the offsets url is missing.
These messages are only shown when the debugMode is true.

To test - use this url for image in the following config: 
https://assets.hubmapconsortium.org/664b8227e17ee2a35a504dd8c19c2531/processedMicroscopy/VAN0012-RK-102-167-PAS_IMS_images/VAN0012-RK-102-167-PAS_IMS-registered.ome.tiff

http://localhost:3000/?dataset=rgb-ome-tiff&debugMode=True






<!-- For other PRs without open issue -->
#### Background
<!-- For all the PRs -->
#### Change List
-
#### Checklist
 - [ ] Have tested PR with one or more demo configurations
 - [ ] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `de0f20ae2365`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.