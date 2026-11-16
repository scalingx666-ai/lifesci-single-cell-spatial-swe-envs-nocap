# Issue

**Title:** ignore the tissue section image when it does't exist and fixed the bug for seurat in new obtain data api etc

## Description

+ ignore the tissue section image when it does't exist

```
> spe2 <- spe
> imgData(spe2) <- NULL
> spe |> sc_spatial("ENSG00000168314", image.rotate.degree=-90, image.mirror.axis=NULL) -> p1
> spe2 |> sc_spatial("ENSG00000168314", image.rotate.degree=-90, image.mirror.axis=NULL) -> p2
> p1 + p2
```
![image](https://github.com/YuLab-SMU/ggsc/assets/17870644/ab832995-e456-484b-bd4e-5abc21e03b6c)

```
> spe |> sc_spatial("ENSG00000168314", image.rotate.degree=-90, image.mirror.axis=NULL, density=T) -> f1
> spe2 |> sc_spatial("ENSG00000168314", image.rotate.degree=-90, image.mirror.axis=NULL, density=T) -> f2
```
![image](https://github.com/YuLab-SMU/ggsc/assets/17870644/e63600a5-e3e6-4849-9175-3bf635790c00)

The `density` is deferent because the `coords` was calculated with the `scaleFactor` when `imgData` exists.

+ fixed a bug for `Seurat` in new api

```
> pbmc |> class()
[1] "Seurat"
attr(,"package")
[1] "SeuratObject"
> pbmc |> sc_dim()
```
![image](https://github.com/YuLab-SMU/ggsc/assets/17870644/9807a42b-33b8-416c-81a3-c6407217d771)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c3e487547d29`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.