# Issue

**Title:** Fix outline color behavior

## Description

## Description

`bg_color` and `gap_color` of the outlines are not converted to RGBA arrays anymore before being passed to `_shaped_scatter()` since this would be interpreted as values to color the shapes by and lead to incorrect rendering.

## How has this been tested?
```python
adata = sq.datasets.visium_hne_adata()
sq.pl.spatial_scatter(adata, shape="circle", color="cluster", outline=True, crop_coord=(1500, 1500, 3000, 3000), groups="Cortex_1")
``` 
Before:
![grafik](https://github.com/user-attachments/assets/ffce1468-64be-4f45-8f2f-4d6f64ae5e3d)
the purple and yellow comes from the RGBA arrays of the default colors black & white ([0, 0, 0, 1] & [1, 1, 1, 1]) being interpreted as values to color the outlines by (the 4 values are recycled so that each outline gets exactly one value). Then, the 0s and 1s are mapped to a color using norm and the colormap (default viridis => that's why we get yellow and purple)
After:
![grafik](https://github.com/user-attachments/assets/cab18130-9cb2-4253-b0b3-946ae1520dd5)

## Closes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fef696671ab3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.