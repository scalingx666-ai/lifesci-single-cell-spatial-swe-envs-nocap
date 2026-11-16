# Issue

**Title:** fix the issue for Seurat object

## Description

+ fixed the issues for `Seurat` object
      the `rmd` file of `docs` runs well.
      and the `make all` no error.

```
> brain |> sc_spatial(features=c("Hpca", "Ttr"), image.mirror.axis='v') -> f1
> brain |> sc_spatial(features=c("Hpca", "Ttr"), image.mirror.axis='v', density=T) -> f2
> f1 / f2
```
![image](https://github.com/YuLab-SMU/ggsc/assets/17870644/ff6dfc28-1807-4097-aa1c-38f9c7fbe2e1)

```
> spe |> sc_spatial(features=c(2000, 3000), image.rotate.degree=-90) -> p1
> spe |> sc_spatial(features=c(2000, 3000), image.rotate.degree=-90, density=T) -> p2
```
![image](https://github.com/YuLab-SMU/ggsc/assets/17870644/6246bcec-a292-4e2f-a17f-35e9afd60d19)

+ adjust the legend title when `joint=T`

```
> spe |> sc_spatial(features=c(2000, 3000), image.rotate.degree=-90, density=T, joint=T) -> p3
> spe |> sc_spatial(features=c(2000, 3000), image.rotate.degree=-90, density=T, joint=T, common.legend=F) -> p4
```
![image](https://github.com/YuLab-SMU/ggsc/assets/17870644/18dc218b-cbb0-4dae-824a-fb9bd045c21d)

```
> brain |> sc_spatial(features=c("Hpca", "Ttr"), image.mirror.axis='v', density=T, joint=T) -> f3
> brain |> sc_spatial(features=c("Hpca", "Ttr"), image.mirror.axis='v', density=T, joint=T, common.legend=F) -> f4
```
![image](https://github.com/YuLab-SMU/ggsc/assets/17870644/d77cd6ad-46ac-46d2-ac0f-091bdf345da6)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `041e3c2ca125`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.