# Issue

**Title:** Method to detect specimens in H&E images

## Description

For other downstream functions, such as  one needs a function to robustly detect where in the image the tissue is and how many of those there are.

This function
a) implements two algorithms for identifying the tissue (otsu & felzenszwalb)
b) deals with arbitrary channel input
c) heuristically tries to identify what is a sample and what is either just random stuff (dirt, Visium frame etc). As a fallback, one can pass in the number of samples expected which should be more robust
d) adds the mask back to the sdata object with the same structure and transformations as the original image had
e) does everything in dask so it's quite fast

```
sdata = sq.datasets.visium_hne_sdata()

sq.exp.im.detect_tissue(
    sdata,
    image_key="hne",
)

sdata
```
```
SpatialData object, with associated Zarr store: [/Users/tim.treis/.cache/squidpy/visium_hne_sdata.zarr](https://file+.vscode-resource.vscode-cdn.net/Users/tim.treis/.cache/squidpy/visium_hne_sdata.zarr)
├── Images
│     └── 'hne': DataTree[cyx] (3, 11757, 11291), (3, 5878, 5645), (3, 2939, 2822), (3, 1469, 1411)
├── Labels
│     └── 'hne_tissue': DataTree[yx] (11757, 11291), (5878, 5645), (2939, 2822), (1469, 1411)
├── Shapes
│     └── 'spots': GeoDataFrame shape: (2688, 2) (2D shapes)
└── Tables
      └── 'adata': AnnData (2688, 18078)
with coordinate systems:
    ▸ 'global', with elements:
        hne (Images), hne_tissue (Labels), spots (Shapes)
with the following elements not in the Zarr store:
    ▸ hne_tissue (Labels)
```

```
(
    sdata
    .pl.render_images("hne")
    .pl.render_labels("hne_tissue", fill_alpha=0, contour_px=10, outline_alpha=1)
    .pl.show()
)
```
<img width="482" height="491" alt="image" src="https://github.com/user-attachments/assets/6a8ff5be-dd47-400d-b847-58ec7fc931af" />

## Todo
- [ ] Manual tests on a bunch of different inputs IHC / H&E / DAPI / multichannel etc
- [ ] Test with multiple samples in the same image
- [ ] Write unit tests for functions

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a3061c237f78`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.