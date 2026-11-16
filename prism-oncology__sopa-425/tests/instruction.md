# Issue

**Title:** Increase point write speed for sopa.io.explorer.write

## Description

Hi Quentin,

I started using Sopa again after quite some time and I noticed that writing transcripts for the explorer was way slower than I remembered. For an average dataset of mine it takes > 12 hours now.

After some investigation this seems to be connected to the update to Zarr v3 in 96832a1 and 1fe1bee.

This slowed transcript writing as it added an additional loop over the data to build GRIDS_ATTRS.
In addition zarr 3 create_array seems to have quite a lot more overhead than zarr 2.

In this draft I made some changes that increase speed by a lot.

<img width="939" height="719" alt="speed_comparison_v2" src="https://github.com/user-attachments/assets/a420c38a-ef80-4d90-a89b-e8f33fe829c6" />


Summary what was changed:

- Instead of a separate loop over the tiles to build GRIDS_ATTRS we can have a single write loop and then append grids/.zattrs at the end
- `np.where(tiles_str_indices == str_index)` was scanning all transcripts per tile, which can be avoided with a groupby
- As the structure of transcripts.zarr.zip is very simple it can be generated without the high level API which would call a lot of unccesary `_open_to_write()` on the Zip


Disclaimer: This was LLM assisted as I don't know much about .zarr internals

I verified that this change does not affect the output transcripts.zarr.zip, It can still be read by Explorer without any issues.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4267f75f33a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.