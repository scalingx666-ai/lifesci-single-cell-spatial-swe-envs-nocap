# Issue

**Title:** Can load annotated slides from HF

## Description

I added annotations to two slides from our dataset on Hugging Face:
- `Xenium_V1_Human_Colon_Cancer_P5_CRC_Add_on_FFPE_outs`
- `Xenium_V1_hPancreas_Cancer_Add_on_FFPE_outs`

In particular, I saved the following columns of `adata.obs`:
- `cell_type` and `cell_type_level1`, obtained via cell-type annotation using scConcept + a reference from `cellxgene` (top-10 neighbors)
- `novae_domains_res0.8` and `novae_domains_res1` obtained via Novae in zero-shot

With this PR, we can load these annotations directly via `novae.load_dataset`, by passing `annotations=True`.
For instance:

```python
adata = novae.load_dataset("Xenium_V1_Human_Colon_Cancer_P5_CRC_Add_on_FFPE_outs", annotations=True)[0]
# now, we have cell_type / cell_type_level1 / novae_domains_res0.8 / novae_domains_res1 in the obs

sc.pl.spatial(adata, color="novae_domains_res1", spot_size=20)
```

<img width="496" height="431" alt="image" src="https://github.com/user-attachments/assets/90c073c8-b0e6-44a7-a829-af4fa37182a7" />

This will be useful for the tutorial on domains labeling, FYI @alihamraoui

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9a9dddc91be2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.