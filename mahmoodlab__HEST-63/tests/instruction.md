# Issue

**Title:** HESTData: update `to_spatial_data()```

## Description

## This PR

Makes several changes to the `HESTData.to_spatial_data()` behaviour: 
* Converts images to different resolutions(`fullres`, `hires_downsampled` and `lowres_downsampled`). 
* Saves full resolution version as `datatree` to prevent buffer error raised in #61




## Test instructions

```
from hest import load_hest
hest_data = load_hest('../hest_data', id_list=['TENX68'])
st = hest_data[0]
st.to_spatial_data(fullres=True)
```

Alternatively, run the first cell in `tutorials/2-Interacting-with-HEST-1k.ipynb`. 



## Expected behaviour

Old `SpatialData` conversion for sample `TENX68`

```
SpatialData object
├── Images
│     └── 'he': DataArray[cyx] (3, 38232, 20690)
├── Shapes
│     ├── 'cellvit': GeoDataFrame shape: (77165, 3) (2D shapes)
│     └── 'tissue_contours': GeoDataFrame shape: (2, 2) (2D shapes)
└── Tables
      └── 'anndata': AnnData (1657, 18085)
with coordinate systems:
    ▸ 'global', with elements:
        he (Images), cellvit (Shapes), tissue_contours (Shapes)
```
⬇️ ⬇️ ⬇️ 

New `SpatialData` conversion: 

```
SpatialData object
├── Images
│     ├── 'ST_downscaled_hires_image': SpatialImage[cyx] (3, 4779, 2586)
│     ├── 'ST_downscaled_lowres_image': SpatialImage[cyx] (3, 1000, 541)
│     └── 'ST_fullres_image': DataTree[cyx] (3, 38232, 20690), (3, 19116, 10345)
├── Shapes
│     ├── 'cellvit': GeoDataFrame shape: (77165, 3) (2D shapes)
│     ├── 'locations': GeoDataFrame shape: (1657, 2) (2D shapes)
│     └── 'tissue_contours': GeoDataFrame shape: (2, 2) (2D shapes)
└── Tables
      └── 'table': AnnData (1657, 18085)
with coordinate systems:
    ▸ 'ST_downscaled_hires', with elements:
        ST_downscaled_hires_image (Images), cellvit (Shapes), locations (Shapes), tissue_contours (Shapes)
    ▸ 'ST_downscaled_lowres', with elements:
        ST_downscaled_lowres_image (Images), cellvit (Shapes), locations (Shapes), tissue_contours (Shapes)
    ▸ 'ST_fullres', with elements:
        ST_fullres_image (Images), cellvit (Shapes), locations (Shapes), tissue_contours (Shapes)
 ```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `56b242670f4b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.