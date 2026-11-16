# Issue

**Title:** Heatmaps look for existing colors in `adata.uns`

## Description

**The issue:** I found that because `cnv.pl.chromosome_heatmap` and `cv.pl.chromosome_heatmap_summary` create a copy of the `adata` input in CNV-space, colors mapped to categorical `adata.obs` fields were not transferred to this `tmp_adata` and thus didn't make the plots.

**The fix:** I simply added a quick check for `"{}_colors".format(groupby)` in `adata.uns`, and add a `tmp_adata.uns["{}_colors".format(groupby)]` key with the corresponding colors from the original `adata` if so.

**Minimal reproducible example**: Adapted from [`tutorial_3k`](https://icbi-lab.github.io/infercnvpy/tutorials/tutorial_3k.html)

Here's a PDF of a notebook containing the below code for convenience:
[infercnvpy_heatmap_color_fix.pdf](https://github.com/icbi-lab/infercnvpy/files/9418063/infercnvpy_heatmap_color_fix.pdf)
```
import scanpy as sc
import infercnvpy as cnv
import matplotlib.pyplot as plt

sc.settings.set_figure_params(figsize=(5, 5))

adata = cnv.datasets.maynard2020_3k()

cnv.tl.infercnv(
    adata,
    reference_key="cell_type",
    reference_cat=[
        "B cell",
        "Macrophage",
        "Mast cell",
        "Monocyte",
        "NK cell",
        "Plasma cell",
        "T cell CD4",
        "T cell CD8",
        "T cell regulatory",
        "mDC",
        "pDC",
    ],
    window_size=250,
)

cnv.pl.chromosome_heatmap(adata, groupby="cell_type")

# these should match colors in above heatmap
adata.uns["cell_type_colors"]

# define custom color dictionary for a couple cell types
colordict = {
    "Epithelial cell":"#e377c2",  # pink
    "Endothelial cell":"#d62728",  # red
}
# let's change colors for cell_type in adata
for x in list(colordict.keys()):
    adata.uns["cell_type_colors"][list(adata.obs.cell_type.cat.categories).index(x)] = colordict[x]

# indexes 4 and 5 should be updated now
adata.uns["cell_type_colors"]

# now, Epithelial cell should be pink and Endothelial cell should be red
cnv.pl.chromosome_heatmap(adata, groupby="cell_type")
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `245224135c1f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.