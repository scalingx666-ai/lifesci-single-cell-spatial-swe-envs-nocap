# Issue

**Title:** NickAkhmetov/Fix double-applied physical pixel size in spatialBeta 3D, restore camera-axis control

## Description

<!-- Replace with the number of the issue filed from UPSTREAM-ISSUE-3d-physical-size.md -->


#### Background

3D volume rendering in `spatialBeta` applies physical pixel size twice, so anisotropic volumes
render stretched along their coarsest axis by the anisotropy ratio. A volume with `1 x 1 x 2 µm`
voxels renders twice as deep as it should. The legacy `spatial` view renders the same file
correctly, so this shows up as a regression for anyone migrating a volumetric dataset to the beta
views.

`ImageWrapper.getModelMatrix()` scales an image into absolute micrometers, and
`Spatial.createImageLayer()` passes that to viv's `VolumeLayer` as `modelMatrix`. But `VolumeLayer`
independently derives its own physical size scaling matrix from the same metadata, and the
`XR3DLayer` vertex shader applies both:

```glsl
gl_Position = proj * view * model * scale * resolution * vec4(positions, 1.);
```

The legacy view avoided this because its `modelMatrix` comes from `loader.metadata.transform`, which
`getMetaWithTransformMatrices` leaves as the identity for a single image, so viv's internal matrix
was the only physical scaling applied. 2D is unaffected — `MultiscaleImageLayer` and `ImageLayer`
default `usePhysicalSizeScaling` to false, so there the model matrix is the only scaling.

Alongside that, the beta stack lost the 3D camera controls the legacy stack had, which compounds the
problem: once a volume is distorted or panned away there is no way back to a known orientation.

- `spatialBeta` reads `spatialAxisFixed` but nothing in the beta stack can set it. The legacy control
  lived in the spatial view's plot options menu (`SpatialOptions`), and `spatialBeta`'s `TitleInfo`
  is never given an `options` prop. `AbstractSpatialOrScatterplot` only pins the orbit target while
  that flag is set, so the target moves on every pan.
- The auto-computed initial view state is applied only when
  `notYetInitialized || stillDefaultInitialized`, and deliberately does not re-run on pan or zoom.
  Switching to 3D after panning in 2D therefore keeps the 2D target and zoom, even though
  `getInitialSpatialTargets` has already recomputed 3D values. The legacy layer controller reset the
  camera explicitly on every 2D/3D transition.

#### Change List

- Added `getVolumeModelMatrix()` in `@vitessce/spatial-beta`, which divides viv's physical size
  scaling matrix back out of the image's model matrix so that `model * scale` still equals the
  physical model matrix. Cancelling viv's matrix rather than passing the identity keeps 3D consistent
  with `ImageWrapper.getBoundingCube()`, which drives the clipping-plane slider ranges in absolute
  micrometers; passing the identity would shrink the render by the minimum physical size and
  desynchronise those sliders.
- Used it in `Spatial.createImageLayer()` when `spatialRenderingMode === '3D'`, and in
  `getInitialSpatialTargets()`, which passes a model matrix to `viv.getDefaultInitialViewState()` —
  that composes the two matrices the same way the render path does, so it needs the same corrected
  matrix or the initial camera does not frame the volume that is drawn. The 2D path is unchanged.
- Added a `SpatialOptions` plot options menu to `spatialBeta` carrying the "Fix Camera Axis" control,
  reusing the legacy control's label and aria-label. It lives in the spatial view rather than the
  layer controller because `spatialAxisFixed` is in `AUTO_INDEPENDENT_COORDINATION_TYPES`: under
  `initStrategy: 'auto'` each view gets its own scope for it, so a control in the layer controller
  writes to a scope the spatial view never reads. No coordination-type changes were needed.
- Re-initialize the camera in `SpatialSubscriber` when `spatialRenderingMode` changes, resetting
  target, zoom and rotation. Guarded on the initial targets being computable, so a dataset that is
  not ready yet does not reset the target to `null` — it re-runs once the data loads.
- Forward `orbitAxis` through the beta view's `setViewState`. DeckGL never emits it (`orbitAxis` is an
  `OrbitView` prop rather than part of its viewState), so nothing was being lost in practice, but it
  left `spatialOrbitAxis` unwritable through the view's only camera bridge despite being a declared
  coordination type for the view.
- Added an `anisotropic-volume` example config over a public HuBMAP 3DIMC dataset
  (`452 x 514 x 50` at `1 x 1 x 2 µm`) as a regression case. It deliberately does not set
  `three: true`, so it exercises the deck.gl/viv `VolumeLayer` path.
- Added unit tests for `getVolumeModelMatrix` (including a regression test pinning the old doubled
  extent) and for the `SpatialOptions` control.

#### Checklist

 - [x] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable

Testing notes: verified with the new `anisotropic-volume` demo config, and against the real file
through the loader — `ImageWrapper.getModelMatrix()` and viv's internal matrix both report a scale of
`[1, 1, 2]`, and the composed `model * scale` extent goes from `452 x 514 x 200` to
`452 x 514 x 100`, now matching `getBoundingCube()`. Compared side by side against the same file
under `spatial` + `layerController`, and confirmed 2D is unchanged. For the camera: panning in 2D and
then switching to 3D previously left the volume clipped at the edge of the view and now re-centers;
and with "Fix Camera Axis" on, a ctrl-drag pan in 3D no longer moves the orbit target, where it does
with the control off.

Documentation: no manual docs change needed. The coordination type page is autogenerated from
`COMPONENT_COORDINATION_TYPES` (`sites/docs/src/pages/_AutogeneratedCoordinationTypes.js`), and this
PR does not add or re-associate any coordination type.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d65046ffe33`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.