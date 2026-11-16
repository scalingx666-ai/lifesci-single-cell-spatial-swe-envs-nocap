# Issue

**Title:** Fix size deprecation warnings in ImageDimPlot and ImageFeaturePlot

## Description

Currently, when using ImageDimPlot or ImageFeaturePlot in Seurat with ggplot2 v4.0.0+, users encounter the following warnings: 

### Warnings

1: The size argument of element_rect() is deprecated as of ggplot2 3.4.0.
i Please use the linewidth argument instead.
i The deprecated feature was likely used in the Seurat package.
This warning is displayed once every 8 hours.
Call lifecycle::last_lifecycle_warnings() to see where this warning was generated.

2: The size argument of element_line() is deprecated as of ggplot2 3.4.0.
i Please use the linewidth argument instead.
i The deprecated feature was likely used in the Seurat package.
This warning is displayed once every 8 hours.
Call lifecycle::last_lifecycle_warnings() to see where this warning was generated.

This quick fix addresses these warnings by replacing the "size" parameters in element_rect, element_line, and geom_polygon as used in visualization.R with "linewidth", which ggplot2 has mentioned to supersede the size variable: https://ggplot2.tidyverse.org/news/index.html

With these changes, the following commands should have the same behaviour and not cause warnings when running either ggplot2 <4.0.0 or 4.0.0+:

```{R}
#Load in any sample object that is plotted via ImageDim/FeaturePlot
#In this case, we use xenium.obj from https://satijalab.org/seurat/articles/seurat5_spatial_vignette_2

#This command results in the warnings above without these changes
ImageDimPlot(xenium.obj, fov = "fov", molecules = c("Gad1", "Sst", "Pvalb", "Gfap"), nmols = 20000)

#The size parameter here can be changed to change the graph with the same behaviour between older and newer ggplot2 versions
ImageFeaturePlot(xenium.obj, features = c("Cux2", "Rorb", "Bcl11b", "Foxp2"), max.cutoff = c(25,
    35, 12, 10), size = 0.75, cols = c("white", "red"))
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d49e46de00e9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.