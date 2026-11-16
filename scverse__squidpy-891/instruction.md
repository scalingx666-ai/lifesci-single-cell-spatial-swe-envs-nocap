# Issue

**Title:** Fix sparse matrix interactions in `sq.gr.utils`.

## Description

Made to be compatible with new `anndata` release.

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description

In `sq.gr.utils`, we change mentions of `SparseCSRView` and  `SparseCSCView` to  `SparseCSRMatrixView` and  `SparseCSCMatrixView`, respectively. We also update `pyproject.toml` to use `anndata>=0.11.0rc1`. I suppose that the latter is still under development, but I feel it will soon be part of the main release.

## How has this been tested?

Unfortunately I ran into an error when trying to test this locally:
```
(squidpy_development) [shahula@lanec1 squidpy]$ tox -e py310-linux -- tests/graph/test_utils.py
.pkg: _optional_hooks> python /work/magroup/shahula/bin/miniconda3/envs/squidpy_development/lib/python3.10/site-packages/pyproject_api/_backend.py True hatchling.build
.pkg: get_requires_for_build_editable> python /work/magroup/shahula/bin/miniconda3/envs/squidpy_development/lib/python3.10/site-packages/pyproject_api/_backend.py True hatchling.build
.pkg: build_editable> python /work/magroup/shahula/bin/miniconda3/envs/squidpy_development/lib/python3.10/site-packages/pyproject_api/_backend.py True hatchling.build
py310-linux: install_package_deps> python -I -m pip install 'Pillow>=8.0.0' 'aiohttp>=3.8.1' 'anndata>=0.11.0rc1' 'cycler>=0.11.0' 'dask-image>=0.5.0' 'dask[array]>=2021.02.0' 'docrep>=0.3.1' 'fsspec>=2021.11.0' 'leidenalg>=0.8.2' 'matplotlib-sc
alebar>=0.8.0' 'matplotlib>=3.3' 'networkx>=2.6.0' 'numba>=0.56.4' 'numpy>=1.23.0' 'omnipath>=1.0.7' 'pandas>=2.1.0' 'scanpy>=1.9.3' 'scikit-image>=0.20' 'scikit-learn>=0.24.0' 'spatialdata>=0.2.0' 'statsmodels>=0.12.0' 'tifffile!=2022.4.22' 'tq
dm>=4.50.2' 'validators>=0.18.2' 'xarray>=0.16.1' 'zarr>=2.6.1'
py310-linux: install_package> python -I -m pip install --force-reinstall --no-deps /work/magroup/shahula/spatiotemporal_transcriptomics_integration/squidpy/.tox/.tmp/package/2/squidpy-1.6.2.dev1+ge6b5b0c.d20240923-py3-none-any.whl
py310-linux: commands[0]> python -m pytest --cov --cov-append --cov-report=xml --cov-config=/work/magroup/shahula/spatiotemporal_transcriptomics_integration/squidpy/tox.ini --ignore docs/ tests/graph/test_utils.py --test-napari
ImportError while loading conftest '/work/magroup/shahula/spatiotemporal_transcriptomics_integration/squidpy/tests/conftest.py'.
tests/conftest.py:20: in <module>
    import spatialdata as sd
.tox/py310-linux/lib/python3.10/site-packages/spatialdata/__init__.py:54: in <module>
    from spatialdata import dataloader, datasets, models, transformations
.tox/py310-linux/lib/python3.10/site-packages/spatialdata/datasets.py:21: in <module>
    from spatialdata._core.operations.aggregate import aggregate
.tox/py310-linux/lib/python3.10/site-packages/spatialdata/_core/operations/aggregate.py:20: in <module>
    from spatialdata._core.operations._utils import _parse_element
.tox/py310-linux/lib/python3.10/site-packages/spatialdata/_core/operations/_utils.py:8: in <module>
    from spatialdata.models import SpatialElement
.tox/py310-linux/lib/python3.10/site-packages/spatialdata/models/__init__.py:18: in <module>
    from spatialdata.models.models import (
.tox/py310-linux/lib/python3.10/site-packages/spatialdata/models/models.py:20: in <module>
    from multiscale_spatial_image import to_multiscale
.tox/py310-linux/lib/python3.10/site-packages/multiscale_spatial_image/__init__.py:14: in <module>
    from .multiscale_spatial_image import MultiscaleSpatialImage
.tox/py310-linux/lib/python3.10/site-packages/multiscale_spatial_image/multiscale_spatial_image.py:7: in <module>
    from zarr.storage import BaseStore
.tox/py310-linux/lib/python3.10/site-packages/zarr/__init__.py:2: in <module>
    from zarr.codecs import *
.tox/py310-linux/lib/python3.10/site-packages/zarr/codecs.py:2: in <module>
    from numcodecs import *
.tox/py310-linux/lib/python3.10/site-packages/numcodecs/__init__.py:25: in <module>
    from numcodecs.version import version as __version__
E   ModuleNotFoundError: No module named 'numcodecs.version'
py310-linux: exit 4 (10.90 seconds) /work/magroup/shahula/spatiotemporal_transcriptomics_integration/squidpy> python -m pytest --cov --cov-append --cov-report=xml --cov-config=/work/magroup/shahula/spatiotemporal_transcriptomics_integration/squidpy/tox.ini --ignore docs/ tests/graph/test_utils.py --test-napari pid=9214
.pkg: _exit> python /work/magroup/shahula/bin/miniconda3/envs/squidpy_development/lib/python3.10/site-packages/pyproject_api/_backend.py True hatchling.build
  py310-linux: FAIL code 4 (79.67=setup[68.77]+cmd[10.90] seconds)
  evaluation failed :( (80.53 seconds)
```

but this should be a drop-in fix...

## Closes

This  .

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8cfd4ba552c1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.