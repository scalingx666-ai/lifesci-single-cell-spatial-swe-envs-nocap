# Issue

**Title:** fix: clear the warnings CI emits

## Description

## Description

Drops the number of warnings from 2173 to 244 in the CIs. Things that needed fix are fixed. Things that are expected and will be removed are marked as ignored for cleaner reports. Rest are also bound to change.

**Fixed at the source**
- Drop the `n_jobs` argument that sklearn has ignored since 1.3.
- Replace `skimage.morphology.binary_closing` / `square` with `closing` /
  `footprint_rectangle`; this is what raises the `scikit-image` floor to `>=0.26`.
- Rename the deprecated `area_threshold` argument.
- Drop a deprecated `astype(..., copy=...)` and an `uns_keys()` membership check.
- Densify the ligrec plotting frames to avoid two sparse-concat `PerformanceWarning`s.
- Cache the `_bfs_shells` numba kernel.

**Expected, so silenced deliberately**
- `spatial_neighbors` is deprecated until v1.9.0 and these tests are its coverage, so
  its own notice is not a finding there.
- `ImageContainer` reads through `skimage.io`'s plugin interface; both are on the way
  out, so the remaining noise is suppressed on the 22 tests that actually read an
  image rather than file-wide.

## How has this been tested?

| | main | this branch | new warnings |
| --- | --- | --- | --- |
| py3.13 | 1525 passed, 2173 warnings (16 kinds) | 1525 passed, 244 (6 kinds) | none |
| py3.14 | 1525 passed, 2146 warnings (15 kinds) | 1525 passed, 218 (5 kinds) | none |

The third row pins the old floor to confirm the `>=0.26` bump is required by the new
morphology API rather than papering over a break: 0.25.2 still passes, it just warns.

The remaining warnings are upstream (skimage `_map_array`, numpy shape-setting, scanpy's
leiden flavour notice) or tied to code already slated for removal.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `87f9a6ad29d0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.