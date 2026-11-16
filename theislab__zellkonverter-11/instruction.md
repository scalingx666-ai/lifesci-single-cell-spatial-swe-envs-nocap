# Issue

**Title:** Further clean-ups

## Description

There are still two outstanding issues:

**1)** What happens with sparse matrices in the H5AD files when we set `backed=TRUE`? Are they ignored or are they all loaded into memory? `readH5AD` will need to respond to this appropriately if someone requests `use_hdf5=TRUE`.

**2)** That `AnnData` datasets are opened with `r+` by **h5py** is a real PITA. It both breaks R and is broken by R; in this case, if anyone opens a file handle (even if it's just read-only), **h5py** is not able to lock the file for writing. Conversely, R cannot open a read-only file handle if it's still locked up by **h5py**. Having an option to open files in `r` mode would solve this.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a1dbf209c7a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.