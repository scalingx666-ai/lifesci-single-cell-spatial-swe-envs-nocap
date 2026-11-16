# Issue

**Title:** Fix InteractiveSpatialPlot axes orientation

## Description

# Issues

The following issues have been reported at:
- 
- 

## Issue 1

Currently, spatial objects loaded in from a segmented_outputs folder contain cellular coordinates that are in a different coordinate space than those loaded in from a binned_outputs folder. These objects would be plotted incorrectly within InteractiveSpatialPlot, which has lead to confusion when trying to subset cells about the actual position of cellular regions. This has been harmonized with the latest release of SeuratObject v5.3.0.

Example of InteractiveSpatialPlot on Visium objects with segmentations:

<img width="372" height="349" alt="image" src="https://github.com/user-attachments/assets/17bab783-d5ed-4d96-bac7-b1d90b07e131" />

This fix addresses this issue by swapping the x and y plotting axes for all instances of InteractiveSpatialPlot going forward. With these changes, the x axis should always be plotted horizontally, and the y axis should always be plotted vertically for any spatial object. For certain platforms such as Xenium and Vizgen, InteractiveSpatialPlot will plot differently than ImageDimPlots and ImageFeaturePlots, this flip is intentional and better matches the orientation used by Xenium Viewer and MERSCOPE Visualizer:

InteractiveSpatialPlot (LEFT) vs ImageFeaturePlot (RIGHT) of [Vizgen Merfish Mouse Brain](https://info.vizgen.com/mouse-brain-data) 
<img width="344" height="227" alt="image" src="https://github.com/user-attachments/assets/b5d7d88d-0f59-4a26-a7cf-7a3aea4334f7" /><img width="218" height="288" alt="image" src="https://github.com/user-attachments/assets/82659377-6fe5-4477-b54b-4c432af24809" />

MERSCOPE Viewer:
<img width="333" height="339" alt="image" src="https://github.com/user-attachments/assets/3bf31e59-58e3-48a7-a699-003d59f26679" />

This fix also adds a "Selected cells" count for InteractiveSpatialPlot which helps to indicate how many cells are being selected by a lasso.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e9ea1980b185`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.