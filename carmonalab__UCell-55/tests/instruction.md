# Issue

**Title:** Accept any matrix-like input instead of a fixed class list

## Description

## The problem

`ScoreSignatures_UCell()` and `StoreRankings_UCell()` gate their input on an explicit list of classes:

```r
} else if (methods::is(matrix, "matrix") |
    methods::is(matrix, "dgCMatrix") |
    methods::is(matrix, "data.frame")) {
        m <- matrix
} else {
    m <- NULL
}
```

Anything else is refused with `Unrecognized input format.` That list has fallen behind the ecosystem. A `DelayedMatrix` (DelayedArray / HDF5Array), an `HDF5Matrix`, a BPCells `IterableMatrix`, or even a plain dense `dgeMatrix` is rejected:

```r
library(UCell); library(DelayedArray)
m <- matrix(rpois(60 * 40, 3), 60, 40)
dimnames(m) <- list(paste0("gene", 1:60), paste0("cell", 1:40))
d <- DelayedArray(Matrix::Matrix(m, sparse = TRUE))

ScoreSignatures_UCell(d, features = list(sig = rownames(m)[1:10]))
#> Error: Unrecognized input format.
```

I ran into this while adding a `DelayedArray` layer backend to Seurat for matrices past the `dgCMatrix` 2^31 limit (satijalab/seurat#10453). `AddModuleScore_UCell()` on the Seurat object works fine; only the bare-matrix entry points refuse.

## Why it is only the gate

The refusal is not a real limitation. `calculate_Uscore()` already opens with

```r
if (!methods::is(matrix, "dgCMatrix")) {
    matrix <- Matrix::Matrix(as.matrix(matrix), sparse = TRUE)
}
```

so the engine already accepts whatever it is handed. Only the entry-point check rejects these inputs.

## The change

Test the capability rather than enumerate classes: accept any object with a length-2 `dim()`. Enumerating classes will always trail the ecosystem; asking "is this two-dimensional and coercible" will not.

Two supporting changes:

- **Coerce sparsely when possible.** `to_dgCMatrix()` tries `as(x, "dgCMatrix")` first and keeps the previous dense route as the fallback (still needed for `data.frame`). Out-of-core backends implement the sparse coercion directly, so admitting them no longer implies building a dense intermediate first, which for these classes is the whole point. Results are unchanged for the input types that already worked.
- **A pointed error for Seurat objects.** A `Seurat` object also has a length-2 `dim()`, so it would now pass the gate and then fail confusingly downstream. It gets an explicit error naming `AddModuleScore_UCell()` (or `LayerData()` for `StoreRankings_UCell`) instead of the generic message.

## Tests

UCell has no `tests/` directory today, so this adds the minimal `testthat` scaffolding along with the cases for this change. **Happy to drop the scaffolding if you would rather keep the package without tests** and verify by hand instead; say the word.

The tests cover: the three formats that already worked (identical scores), `DelayedMatrix` and `dgeMatrix` now giving the same scores as the base-matrix reference, `StoreRankings_UCell` on a `DelayedMatrix`, non-matrix input still being rejected, and the Seurat-object error.

Against `master` they report **2 failures and 2 errors**; with this change **all 13 pass**. `testthat` and `DelayedArray` are added to `Suggests`, and every new test is guarded with `skip_if_not_installed()`.

`R CMD check` reports the same 3 WARNINGs before and after this change (deprecated `normalizeCounts` in the existing examples, plus two vignette warnings from building with `--no-build-vignettes`), so it introduces none; `checking tests ... OK` is new.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `15b029a9bf40`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.