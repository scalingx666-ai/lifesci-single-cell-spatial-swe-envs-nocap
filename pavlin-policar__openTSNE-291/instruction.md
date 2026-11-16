# Issue

**Title:** Pickle HNSW indices natively

## Description

.

## What was broken

With numpy input and a current hnswlib, HNSW pickling already worked. It failed when the training data was a pandas DataFrame: `__setstate__` read `state["data"].data.shape`, which only numpy arrays have.

## Changes

- **Native pickling.** `hnswlib.Index` has supported pickling since hnswlib 0.5.0, so the index is now pickled as part of the object's state, without our own temp-file and base64 code. Pickles are about half the size, keep the index settings (space, dim, ef), and don't depend on the type of the training data.
- **Dependency.** The `hnsw` extra is raised from `hnswlib~=0.4.0` (a 2020 release without native pickling) to `hnswlib>=0.5.0`.
- **Old pickles still load.** Pickles written by openTSNE<=1.0.4 store the index base64-encoded. They still load, now including ones whose data was a DataFrame, but raise a `FutureWarning` asking the user to re-save the object, so this code path can be removed in a later release.
- **Small refactor.** The metric-to-space mapping, previously written out twice, is now one class attribute, `HNSW.HNSW_SPACES`.

## Tests

- A save/load round trip for every supported metric (no warning raised), and one with DataFrame input.
- Loading old base64 pickles with array and DataFrame data, checking that it raises a `FutureWarning`.
- Pickling a full `TSNEEmbedding` built with `neighbors="hnsw"`; after loading, `transform` gives the same result.
- The Windows skips on the HNSW pickle tests are removed, since the index no longer writes temp files. **This is the first time these tests run on Windows.**

The DataFrame tests fail on master. Run locally on macOS with hnswlib 0.8.0: the nearest-neighbor tests and the TSNEEmbedding tests pass. I also loaded a pickle written by master's code with this branch: `transform` output was identical.

## Not in this PR

HNSW returns squared Euclidean distances, while the other methods return plain distances. It also returns uint64/float32 instead of int64/float64. Both change results, so they will be handled in a separate PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7d7f5cf621e9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.