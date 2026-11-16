# Issue

**Title:** fix: require spatialdata>=0.7.2 to drop the xarray-schema/pkg_resources break

## Description

.

`import squidpy` crashed on Python 3.12 / setuptools>=82 with `ModuleNotFoundError: No module named 'pkg_resources'`, traced into `xarray_schema` — pulled in transitively by spatialdata, which imported the removed `pkg_resources`.

spatialdata **0.7.2** dropped the `xarray-schema` dependency, so the proper fix is a lower-bound bump. The previous `>=0.7.1` floor (#1114) was set to drop `dask-expr` and still permits spatialdata 0.7.1, which keeps the bug.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0b432966096b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.