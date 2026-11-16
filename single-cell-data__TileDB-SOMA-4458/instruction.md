# Issue

**Title:** [py] Add `to_dict()` and `__repr__` to `PlatformConfig` and `PlatformSchemaConfig`

## Description

**Issue and/or context:** [SOMA-939]

The `PlatformConfig` and `PlatformSchemaConfig` attributes can only be viewed individually, with no convenient way to dump the full configuration for logging, diagnostics, etc. 

**Changes:**

- `PlatformConfig` and `PlatformSchemaConfig` now expose:
    - `to_dict()` returns a Python dict of all fields. 
    - `__repr__` provides a single-line representation showing each field. 

Example:

```py
import tempfile
from pprint import pprint

import pyarrow as pa

import tiledbsoma
from tiledbsoma import pytiledbsoma as clib

pc = clib.PlatformConfig()
print("\n\nrepr(pc):\n")
print(repr(pc))
print("\n\npc.to_dict():\n")
pprint(pc.to_dict())


with tempfile.TemporaryDirectory() as tmp:
    uri = f"{tmp}/sparse"
    tiledbsoma.SparseNDArray.create(uri, type=pa.float32(), shape=(100, 100)).close()
    with tiledbsoma.SparseNDArray.open(uri) as arr:
        cfg = arr.schema_config_options()
        print("\n\nrepr(cfg):\n")
        print(repr(cfg))
        print("\n\ncfg.to_dict():\n")
        pprint(cfg.to_dict())
```

Output:

```text
repr(pc):

PlatformConfig(dataframe_dim_zstd_level=3, sparse_nd_array_dim_zstd_level=3, dense_nd_array_dim_zstd_level=3, write_X_chunked=True, goal_chunk_nnz=100000000, remote_cap_nbytes=2400000000, capacity=100000, offsets_filters='["DOUBLE_DELTA", "BIT_WIDTH_REDUCTION", "ZSTD"]', validity_filters='', allows_duplicates=False, tile_order=None, cell_order=None, attrs='', dims='', consolidate_and_vacuum=False)


pc.to_dict():

{'allows_duplicates': False,
 'attrs': '',
 'capacity': 100000,
 'cell_order': None,
 'consolidate_and_vacuum': False,
 'dataframe_dim_zstd_level': 3,
 'dense_nd_array_dim_zstd_level': 3,
 'dims': '',
 'goal_chunk_nnz': 100000000,
 'offsets_filters': '["DOUBLE_DELTA", "BIT_WIDTH_REDUCTION", "ZSTD"]',
 'remote_cap_nbytes': 2400000000,
 'sparse_nd_array_dim_zstd_level': 3,
 'tile_order': None,
 'validity_filters': '',
 'write_X_chunked': True}


repr(cfg):

PlatformSchemaConfig(capacity=100000, allows_duplicates=False, tile_order='row-major', cell_order='row-major', offsets_filters='[{"COMPRESSION_LEVEL":-1,"COMPRESSION_REINTERPRET_DATATYPE":17,"name":"DOUBLE_DELTA"},{"BIT_WIDTH_MAX_WINDOW":256,"name":"BIT_WIDTH_REDUCTION"},{"COMPRESSION_LEVEL":-1,"name":"ZSTD"}]', validity_filters='[{"COMPRESSION_LEVEL":-1,"name":"RLE"}]', attrs='{"soma_data":{"filters":[{"COMPRESSION_LEVEL":-1,"name":"ZSTD"}]}}', dims='{"soma_dim_0":{"filters":[{"COMPRESSION_LEVEL":3,"name":"ZSTD"}],"tile":"2048"},"soma_dim_1":{"filters":[{"COMPRESSION_LEVEL":3,"name":"ZSTD"}],"tile":"2048"}}')


cfg.to_dict():

{'allows_duplicates': False,
 'attrs': '{"soma_data":{"filters":[{"COMPRESSION_LEVEL":-1,"name":"ZSTD"}]}}',
 'capacity': 100000,
 'cell_order': 'row-major',
 'dims': '{"soma_dim_0":{"filters":[{"COMPRESSION_LEVEL":3,"name":"ZSTD"}],"tile":"2048"},"soma_dim_1":{"filters":[{"COMPRESSION_LEVEL":3,"name":"ZSTD"}],"tile":"2048"}}',
 'offsets_filters': '[{"COMPRESSION_LEVEL":-1,"COMPRESSION_REINTERPRET_DATATYPE":17,"name":"DOUBLE_DELTA"},{"BIT_WIDTH_MAX_WINDOW":256,"name":"BIT_WIDTH_REDUCTION"},{"COMPRESSION_LEVEL":-1,"name":"ZSTD"}]',
 'tile_order': 'row-major',
 'validity_filters': '[{"COMPRESSION_LEVEL":-1,"name":"RLE"}]'}
```

**Notes for Reviewer:**

PR includes two other fixes:

- Fixed the `schema_config_options` docstring which incorrectly said the method returned a `PlatformConfig`, rather than a `PlatformSchemaConfig`.
- `PlatformConfig.dense_nd_array_dim_zstd_level` is now bound to the correct C++ member.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3d46320bf219`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.