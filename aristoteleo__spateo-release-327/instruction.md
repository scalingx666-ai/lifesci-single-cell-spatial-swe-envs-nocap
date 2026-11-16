# Issue

**Title:** Added MERFISHVI and SpatialVI

## Description

```python
from spateo.external.MERFISHVI import MERFISHVI  



MERFISHVI.setup_anndata(adata_concat, batch_key="batch")
MERFISHVI.setup_nonspatial_anndata(adata=adata_sc)

model = MERFISHVI(
    adata_spatial=adata_concat,
    adata_nonspatial=adata_sc,  # 可选的非空间模态
    n_hidden=128,
    n_latent=30,
    n_spatial=10
)

model.train(max_epochs=100)

gene_means = model.get_normalized_expression(
    n_samples=1,
    transform_batch="2000panel",
)
adata_concat.layers['Impute_2000'] = gene_means

gene_means = model.get_normalized_expression(
    n_samples=1,
    transform_batch="250panel",
)
adata_concat.layers['Impute_250'] = gene_means

adata_concat.obsm["X_MERFISHVI"] = model.get_latent_representation()

```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d94230fcda6f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.