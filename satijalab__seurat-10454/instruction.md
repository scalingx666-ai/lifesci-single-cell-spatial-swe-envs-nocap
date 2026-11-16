# Issue

**Title:** Fix Radius returning NULL for VisiumV2 images

## Description

## The bug

`Radius()` returns `NULL` for every `VisiumV2` image, including all Visium HD data.

```r
image <- Read10X_Image("…/spatial", image.name = "tissue_lowres_image.png")
class(image)
#> [1] "VisiumV2"

Radius(image, scale = "lowres")
#> NULL

Seurat:::Radius.VisiumV2(image, scale = "lowres")
#> [1] 0.00769987
```

The method exists and computes the right answer. It is simply never reached.

## Root cause

`Radius.VisiumV2` is defined in `R/objects.R`, but its roxygen block carries the tag from the block above it:

```r
#' @method Radius VisiumV1      # <- should be VisiumV2
#' @export
#'
Radius.VisiumV2 <- Radius.VisiumV1
```

Roxygen therefore emitted `S3method(Radius,VisiumV1)` twice and never generated an entry for `VisiumV2`. `NAMESPACE` on `main` confirms it:

```
S3method(Radius,STARmap)
S3method(Radius,SlideSeq)
S3method(Radius,VisiumV1)
```

Because `VisiumV2` extends `FOV` extends `SpatialImage`, dispatch walks past the unregistered method and lands on `SeuratObject:::Radius.SpatialImage`, whose entire body is `return(NULL)`. Nothing errors, so the failure is silent.

## User-visible impact

The only caller in the package is spot sizing in spatial plots (`R/visualization.R`):

```r
spot.radius <- Radius(object = image, scale = image.scale)
base.point.size <- if (length(spot.radius) == 1L) {
  unit(spot.radius, "npc")
} else {
  unit(rep_len(1, nrow(data)), "mm")
}
```

With `NULL`, `length(spot.radius) == 1L` is `FALSE`, so every spot is drawn at a fixed **1 mm** rather than at a radius scaled to the image. Visium V2 and Visium HD plots lose their spot scaling, and because the fallback produces a plausible-looking figure, nothing signals that it happened.

## The fix

Correct the `@method` tag and add the missing `S3method(Radius,VisiumV2)` entry. No behaviour change beyond dispatch now reaching the existing, already-correct method.

## Tests

`test_load_10X.R` already asserted the scaled radius and **was failing on `main`** for exactly this reason:

```
Failure ('test_load_10X.R:108:5'): Read10X_Image works as expected
Expected `(spot.radius/scale.factors[["lowres"]] * max(dim(image.lowres)))`
  to equal `scale.factors.expected[["spot"]]`.
Lengths differ: 0 is not 1
```

Verified that the round-trip now recovers the value from `scalefactors_json.json` exactly (89.47248).

Added a test that names the mechanism, so a future regression is diagnosed rather than merely observed: it asserts the S3 method is registered, that `Radius()` returns a single positive number, and that dispatching through the generic gives the same value as calling `Radius.VisiumV2` directly.

`tests/testthat/test_load_10X.R`: **5 failures before, 0 failures and 28 passing after**. Full suite on the branch: 534 passing, 0 failures.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c3f504b1eb2e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.