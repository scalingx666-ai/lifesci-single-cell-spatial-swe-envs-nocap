# Issue

**Title:** add pca feature loadings

## Description

Hi, 
I notice that when harmony is used to generate the integrated reference object, then harmony reduction in the integrated reference object fails in Seurat mapping framework. 


The main reason is that the feature loadings in the harmony reduction is not an orthogonal matrix.  Projection query cells to the feature loadings in harmony reduction doesn't work under the current settings. 
However, when I replace the current feature loadings to the PCA feature loadings, Seurat mapping starts working well. 
One demo example:
```
library(Seurat)
library(SeuratData)

LoadData("ifnb")
ifnb <- NormalizeData(ifnb)%>%FindVariableFeatures()%>%ScaleData()%>%RunPCA()%>%RunUMAP(dims = 1:30)
library(harmony)
ifnb <- RunHarmony(ifnb, group.by.vars = "stim")
ifnb <- RunUMAP(ifnb, dims = 1:30, reduction = "harmony", reduction.name = "umap.harmony", reduction.key = "Uh_", return.model = T)

 pbmc3k <- LoadData("pbmc3k")
 pbmc3k <- NormalizeData(pbmc3k)
 anchor <- FindTransferAnchors(reference = ifnb,
                               reference.reduction = "harmony",
                               query = pbmc3k ,
                               k.filter = NA 
                               )
 pbmc3k <- MapQuery(anchorset = anchor,
                    query = pbmc3k, 
                    reference = ifnb, 
                    refdata = list(celltype = "seurat_annotations"),
                    reduction.model = "umap.harmony")
 
 p1 <- DimPlot(pbmc3k, reduction = "ref.umap", group.by = "predicted.celltype", label = T) + NoLegend()
 p2 <- DimPlot(pbmc3k, reduction = "ref.umap", group.by = "seurat_annotations", label = T) + NoLegend()
 
 # add pca feature loadings to the harmony reduction
 ifnb[['harmony2']] <- CreateDimReducObject(embeddings = ifnb[['harmony']]@cell.embeddings,
                                           key = "harmony2_", 
                                           loadings = ifnb[['pca']]@feature.loadings, 
                                           assay = "RNA")
 anchor  <- FindTransferAnchors(reference = ifnb,
                               reference.reduction = "harmony2",
                               query = pbmc3k ,
                               k.filter = NA 
 )
 pbmc3k <- MapQuery(anchorset = anchor,
                    query = pbmc3k, 
                    reference = ifnb, 
                    refdata = list(celltype = "seurat_annotations"),
                    reduction.model = "umap.harmony")
 p3 <- DimPlot(pbmc3k, reduction = "ref.umap", group.by = "predicted.celltype", label = T) + NoLegend()
 p4 <- DimPlot(pbmc3k, reduction = "ref.umap", group.by = "seurat_annotations", label = T) + NoLegend()

```
## reference UMAP
![image](https://user-images.githubusercontent.com/29529544/139495946-72aacf03-9bb0-47f2-bff2-15ef4368b077.png)


## current mapping result
![image](https://user-images.githubusercontent.com/29529544/139495758-2e4d77af-968f-4fef-9838-7de9a3faf426.png)

## PCA feature loadings mapping result
![image](https://user-images.githubusercontent.com/29529544/139495842-5a8214d4-2953-49f1-8f42-689ba250e468.png)


This PR is to set PCA feature loadings as the default feature loadings for harmony.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d1653870d4d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.