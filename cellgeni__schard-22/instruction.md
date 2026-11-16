# Issue

**Title:** feat: layers= arg routing h5ad layers to Seurat slots

## Description

Hi firstly thanks for the very useful function! I have been using schard often to shuttle things between anndata and seurat but find the layers porting difficult without loading the file twice and splice the assays together manually (e.g., 
`library(schard)`
`library(Seurat)`

`seu <- schard::h5ad2seurat('adata.h5ad')`
`log1p_mat <- GetAssayData(seu, assay = "RNA", layer = "counts")`

`raw_mat <- schard::h5ad2Matrix(f, "layers/counts")`
`dimnames(raw_mat) <- dimnames(log1p_mat)`

`seu <- SetAssayData(seu, assay = "RNA", layer = "counts", new.data = raw_mat)`
`seu <- SetAssayData(seu, assay = "RNA", layer = "data", new.data = log1p_mat)`)

I intended to add a `layers` argument into the function so this is much more friendlier.

h5ad2seurat() gains an optional `layers=` named character vector mapping Seurat slots (counts/data/scale.data) to h5ad matrices (a /layers/<name> or the literal 'X'). NULL (default) preserves the original adata.X->counts behaviour exactly. Adds internal helpers .h5ad_layer_path / .h5ad_load_layer in h5ad_util.R, reusing the existing h5ad2Matrix reader.

Skips loading adata.X only when no slot needs it (fixes a silent zero-data slot in the counts-from-layer + data='X' case present in the prototype).

Hopefully it's useful! 

**Usage**:

layers is a **named character vector**:
    • **Names** must be Seurat slots: counts, data, and/or scale.data.
    • **Values** are either a layer name found in adata.layers, or the literal "X" to refer to adata.X.
`# raw counts from a layer, log-normalised X into the data slot`
`h5ad2seurat("adata.h5ad", layers = c(counts = "counts", data = "X"))`

`# put a pre-scaled layer straight into scale.data`
`h5ad2seurat("adata.h5ad", layers = c(counts = "counts", scale.data = "scaled"))`

`# unchanged, original behaviour`
`h5ad2seurat("adata.h5ad")            # adata.X -> counts`
`Invalid input is rejected early with a clear message:`
`h5ad2seurat("adata.h5ad", layers = c(foo = "X"))`
`#> Error: `layers` must be a named character vector with names in`
`#>        {counts, data, scale.data}`

`h5ad2seurat("adata.h5ad", layers = c(counts = "nope"))`
`#> Error: layer(s) not found in adata.h5ad: nope (available: counts)`

New argument is the last positional parameter and defaults to NULL.
With layers = NULL, output verified byte-identical to the released behaviour.

Verified with devtools::load_all() against a synthetic h5ad (built with anndata, carrying a distinct counts layer and a log1p X) and a real Stereo-seq file:
    • ✅ Routing c(counts='counts', data='X'): counts slot holds raw integers, data slot holds the log1p X, and the two are distinct.
    • ✅ Default (layers=NULL): adata.X lands in counts, and the full object (dims, assay, reductions, counts sum, metadata columns, dimnames) is identical to stock schard 1.0.0 on a real file.
    • ✅ Validation guards fire for bad slot names and missing layers.
    • ✅ Package installs cleanly into a fresh library; installed copy exposes the new argument.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4bd52b4ff014`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.