# Issue

**Title:** NickAkhmetov/Add `globalDisable3d` prop and prevent hidden layers from being loaded/affecting performance

## Description

#### Background

A view config that suppressed 3D on the legacy `layerController` gains an unsuppressable 3D switch when it moves to `layerControllerBeta`: the beta controller renders the switch for any image with more than one z-slice and never reads `disable3d` or `globalDisable3d`. Flipping that switch is expensive in a way the legacy stack was not, because `spatialBeta`'s `createImageLayers()` builds a viv `VolumeLayer` for _every_ image layer, and `VolumeLayer` downloads a whole volume per channel from `updateState`. DeckGL does not gate layer updates on `visible`, so hidden layers load too.

The legacy `spatial` view filtered `imageLayerDefs` by `layer.use3d === use3d`, so exactly one volume was ever loaded no matter how many images a config held.

We hit this in the HuBMAP portal on a seqFISH dataset: 18 co-located hybridization-cycle images in one spatial view, each 2048x2048x11 with 4 channels. Switching to 3D tried to pull ≈755 MB across ≈360 concurrent range requests, and the view sat on viv's `Loading Volume xx%...` indefinitely.

#### Change List

- `layerControllerBeta` accepts `globalDisable3d`, threaded from `LayerControllerSubscriber` through  `LayerController` to `GlobalDimensionSlider`, which withholds the 3D switch when set. The Z-slice slider is unaffected.
- `spatialBeta` skips building a layer for hidden image layers when in 3D, via a new  `isLayerVisible` helper. It compares against `false` rather than falsiness so that an unset  `spatialLayerVisible` still counts as visible, matching `ImageLayerController`'s own default.

#### Notes for reviewers

- **Why a boolean and not the legacy `disable3d` name list.** The beta stack has one switch per view  driving the shared `spatialRenderingMode`, so there is no per-layer 3D state to disable. Beta layer  names also come from `ImageWrapper.getName()` — the image's own OME metadata — rather than from the  view config, and the `image.ome-tiff` file def has no `name` field, so a config author has nothing  to match against. On the dataset above, all 18 files report the same OME `Name`  (`MMStack_Pos10`, the acquisition position) even though the config distinguishes them, so a name-keyed list would have matched all layers or none.
- **`globalDisable3d` is a negated name**, which we are trying to avoid. Kept to match the existing prop of the same meaning on the legacy `layerController`, so configs can move between stacks unchanged. Happy to rename to `enable3d` (default `true`) if preferred — the internal prop passed down to `GlobalDimensionSlider` is already named that way.
- **Hidden-layer skipping does not fix the all-layers-visible case.** A config where every layer is visible still loads one volume per layer. Capping how many volumes load at once reads as a product decision rather than a bug fix, so this PR leaves it alone; it only makes the cost controllable by a config that hides layers, which today it is not.
- `packages/view-types/spatial-beta/src/utils.test.js` is a new file here and is also added by the `spatialBeta` 3D physical-size PR (#2551). If both land, the merge is additive (two `describe` blocks).
- The `pnpm-lock.yaml` diff adds `@testing-library/react` as a devDependency of
  `@vitessce/layer-controller-beta` for the new component test; the one unrelated `deprecated:` annotation in that diff came from pnpm refreshing registry metadata.

#### Testing

- `GlobalDimensionSlider.test.jsx` — asserts the 3D switch is present by default, absent when 3D is disabled (and that the Z-slice slider survives), and absent on a non-Z dimension.
- `spatial-beta/src/utils.test.js` — pins `isLayerVisible`, in particular that an unset value counts as visible.
- Full workspace suite: 56 files / 333 tests passing. `eslint` clean on both changed packages (5 pre-existing warnings in untouched files). `tsc --build` clean for both packages.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `780cb082ba35`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.