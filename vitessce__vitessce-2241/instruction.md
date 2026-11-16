# Issue

**Title:** Hide the overall image layer on `spatialLayerVisible: false`

## Description

#### Background
The image layer creation was only using `channelsVisible` to control visibility, but DeckGL/VIV layers require both:
- `channelsVisible` - controls which channels within a layer are visible
- `visible` - controls the overall layer visibility

The `visible` property was missing from the layer configuration, causing the layer to always render regardless of the `spatialLayerVisible` coordination value.

#### Change List
- Added `visible` property to the Layer construction options of `createImageLayer`

#### Checklist
 - [x] Have tested PR with one or more demo configurations
 - [ ] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ceb035980aad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.