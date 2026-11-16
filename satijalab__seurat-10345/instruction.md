# Issue

**Title:** Streamline spatial plotting for Visium data

## Description

# Summary

Improve plotting performance for Visium data.

- Check Visium image dimensions without loading it as a grob
- Avoid expensive dataframe operations on segmentation data by handling polygons and centroids _separately_ (improves segmentation centroid plotting time drastically)
- Only construct an image grob when `image.alpha > 0`
- Move color palette construction to new (internal) utility function `.BuildDiscreteScale`
- Restructure code for readability
- Introduce `stroke.alpha` parameter to control stroke and fill transparency separately

## Tests & benchmarking

`obj` contains 376,419 8um bins and 84,031 cell segmentations. The data is available for download at https://www.10xgenomics.com/datasets/visium-hd-three-prime-mouse-brain-fresh-frozen.

<details><summary>Expand to see object creation details</summary>

```R
library(Seurat)
obj <- Load10X_Spatial(data.dir = "~/mouse_brain_sr_4", bin.size = c(8, "polygons"))

# create a VisiumV1 image
obj@images$slice1.008um.v1 <- Read10X_Image(image.dir="~/mouse_brain_sr_4/binned_outputs/square_008um/spatial", assay = "Spatial.008um", slice = "slice1.008um.v1", image.type="VisiumV1")

# define groupings (pseudo clusters)
tc_seg <- GetTissueCoordinates(obj@images[["slice1.polygons"]]) # segmentations
obj$x <- tc_seg$x[match(colnames(obj), tc_seg$cell)]
obj$y <- tc_seg$y[match(colnames(obj), tc_seg$cell)]
tc_bin <- GetTissueCoordinates(obj@images[["slice1.008um"]]) # bins
idx <- match(colnames(obj), tc_bin$cell) # preserve the coords already set so do if-else matching
obj$x <- ifelse(is.na(idx), obj$x, tc_bin$x[idx])
obj$y <- ifelse(is.na(idx), obj$y, tc_bin$y[idx])

# set regions
# print ranges to define breaks prior to this step
x_breaks <- c(-Inf, 4000, 10000, 16000, Inf)
y_breaks <- c(-Inf, 10000, Inf)
obj$x_cut <- cut(obj$x, breaks = x_breaks, labels = FALSE)
obj$y_cut <- cut(obj$y, breaks = y_breaks, labels = FALSE)
obj$region <- as.numeric(interaction(obj$x_cut, obj$y_cut))
```

</details>

- - -

Benchmarking was performed with `ggplot2::benchplot(...plotting command...); graphics.off()`. Compared to the release version, we see a substantial speedup for plotting segmentation centroids (particularly for the `draw` step, 28x) with minor speedup for other cases.

<details><summary>benchplot results w/ changes from this branch</summary>

Note there is some variability in times.

```
> ggplot2::benchplot(SpatialDimPlot(obj, images = "slice1.polygons", group.by = "region")); graphics.off()
       step user.self sys.self elapsed
1 construct     0.059    0.002   0.062
2     build     0.038    0.003   0.041
3    render     0.071    0.002   0.077
4      draw     0.177    0.011   0.183
5     TOTAL     0.345    0.018   0.363
> ggplot2::benchplot(SpatialDimPlot(obj, images = "slice1.polygons", plot_segmentations = TRUE, group.by = "region")); graphics.off()
Changing image annotation limits to work with ggplot2 < 4.0.0.
       step user.self sys.self elapsed
1 construct     0.618    0.050   0.675
2     build     0.665    0.175   0.853
3    render     0.130    0.023   0.155
4      draw     0.702    0.084   0.765
5     TOTAL     2.115    0.332   2.448
> ggplot2::benchplot(SpatialDimPlot(obj, images = "slice1.008um", group.by = "region")); graphics.off()
       step user.self sys.self elapsed
1 construct     0.240    0.015   0.256
2     build     0.138    0.028   0.168
3    render     0.111    0.009   0.119
4      draw     0.768    0.058   0.817
5     TOTAL     1.257    0.110   1.360
> ggplot2::benchplot(SpatialDimPlot(obj, images = "slice1.008um.v1", group.by = "region")); graphics.off()
       step user.self sys.self elapsed
1 construct     0.340    0.010   0.352
2     build     0.140    0.024   0.172
3    render     0.110    0.011   0.122
4      draw     0.741    0.057   0.791
5     TOTAL     1.331    0.102   1.437
> ggplot2::benchplot(SpatialDimPlot(obj, images = "slice1.polygons", group.by = "region", image.alpha = 0)); graphics.off()
       step user.self sys.self elapsed
1 construct     0.063    0.004   0.066
2     build     0.038    0.005   0.047
3    render     0.048    0.003   0.053
4      draw     0.182    0.027   0.201
5     TOTAL     0.331    0.039   0.367
> ggplot2::benchplot(SpatialDimPlot(obj, images = "slice1.polygons", plot_segmentations = TRUE, group.by = "region", image.alpha = 0)); graphics.off()
       step user.self sys.self elapsed
1 construct     0.609    0.038   0.652
2     build     0.673    0.179   0.877
3    render     0.123    0.018   0.142
4      draw     0.726    0.113   0.812
5     TOTAL     2.131    0.348   2.483
> ggplot2::benchplot(SpatialDimPlot(obj, images = "slice1.008um", group.by = "region", image.alpha = 0)); graphics.off()
       step user.self sys.self elapsed
1 construct     0.247    0.018   0.267
2     build     0.137    0.014   0.152
3    render     0.084    0.004   0.088
4      draw     0.963    0.070   1.028
5     TOTAL     1.431    0.106   1.535
> ggplot2::benchplot(SpatialDimPlot(obj, images = "slice1.008um.v1", group.by = "region", image.alpha = 0)); graphics.off()
       step user.self sys.self elapsed
1 construct     0.303    0.005   0.308
2     build     0.136    0.019   0.158
3    render     0.084    0.007   0.093
4      draw     0.734    0.061   0.782
5     TOTAL     1.257    0.092   1.341
```
</details>

