# Issue

**Title:** Saving / exporting new elements back to SpatialData

## Description

This PR allows for saving / exporting back new layers to the SpatialData zarr store. Furthermore, it adds preparation code for being able to make changes in those layers visualizing existing elements in a SpatialData object and storing those back. 
A requirement for saving new layers / elements is to first link it to an existing SpatialData object by `shift+click` on the new layer and a layer with the already existing SpatialData object and pressing `shift+L`. Afterwards select the layer to be saved and press `shift+S`.

The PR is dependent on  for partially updating SpatialData objects in memory. A follow up PR of this one will allow for writing partial updates back to disk.

*EDIT from Luca: users can use [this other (legacy) branch](https://github.com/scverse/napari-spatialdata/tree/spatialdata) to have the functionality enabled before the current PR is merged.
The current PR gives a more stable implementation, has more tests and deals with the case of multiple `SpatialData` objects in a transparent way, letting the user choose where to save the annotations*

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `748c7633a50e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.