# Issue

**Title:** Improve linking new layers to sdata

## Description

This PR allows for the user that if a layer with `sdata` in the metadata is created and a new layer is created from the napari menu to link the new layer without having to select the layer with `sdata` in the metadata. In case multiple `sdata` objects are in the opened layers it will check to see if there is only one `sdata` in the metadata of the layers in `layers.selection`. If there is no `sdata` an error gets thrown. If exactly 1 `sdata` the layer will be linked. If more than 1 `sdata` an errow will be thrown.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5b600dc83d6d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.