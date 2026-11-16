# Issue

**Title:** Refactor flux algorithm to use Image2DModel with chunked ome-zarr storage

## Description

The flux algorithm stored results inefficiently as points DataFrames and required pre-existing raster points. Refactored to use Image2DModel with chunked ome-zarr for better memory efficiency and native spatial data support.

## Changes

**Storage Architecture**
- Store flux results as Image2DModel with channels: gene expressions, embeddings (flux_embed_*), RGB colors, counts
- Use dask arrays with configurable `chunk_size` parameter (default: 10000)
- Enable chunked ome-zarr writes via `sdata.write_element()`
- Add adaptive multiscale pyramids (2x, 4x downsampling) for images ≥32px

**Raster Grid Generation**
- Create spatial grid programmatically from shape bounds and resolution
- Use geopandas spatial join to assign grid points to cells
- Remove dependency on pre-existing `{instance_key}_raster` points

**Computation Pipeline**
- Maintain sparse matrices during flux computation
- Convert sparse results to chunked images only for final storage
- Update `set_points_metadata()` to preserve sparse DataFrame columns

**API Changes**
- Results at `sdata.images["{instance_key}_flux"]` instead of `sdata.points["{instance_key}_raster"]`
- Metadata in `sdata.tables["table"].uns["flux_image_key"]` and `"flux_channel_names"`
- Fixed `scipy` version constraint: `~=1.10.0` → `>=1.11.0` for Python 3.12 compatibility
- Renamed imported `radius` function to `compute_radius` to avoid parameter shadowing

## Example

```python
import bento as bt

bt.tl.flux(
    sdata=sdata,
    points_key="transcripts",
    instance_key="cell_boundaries",
    chunk_size=5000  # Control memory usage
)

# Access flux image with all channels
flux_img = sdata.images["cell_boundaries_flux"]
gene_channels = sdata.tables["table"].uns["flux_genes"]
```

## Notes

Downstream functions (`fluxmap`, `fe_fazal2019`, `fe_xia2019`) expect the old raster points format and will require updates to work with image-based storage.

<!-- START COPILOT CODING AGENT SUFFIX -->

<details>

<summary>Original prompt</summary>

> refactor the bt.tl.flux algorithm to store values more efficiently via sparse matrices and chunked writing to spatialdata via ome-zarr

</details>

<!-- START COPILOT CODING AGENT TIPS -->
---

💬 We'd love your input! Share your thoughts on Copilot coding agent in our [2 minute survey](https://gh.io/copilot-coding-agent-survey).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3c6ff70def96`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.