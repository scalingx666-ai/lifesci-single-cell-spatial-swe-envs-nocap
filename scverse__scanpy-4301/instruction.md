# Issue

**Title:** ci: more robust tests

## Description

## benchmarks

fail because a conflict between the `dask` meta package’s `pyarrow` dependency and `hdf5`.

```
$ pixi add hdf5=2.2.* pyarrow
├─ hdf5 2.2.* … would require aws-c-common >=0.14.3,<0.14.4.0a0 … conflicts
└─ pyarrow * … libarrow 25.0.0 would require aws-sdk-cpp >=1.11.833
      └─ aws-c-common >=0.14.2,<0.14.3.0a0 … conflicts
```

This causes it to to pull in `dask` 2023, so by avoiding `pyarrow` we can get new dask and new h5py.

## notebook tests

are flaky because of two groups flip-flopping

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9df46b48096a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.