# Issue

**Title:** WSI I/O and Tissue Segmentation with Otsu

## Description

Hey @quentinblampey and @loic-lb,

in this PR I am adding two functions towards the goals of #19 :

```python
sopa.io.histopathology.read_wsi(path: Path) -> SpatialData
``` 
This function is using tiffslide as backend to get a zarr store from propriatery wsi formats (support is subject tifffile/tiffslide support) and returns a `SpatialData` obj with a `MultiscaleSpatialImage` and the proper transformations configurations. OpenSlide could also be used however it is not supporting python3.10 atm.

```python 
sopa.segmentation.tissue.hsv_otsu(sdata: SpatialData, **seg_params)
```
This function is performing an hsv colorspace otsu based segmentation of the tissue using the lowest available level in the WSI and appends the tissue segmentation polygons in the `SpatialData` object.

I did not do extensive tests for the different filetypes and I did not update the dependencies (the tiffslide dependency needs to be resolved).

Let me know what you think. 🔥

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `33d007eb7ff1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.