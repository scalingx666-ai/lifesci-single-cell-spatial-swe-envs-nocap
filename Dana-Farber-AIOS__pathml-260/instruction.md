# Issue

**Title:** Improve h5path read/write

## Description

This PR fixes a read/write bug when .h5path contains a counts matrix created by our QuantifyMIF transform #159. The problem was that certain types are not supported by AnnData. 

Meanwhile we now use proper scope 
```python3
with h5py.File() as f:
```
instead of 
```
f = h5py.File()
```
when adding counts.

Since read/write for .h5path breaks when reading a file edited by QuantifyMIF, I think we should add this change directly to master.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dfb3d1106bf4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.