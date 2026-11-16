# Issue

**Title:** Layer cs visibility

## Description

This PR is the replacement for #96. In its current state it has the following behavior when having multiple coordinate spaces:

Layer.metadata has a field to keep track of the visibility state in a coordinate system.

When starting napari
1. When a layer is present in the selected coordinate system and is made visible `active_in_cs` metadata is a set containing only the name of the coordinate system.
   If made invisible afterwards, the selected coordinate system is removed from the set.
2. If present and visible, but then changing to a different coordinate system in which the spatialdata element is not present, `layer.visible` is set to `False`, but `active_in_cs` still contains the name of the coordinate system in which it was made visibe. If present but not visible and then changing, nothing changes. 
3. When going back to the original coordinate system, the `active_in_cs` metadata of the layers visualizing the elements in that coordinate system are checked to whether a layer should become visible again or not.

Even when an element is not present in the selected coordinate system, it can still be made visible again by clicking on the eye. This would allow for now for the landmark registration approach. However, the name of the coordinate system is not added to `active_in_cs` in this case.

Note that changing the visibility does cause the scene to have to be redrawn upon visualizing again, which can take time (image is loaded again).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e2df7ecc597`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.