# Issue

**Title:** Standardize coordinate system used in InteractiveSpatialPlot

## Description

# Errors

Previously, when running InteractiveSpatialPlot on VisiumV2, Visium HD, Xenium, or SlideSeq-derived Seurat objects, the coordinate system would be inconsistent when plotting. For instance, sometimes the axes scale would follow the original dimensions of the tissue image, or the original cell coordinates, or neither:

<img width="218" height="251" alt="image" src="https://github.com/user-attachments/assets/737d3af2-c677-45f5-aef3-4cb805da290c" />


## Fix

This fix addresses this issue by introducing a sub function into InteractiveSpatialPlot called create_axis_ticks, which is responsible for retrieving the original cell coordinate scaling and mapping it onto the axes labels while not affecting the original tissue overlay. Additionally, the parameter pt.size.factor is introduced into InteractiveSpatialPlot, allowing users to customize the size of the points visualized within the plot gadget. 

<img width="203" height="207" alt="image" src="https://github.com/user-attachments/assets/c665cd7b-fcb8-4111-aa22-c60e3d75a34c" />

**Reproducible Example** (this example should produce the plot shown above if run on this [dataset](https://cf.10xgenomics.com/samples/spatial-exp/4.0.1/Visium_HD_3prime_Zebrafish_Head/Visium_HD_3prime_Zebrafish_Head_web_summary.html)):

```{R}
#Launch interactive gadget
InteractiveSpatialPlot(object, pt.size.factor=0.1)
```

With this fix, the following should work:
- Lassoing cells of interest using InteractiveSpatialPlot with a consistent coordinate system for Visium V2, Visium HD, Xenium, and SlideSeq objects
- Adjusting representative size of points within InteractiveSpatialPlot

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e35abd442520`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.