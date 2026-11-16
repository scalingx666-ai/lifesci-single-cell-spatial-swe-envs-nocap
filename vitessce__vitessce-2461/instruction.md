# Issue

**Title:** Tkakar/ng opacity fix 2460

## Description

This PR enables the following
1.  Opacity change in Neuroglancer segmentation and annotation layers using their respective opacity sliders in layerController.
2. Points in the annotationLayer does not have a border now to have a clear view of the meshes
3. showAxisLines can be passed as prop to NeuroglancerView
4.  now accepts subsources which allow specifying bounds = false/true for the segmentation layer


 

<img width="421" height="595" alt="Screenshot 2026-04-17 at 2 14 21 PM" src="https://github.com/user-attachments/assets/30a3e7e8-e5ab-4993-b5ff-d45f3891bd44" />

Bounds are the yellow box and axisLines are the xyz lines

<!-- For other PRs without open issue -->
#### Background
<!-- For all the PRs -->
#### Change List
-
#### Checklist
 - [ ] Have tested PR with one or more demo configurations
 - [ ] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `61a79985f28c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.