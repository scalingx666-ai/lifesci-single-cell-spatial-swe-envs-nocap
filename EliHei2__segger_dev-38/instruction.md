# Issue

**Title:** Preliminary support for SpatialData Zarr file for Xenium data

## Description

This PR addresses the Xenium part of the first task ("Method 1") of this issue  i.e. it shows an example of running `segger` of a `.zarr` file, for a Xenium dataset, saved using `sdata.write()`.

@EliHei2 @andrewmoorman this PR mostly leaves things untouched and implements extra behavior only for data that is detected to be written using the `spatialdata` package (this check is done in a simple way for the moment: by looking the column values of the Parquet files).

I ask you for your code review in particular for two things:
- [ ] I use `read_table` instead of `ParquetFile`, please check that it is fine.
- [ ] I made some bugfixes around the repo, please check that you agree with them.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `196ac7ad064a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.