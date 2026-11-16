# Issue

**Title:** Fix panel/axis scales for spatial plots when `crop = FALSE`

## Description

## Summary

### Issue

Panel scales in `GeomSpatial` (ggproto class) aren't being set to the correct ranges when `crop = F`, which becomes obvious when working with spatial images that do not have an aspect ratio of ~1. The initial solution of specifying an aspect ratio (#10276) was the incorrect approach, as the underlying axis ranges were the reason for the distortion in appearance.

### Fixes to `crop = FALSE` condition (non-default)

* Say the dimensions of the image, height (`nrow`) x width (`ncol`), are in a 2-element vector `dim`; then, the fixes proposed here are to:
  * Define the x range as `(0, dim[2])`
  * Define the y range as `(-dim[1], 0)` (this, as before, gets reversed when plotting to display as `(0, image_dim[1])`, increasing downwards on the axis
  * ~~Use `coord_fixed` instead of `theme` to define the aspect ratio for the `crop = F` case `(dim[1] / dim[2])`~~

* We make sure to set the proper `xlim` and `ylim` in `coord_fixed` so that, if plotting axis labels, the correct ranges are shown. Otherwise the cropped ranges -- the actual range within which the data lies -- will be shown rather than the range of the entire image, which is what we want.

* Here we also make sure that the `crop` argument works for segmented data (in the case of plotting centroids or polygons).

* Prior to ggplot2 4.0.0, `coord_*` layers did not recognize reversed axes (with `scale_y_reverse` for example) so a condition has to be added to make sure we are using the correct axis ranges for earlier versions. This is pretty much only relevant when a user adds axis labels to the visualization.

| original tissue image | dimensions |
| --- | --- |
| <img width="200" src="https://github.com/user-attachments/assets/6ff4b902-bbf4-4652-8091-0a114c8959e1" /> | `6000 x 4456 x 3` |

## Example (fixed)

Below, `kidney_segm` contains segmented data and `kidney_8um` contains 8um binned data.

```R
a <- SpatialDimPlot(kidney_segm,
                    plot_segmentations = TRUE,
                    image.scale = "hires", 
                    crop = T) + NoLegend() +
  theme(axis.text.x  = element_text(size = 10),
        axis.text.y  = element_text(size = 10),
        axis.title.x = element_text(size = 10),
        axis.title.y = element_text(size = 10))

b <- SpatialDimPlot(kidney_segm,
                    plot_segmentations = TRUE,
                    image.scale = "hires", 
                    crop = F) + NoLegend() +
  theme(axis.text.x  = element_text(size = 10),
        axis.text.y  = element_text(size = 10),
        axis.title.x = element_text(size = 10),
        axis.title.y = element_text(size = 10))

a + b
```

<img width="1860" height="1015" alt="a_b_" src="https://github.com/user-attachments/assets/ab468f85-5ea8-4466-a75a-4499296bea75" />

```R
c <- SpatialDimPlot(kidney_8um,
                    image.scale = "hires", 
                    crop = T) + NoLegend() +
  theme(axis.text.x  = element_text(size = 10),
        axis.text.y  = element_text(size = 10),
        axis.title.x = element_text(size = 10),
        axis.title.y = element_text(size = 10))

d <- SpatialDimPlot(kidney_8um,
                    image.scale = "hires", 
                    crop = F) + NoLegend() +
  theme(axis.text.x  = element_text(size = 10),
        axis.text.y  = element_text(size = 10),
        axis.title.x = element_text(size = 10),
        axis.title.y = element_text(size = 10))

c + d
```

<img width="1860" height="1015" alt="c_d_" src="https://github.com/user-attachments/assets/271ea2a7-d314-465c-a71a-c76a26e8b3de" />

## To-do
- [x] Test with ggplot2 < v4.0.0

- - -
<details> <summary>Session info</summary>

```R
R version 4.3.2 (2023-10-31)
Platform: x86_64-pc-linux-gnu (64-bit)
Running under: Ubuntu 20.04.6 LTS

Matrix products: default
BLAS:   /usr/lib/x86_64-linux-gnu/blas/libblas.so.3.9.0 
LAPACK: /usr/lib/x86_64-linux-gnu/lapack/liblapack.so.3.9.0

locale:
 [1] LC_CTYPE=en_US.UTF-8       LC_NUMERIC=C               LC_TIME=en_US.UTF-8       
 [4] LC_COLLATE=en_US.UTF-8     LC_MONETARY=en_US.UTF-8    LC_MESSAGES=en_US.UTF-8   
 [7] LC_PAPER=en_US.UTF-8       LC_NAME=C                  LC_ADDRESS=C              
[10] LC_TELEPHONE=C             LC_MEASUREMENT=en_US.UTF-8 LC_IDENTIFICATION=C       

time zone: America/New_York
tzcode source: system (glibc)

attached base packages:
[1] stats     graphics  grDevices utils     datasets  methods   base     

other attached packages:
[1] Seurat_5.4.0.9005  testthat_3.3.1     SeuratObject_5.3.0 sp_2.2-0          

loaded via a namespace (and not attached):
  [1] RcppAnnoy_0.0.22       splines_4.3.2          later_1.4.4            tibble_3.3.0          
  [5] polyclip_1.10-7        fastDummies_1.7.5      lifecycle_1.0.4        sf_1.0-13             
  [9] rprojroot_2.1.1        processx_3.8.6         globals_0.18.0         lattice_0.21-8        
 [13] hdf5r_1.3.8            MASS_7.3-60            magrittr_2.0.4         plotly_4.11.0         
 [17] rmarkdown_2.30         yaml_2.3.10            remotes_2.5.0.9000     httpuv_1.6.16         
 [21] otel_0.2.0             sctransform_0.4.2      spam_2.11-1            sessioninfo_1.2.3     
 [25] pkgbuild_1.4.8         spatstat.sparse_3.1-0  reticulate_1.43.0      cowplot_1.2.0         
 [29] pbapply_1.7-4          DBI_1.2.3              RColorBrewer_1.1-3     abind_1.4-8           
 [33] pkgload_1.4.1          Rtsne_0.17             purrr_1.1.0            ggrepel_0.9.6         
 [37] irlba_2.3.5.1          listenv_0.9.1          spatstat.utils_3.2-0   units_0.8-2           
 [41] goftest_1.2-3          RSpectra_0.16-2        spatstat.random_3.4-2  fitdistrplus_1.2-4    
 [45] parallelly_1.45.1      codetools_0.2-19       tidyselect_1.2.1       farver_2.1.2          
 [49] matrixStats_1.5.0      spatstat.explore_3.5-3 jsonlite_2.0.0         e1071_1.7-13          
 [53] ellipsis_0.3.2         progressr_0.17.0       ggridges_0.5.7         survival_3.5-7        
 [57] systemfonts_1.3.1      tools_4.3.2            ragg_1.2.5             ica_1.0-3             
 [61] Rcpp_1.1.0             glue_1.8.0             gridExtra_2.3          xfun_0.53             
 [65] usethis_2.2.1          RcppProgress_0.4.2     dplyr_1.1.4            withr_3.0.2           
 [69] fastmap_1.2.0          callr_3.7.6            digest_0.6.37          R6_2.6.1              
 [73] mime_0.13              textshaping_0.3.6      scattermore_1.2        tensor_1.5.1          
 [77] dichromat_2.0-0.1      spatstat.data_3.1-9    tidyr_1.3.1            generics_0.1.4        
 [81] data.table_1.17.8      class_7.3-22           httr_1.4.7             htmlwidgets_1.6.4     
 [85] uwot_0.2.3             pkgconfig_2.0.3        gtable_0.3.6           lmtest_0.9-40         
 [89] S7_0.2.0               brio_1.1.5             htmltools_0.5.8.1      profvis_0.3.8         
 [93] dotCall64_1.2          scales_1.4.0           png_0.1-8              spatstat.univar_3.1-4 
 [97] knitr_1.50             rstudioapi_0.14        reshape2_1.4.4         nlme_3.1-163          
[101] proxy_0.4-27           cachem_1.1.0           zoo_1.8-14             stringr_1.5.1         
[105] KernSmooth_2.23-22     parallel_4.3.2         miniUI_0.1.2           arrow_21.0.0          
[109] desc_1.4.3             pillar_1.11.1          grid_4.3.2             vctrs_0.6.5           
[113] RANN_2.6.2             urlchecker_1.0.1       promises_1.4.0         xtable_1.8-4          
[117] cluster_2.1.6          evaluate_1.0.5         cli_3.6.5              compiler_4.3.2        
[121] rlang_1.1.6            future.apply_1.20.0    labeling_0.4.3         classInt_0.4-9        
[125] ps_1.9.1               plyr_1.8.9             fs_1.6.6               stringi_1.8.7         
[129] viridisLite_0.4.2      deldir_2.0-4           assertthat_0.2.1       lazyeval_0.2.2        
[133] devtools_2.4.5         spatstat.geom_3.6-0    Matrix_1.6-4           RcppHNSW_0.6.0        
[137] RcppEigen_0.3.4.0.2    patchwork_1.3.2.9000   bit64_4.6.0-1          future_1.67.0         
[141] ggplot2_3.5.2          shiny_1.11.1           ROCR_1.0-11            igraph_2.2.0          
[145] memoise_2.0.1          bit_4.6.0
```

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `063a41a820ec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.