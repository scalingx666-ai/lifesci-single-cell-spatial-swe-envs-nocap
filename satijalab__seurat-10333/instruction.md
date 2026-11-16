# Issue

**Title:** Update layer-building logic in E x I plots for ggplot2 v4+ compatibility

## Description

Expression-by-identity plots (VlnPlot, RidgePlot, etc) are built with `SingleExIPlot` and `MultiExIPlot`. The addition of plot layers has been handled in previous versions dynamically via `do.call("+", ...)`.

ggplot2 v4 (September 2025) [transitioned to the S7 OOP system](https://tidyverse.org/blog/2025/09/ggplot2-4-0-0/). With the new update, some users (#10101) began encountering an error when running `VlnPlot` or `RidgePlot` with the following message[^1]:

```
Error in deparse(substitute(e2, env = caller_env(2))) :
'S4SXP': should not happen - please report
Error during wrapup: 'S4SXP': should not happen - please report
```

Since `+` is a builtin primitive operator whose method dispatch is handled in the R evaluator, `do.call` can behave differently from a direct call (`plot + geom`) when working with S4/S7 objects. So the fix here is to build plots iteratively, instead of passing all layers to be added to `do.call`. 

**Below: Reprex 1 demonstrates where/how exactly the problem occurs, and reprex 2 demonstrates that the change proposed in this branch fixes the issue in `VlnPlot` and `RidgePlot`.**

[^1]: Seemed to only occur in older R versions; there were no known `deparse` errors when using the `do.call` method for plot generation with ggplot2 v4+ in R 4.5.0+.

# reprex 1
``` r
library(ggplot2)
library(sessioninfo)

###
R.version$version.string
#> [1] "R version 4.3.2 (2023-10-31)"
packageVersion("ggplot2")
#> [1] '4.0.2'
###

p <- ggplot(iris, aes(x = Species, y = Petal.Length, fill = Species))

S7::S7_inherits(p)
#> [1] TRUE
class(p)
#> [1] "ggplot2::ggplot" "ggplot"          "ggplot2::gg"     "S7_object"      
#> [5] "gg"

layer1 <- geom_violin(scale = 'width', trim = TRUE)
layer2 <- theme(axis.text.x = element_text(angle = 45, hjust = 1))

S7::S7_inherits(layer1)
#> [1] FALSE
class(layer1)
#> [1] "LayerInstance" "Layer"         "ggproto"       "gg"

S7::S7_inherits(layer2)
#> [1] TRUE
class(layer2)
#> [1] "theme"          "ggplot2::theme" "gg"             "S7_object"

geom <- list(layer1, layer2)

do.call(what = '+', args = list(p, geom))
#> Error in deparse(substitute(e2, env = caller_env(2))): 'S4SXP': should not happen - please report

for (layer in geom) {
  p <- p + layer
}

p
```

![](https://i.imgur.com/2MxjKV0.png)<!-- -->

<sup>Created on 2026-03-16 with [reprex v2.1.1](https://reprex.tidyverse.org)</sup>

# reprex 2

``` r
test_ggplot2_v4_compat <- function(path_to_seurat) {
  devtools::load_all(path_to_seurat, quiet = TRUE)
  print(git2r::repository_head(repo = path_to_seurat))
  p1 <- try(VlnPlot(pbmc_small, features = "nCount_RNA"))
  p2 <- try(RidgePlot(object = pbmc_small, features = 'PC_1'))
  return(list("vln" = p1, "ridge" = p2))
}

invisible(test_ggplot2_v4_compat("~/seurat-testing-clone/seurat"))
#> [350dfa] (Local) (HEAD) main
#> Error in deparse(substitute(e2, env = caller_env(2))) : 
#>   'S4SXP': should not happen - please report
#> Error in deparse(substitute(e2, env = caller_env(2))) : 
#>   'S4SXP': should not happen - please report

res <- test_ggplot2_v4_compat("~/seurat")
#> [9e70e0] (Local) (HEAD) fix/ggplot2-v4-compat
gridExtra::grid.arrange(res$vln, res$ridge, ncol = 2)
#> Picking joint bandwidth of 0.387
```

![](https://i.imgur.com/cLY2Apq.png)<!-- -->

<sup>Created on 2026-03-16 with [reprex v2.1.1](https://reprex.tidyverse.org)</sup>

More info:

- https://stat.ethz.ch/R-manual/R-devel/library/methods/html/Methods_for_S3.html
  - > The R evaluator will ‘dispatch’ a method from a function call either when the body of the function calls the special primitive [UseMethod](https://stat.ethz.ch/R-manual/R-devel/library/base/html/UseMethod.html) or when the call is to one of the builtin primitives such as the math functions or the binary operators.
- https://adv-r.hadley.nz/base-types.html#base-types-2
- https://cran.r-project.org/doc/manuals/r-devel/R-ints.html#Argument-evaluation-1

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `350dfa82591b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.