# Issue

**Title:** Integrate SysVI into scArches

## Description

Dear scArches dev team,

I recently open an issue on integrating SysVI, a new model from scVI that is very performant on complex integration cases. I had a little bit of time to implement it today and it was quite simple (as you can see in the changes) and would like to help anyone that would like to use this model too.

I tested it on the `scvi_surgery_pipeline.ipynb` as show below and it works on my machine.
Please let me know if I need to make any change before it is accepted, and thanks again for this great package!


```
# On normalized and log-transformed data as recommended in https://docs.scvi-tools.org/en/1.3.3/tutorials/notebooks/scrna/sysVI.html
# Setup adata for training
sca.models.SysVI.setup_anndata(
    adata=source_adata,
    batch_key=system_key,
    categorical_covariate_keys=[batch_key]
)

vae = sca.models.SysVI(
    adata=source_adata,
    embed_categorical_covariates=True
)

# Example showing how to adjust loss weights
vae.train(check_val_every_n_epoch=1)
```

[...] Umap and saving ref model
```
# Perform surgery on reference model and train on query dataset
model = sca.models.SysVI.load_query_data(
    target_adata,
    ref_path,
    freeze_dropout = True,
)

```

Session info

| Package    | Version     |
| ---------- | ----------- |
| matplotlib | 3.10.8      |
| scanpy     | 1.12        |
| torch      | 2.7.1+cu118 |
| scArches   | 0.6.1       |
| numpy      | 2.3.5       |
| gdown      | 5.2.1       |
| anndata    | 0.12.10     |
| scvi-tools | 1.4.1       |

| Dependency          | Version               |
| ------------------- | --------------------- |
| more-itertools      | 10.8.0                |
| llvmlite            | 0.46.0                |
| sympy               | 1.14.0                |
| lightning           | 2.6.1                 |
| certifi             | 2026.1.4 (2026.01.04) |
| requests            | 2.32.5                |
| seaborn             | 0.13.2                |
| matplotlib-inline   | 0.2.1                 |
| leidenalg           | 0.11.0                |
| joblib              | 1.5.3                 |
| wcwidth             | 0.6.0                 |
| tensorboard         | 2.20.0                |
| pillow              | 12.0.0                |
| numcodecs           | 0.16.5                |
| filelock            | 3.20.0                |
| sparse              | 0.17.0                |
| urllib3             | 2.6.3                 |
| statsmodels         | 0.14.6                |
| traitlets           | 5.14.3                |
| packaging           | 25.0                  |
| igraph              | 1.0.0                 |
| backports.tarfile   | 1.2.0                 |
| kiwisolver          | 1.4.9                 |
| fsspec              | 2025.12.0             |
| jupyter_client      | 8.8.0                 |
| threadpoolctl       | 3.6.0                 |
| opt_einsum          | 3.4.0                 |
| mpmath              | 1.3.0                 |
| idna                | 3.4                   |
| pyro-ppl            | 1.9.1                 |
| natsort             | 8.4.0                 |
| pyzmq               | 27.1.0                |
| stack-data          | 0.6.3                 |
| beautifulsoup4      | 4.14.3                |
| parso               | 0.8.6                 |
| attrs               | 25.4.0                |
| protobuf            | 6.33.5                |
| tqdm                | 4.66.5                |
| typing_extensions   | 4.15.0                |
| jaraco.functools    | 4.4.0                 |
| legacy-api-wrap     | 1.5                   |
| torchvision         | 0.22.1+cu118          |
| zarr                | 3.1.5                 |
| patsy               | 1.0.2                 |
| python-dateutil     | 2.9.0.post0           |
| scHPL               | 1.0.3                 |
| cycler              | 0.12.1                |
| pyparsing           | 3.3.2                 |
| soupsieve           | 2.8.3                 |
| executing           | 2.2.1                 |
| absl-py             | 2.4.0                 |
| asttokens           | 3.0.1                 |
| comm                | 0.2.3                 |
| PyYAML              | 6.0.3                 |
| newick              | 1.0.0                 |
| h5py                | 3.15.1                |
| umap-learn          | 0.5.11                |
| psutil              | 7.2.2                 |
| fast-array-utils    | 1.3.1                 |
| pure_eval           | 0.2.3                 |
| PySocks             | 1.7.1                 |
| charset-normalizer  | 3.4.4                 |
| scipy               | 1.16.3                |
| numba               | 0.63.1                |
| xarray              | 2026.1.0              |
| jaraco.text         | 4.0.0                 |
| platformdirs        | 4.7.0                 |
| triton              | 3.3.1                 |
| prompt_toolkit      | 3.0.52                |
| setuptools          | 80.10.2               |
| donfig              | 0.8.1.post1           |
| six                 | 1.17.0                |
| texttable           | 1.7.0                 |
| jaraco.context      | 6.1.0                 |
| ml_collections      | 1.1.0                 |
| jedi                | 0.19.2                |
| pandas              | 2.3.3                 |
| networkx            | 3.6.1                 |
| Pygments            | 2.19.2                |
| pytz                | 2025.2                |
| mudata              | 0.3.3                 |
| debugpy             | 1.8.20                |
| docrep              | 0.3.2                 |
| session-info2       | 0.4                   |
| jupyter_core        | 5.9.1                 |
| ipython             | 9.10.0                |
| lightning-utilities | 0.11.8                |
| pynndescent         | 0.6.0                 |
| torchmetrics        | 1.0.3                 |
| rich                | 14.3.2                |
| torchaudio          | 2.7.1+cu118           |
| decorator           | 5.2.1                 |
| google-crc32c       | 1.8.0                 |
| tornado             | 6.5.4                 |
| ipykernel           | 7.2.0                 |
| scikit-learn        | 1.8.0                 |

| Component | Info                                                                              |
| --------- | --------------------------------------------------------------------------------- |
| Python    | 3.13.11 | packaged by Anaconda, Inc. | (main, Dec 10 2025, 21:28:48) [GCC 14.3.0] |
| OS        | Linux-5.15.153.1-microsoft-standard-WSL2-x86_64-with-glibc2.39                    |
| Updated   | 2026-02-13 13:15                                                                  |

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b5ae098242cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.