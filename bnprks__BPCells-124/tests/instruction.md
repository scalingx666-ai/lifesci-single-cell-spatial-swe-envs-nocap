# Issue

**Title:** enable setting HDF5_CFLAGS and HDF5_LIBS external to ./configure

## Description

The local `./configure` for BPCells does not have a mechanism for setting `HDF5_CFLAGS` and `HDF5_LIBS` external to the script, as do other `./configure` scripts; it relies only on its own internal mechanisms for determining the flags for interacting with hdf5. We do not provide hdf5 in the standard locations, but rather provide it from an Lmod module, so the include files and libraries for hdf5 are not in standard system locations..

This just uses a little bashiness to set the compilation and link flag variables to current environment variables if these are provided, otherwise it uses the current defaults.  With these changes, compilation against an hdf5 in a nonstandard location works correctly with

```
HDF5_CFLAGS="-I${HDF5_INCLUDE}" HDF5_LIBS="-L${HDF5_LIB} -lhdf5" R CMD INSTALL BPCells_0.2.0.tar.gz
```

assuming `HDF5_INCLUDE` is set to the hdf5 `.../include` directory and `HDF5_LIB` is set to its `.../lib` directory. Any other mechanism that can provide settings for these variables can be used to set these variables within the `./configure`.

This can address issues in #86 and #84.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d409a68e74c9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.