- - -

```R
path <- "~/seurat-clones/seurat" # should point to this branch
devtools::load_all(path)
# print(git2r::repository_head(repo = path))
# print(packageVersion("Seurat"))

p1 <- SpatialDimPlot(obj, images = "slice1.polygons", group.by = "region") + ggtitle("segmentations | centroids")
p2 <- SpatialDimPlot(obj, images = "slice1.polygons", plot_segmentations = TRUE, group.by = "region") + ggtitle("segmentations | polygons")
p3 <- SpatialDimPlot(obj, images = "slice1.008um", group.by = "region") + ggtitle("8um bins | VisiumV2")
p4 <- SpatialDimPlot(obj, images = "slice1.008um.v1", group.by = "region") + ggtitle("8um bins | VisiumV1")

p1.5 <- SpatialDimPlot(obj, images = "slice1.polygons", group.by = "region", label = T) + ggtitle("segmentations | centroids | label")
p2.5 <- SpatialDimPlot(obj, images = "slice1.polygons", plot_segmentations = TRUE, group.by = "region", label = T) + ggtitle("segmentations | polygons | label")
p3.5 <- SpatialDimPlot(obj, images = "slice1.008um", group.by = "region", label = T) + ggtitle("8um bins | VisiumV2 | label")
p4.5 <- SpatialDimPlot(obj, images = "slice1.008um.v1", group.by = "region", label = T) + ggtitle("8um bins | VisiumV1 | label")

p5 <- SpatialDimPlot(obj, images = "slice1.polygons", group.by = "region", image.alpha = 0) + ggtitle("segmentations | centroids | no image")
p6 <- SpatialDimPlot(obj, images = "slice1.polygons", plot_segmentations = TRUE, group.by = "region", image.alpha = 0) + ggtitle("segmentations | polygons | no image")
p7 <- SpatialDimPlot(obj, images = "slice1.008um", group.by = "region", image.alpha = 0) + ggtitle("8um bins | VisiumV2 | no image")
p8 <- SpatialDimPlot(obj, images = "slice1.008um.v1", group.by = "region", image.alpha = 0) + ggtitle("8um bins | VisiumV1 | no image")

p9 <- p1 + p2 + p3 + p4 + p1.5 + p2.5 + p3.5 + p4.5 + p5 + p6 + p7 + p8 + patchwork::plot_layout(nrow = 3, ncol = 4)

# ggsave(p9, filename="p9.png", width=20, height=10, dpi=300)
```

<img width="800" alt="p9" src="https://github.com/user-attachments/assets/e16da8f1-8424-415b-ad66-fed8b8ff8104" />

<br/>Also tested SlideSeq, `crop=F` argument, various color palettes (RColorBrewer palette (both name and number), other palettes (ex. "glasbey"), vector of colors (both named and unnamed)).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `86902e639f1b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.