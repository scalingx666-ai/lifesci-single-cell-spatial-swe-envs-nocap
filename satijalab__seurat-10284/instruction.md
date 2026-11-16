# Issue

**Title:** Quick patch to #10278

## Description

Patch to fix error resulting from #10278: added safe check for `image` slot to avoid errors when plotting SlideSeq objects, as both Visium binned data and SlideSeq data take the `"spatial"` code path of the `geom` switch case in `SingleSpatialPlot`.

<details> <summary> Testing results </summary>

Code chunk from spatial vignette using `ssHippo` data from `SeuratData`.

```R
plot1 <- VlnPlot(slide.seq, 
                 features = 'nCount_Spatial', 
                 pt.size = 0, log = TRUE) + NoLegend()

slide.seq$log_nCount_Spatial <- log(slide.seq$nCount_Spatial)

plot2 <- SpatialFeaturePlot(slide.seq, 
                            features = 'log_nCount_Spatial') + 
          theme(legend.position = "right")

wrap_plots(plot1, plot2)
```

<img width="150" src="https://github.com/user-attachments/assets/47e34554-5b14-4d23-a54c-633e60a32623" />

Previous examples in #10278 also work.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9d844a6a90c7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.