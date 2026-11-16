# Issue

**Title:** Filter clonotype clusters to be displayed by anndata.obs data

## Description

Currently there is a problem with too crowded clonotype clustering result graphs. Therefore I was asked to implement something to filter the clonotype clusters that should be displayed in the result graph. My solution would be to allow the user to pass a list with cell indices of anndata.obs to the clonotype_network function. Only clusters that contain at least one of these cells should be shown. The call could look like this:

```python
condition = (adata.obs['gex:patient'] == 'Lung1') & (adata.obs['gex:source'] == 'Tumor')
cell_index_filter = adata.obs.index[condition].tolist()
ir.tl.clonotype_network(adata, min_cells=1, sequence="aa", metric="hamming", cell_index_filter=cell_index_filter)
_ = ir.pl.clonotype_network(adata, color="gex:patient", label_fontsize=9, panel_size=(7, 7), base_size=20)
```

![image](https://github.com/user-attachments/assets/d14b32b0-9299-46f2-ab47-2a93eda40a32)

That way the user would be able to do quite flexibel filtering which could be interesting for result graphs of any size. If this filtering would be done already at the beginning of the pipeline (before ir_dist) you couldn't see the whole clusters the filtered cells are part of. What do you think about this approach @grst ?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4bc951ede5d7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.