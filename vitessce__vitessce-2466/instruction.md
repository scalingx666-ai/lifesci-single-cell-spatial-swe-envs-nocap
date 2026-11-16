# Issue

**Title:** NickAkhmetov/Add compatibility for OME 0.5/Zarr v3 images and label-only spatialdata elements

## Description

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->
 
<!-- For other PRs without open issue -->
#### Background

This PR adds a compatibility layer that flattens OME metadata attributes to ensure compatibility with OME 0.5/Zarr v3.

The implementation was tested by checking an existing demo config and a xenium dataset which was previously failing to visualize.

The update also fixes an issue with loading cell labels which surfaced in the same dataset after resolving the image loading problem.

#### Change List
- Adds `ome-ngff-version` util and unit tests.
#### Checklist
 - [x] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable

<img width="1868" height="931" alt="image" src="https://github.com/user-attachments/assets/4495b07a-527d-4c38-bab4-6e91e4c7dea4" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e4e694df70e7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.