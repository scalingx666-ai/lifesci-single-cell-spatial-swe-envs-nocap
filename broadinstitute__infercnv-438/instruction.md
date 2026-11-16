# Issue

**Title:** Allow adding a custom column prefix when using add_to_seurat

## Description

By default, when adding an inferCNV run to a Seurat object using `add_to_seurat`, the column names are uniform for all samples (has_proportion_.cnv, top_loss, has_dupli, etc.) This means, for multiple different inferCNV runs from the same sample, adding these results to the Seurat object will overwrite the previous results added, so there is no option to add multiple inferCNV runs to a Seurat object without replacing existing results. 

This PR allows for an optional function input that is a column prefix. The prefix can be appended to the columns of the results in the Seurat metadata, so that multiple runs can be added to the metadata. By default, the input is NULL, which means that no column prefix gets added. 

Example below where inferCNV results are added from two different runs, and identified using two different column prefixes. 

```
seurat <- add_to_seurat(seurat,
  infercnv_output_path = "group_cluster_no_denoise_annot_mean_score_reduced_mal_list/",
  column_prefix = "reduced_malignant")

seurat <- add_to_seurat(seurat,
  infercnv_output_path = "group_cluster_no_denoise_annot_mean_score_in_house_mal_list/",
  column_prefix = "new_set_malignant")
```

```
DimPlot(seurat,
        group.by = c("reduced_malignant_has_loss_chr5",
                     "new_set_malignant_has_loss_chr5"),
        reduction = "umap.rna")
```

With the resulting plot, we can view the results of two inferCNV runs side by side and differentiate by the column prefix to see predicted CNV differences. 

![image](https://user-images.githubusercontent.com/40243147/179833500-fff1b49a-0ad0-4c5c-9960-4b5490de9d74.png)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `56b97ff96596`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.