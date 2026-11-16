# Issue

**Title:** Create SpatialDataViewer

## Description

Currently napari-spatialdata doesn't have a viewer class on itself. This PR creates a `SpatialDataViewer` subclassing the napari `Viewer`. This allows us to have `Viewer` designated callbacks in our viewer class, preventing the widget classes from becoming too convoluted with functions that are `Viewer` specific. Most of the code related to adding spatial elements as layers has been moved to this new `SpatialDataViewer`. 

In addition when a user is adding a new layer there is no information regarding which `SpatialData` object it belongs to and neither about the coordinate systems. The new viewer class has a callback which allows for inheriting the metadata of the active layer. In napari at most one layer is active at the time, even when multiple are selected. Within the insert layer callback, the added layer is not yet the new active layer, which allows for inheriting metadata from the layer that is active just before adding a new layer.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `450ad8c0e620`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.