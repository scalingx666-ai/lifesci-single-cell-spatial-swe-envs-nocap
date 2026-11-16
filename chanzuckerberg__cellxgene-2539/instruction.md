# Issue

**Title:** feat: add cli annotation subcommand

## Description

https://app.zenhub.com/workspaces/single-cell-5e2a191dad828d52cc78b028/issues/chanzuckerberg/cellxgene/2518

#### Reviewers
**Functional:**
@MaximilianLombardo @seve @atarashansky @MDunitz 

**Readability:** 

---

## Changes
Adds `cellxgene annotate` subcommand. This invokes an arbitrary MLflow model that accepts an H5AD file as input and outputs an H5AD (or updates existing H5AD) with annotations added. The initial use case is for a cell type annotation ML model.

I've commented out test_api test_static unit test(s), as this is the only failing backend test. It is just the favicon request that is failing, and we can fix that as another issue/PR.

### QA

```
cellxgene annotate --help

cellxgene annotate -i /PATH/TO/SOME.h5ad  -m s3://cellxgene-annotation-public/cell_type/models/hlca_mlflow_model_13a81625757c4e05865971deae3f51b2.zip -o /PATH/TO/OUTPUT.h5ad  -g feature_name --no-use-gpu

cellxgene launch /PATH/TO/OUTPUT.h5ad
open localhost:5005
# look for `cxg_cell_type_predicted` annotation `cxg_cell_type_umap` umap
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d2b20129f7a3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.