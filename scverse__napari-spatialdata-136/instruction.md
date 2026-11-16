# Issue

**Title:** Support multiple SpatialData objects

## Description

This PR allows for viewing multiple `SpatialData` objects with napari-spatialdata. This, by passing a list of `SpatialData` objects to `Interactive`. This list is converted to an `EventedList`. In order to properly support viewing elements even when `SpatialElement` names are shared between `SpatialData` objects a few changes have been made.

1. The' ElementWidget' checks whether there are duplicate elements which are stored in the list `element_names`, If `element_name` is in this `list` then a suffix `_{index}` is added to `element_name`. The entry of `element_name` in `_elements` is changed from a `str` corresponding to the element type, to a dictionary with key-values 
         -  `element_type` corresponding to the original value of `_elements, `
         - `sdata_index` corresponding to the index of the `SpatialData` object in the `EventedList`
         - `original_name` corresponding to the original name.
 This behavior also ensures that instead of napari creating an index for the copy which is not informative, a suffix will be pointing to the `SpatialData` object. This also means in case of more than 1 duplicate `SpatialElement` name, both layers belonging to the same `SpatialData` will have the same suffix. The way it is implemented can also handle duplicate `element_name` with different associated coordinate systems.
2. A new `_get_sdata` function is used to obtain the `SpatialData` object from the `EventedList` and to indicate whether multiple `SpatialElements` with the same name exist.
3. `SdataWidget` and `SpatialDataViewer` make use of the function at 2 to create the layers appropriately. In the viewer, the `name` argument now corresponds to the name with a potential suffix, and `name` in metadata is the name in the `SpatialData` object.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bfbe48442ddf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.