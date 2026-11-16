# Issue

**Title:** feat: add experimental IREA analysis and reference preparation

## Description

## Summary

Add experimental IREA cytokine-response and cell-polarization analysis through `RunIREA()` and `IREAPlot()`. Gene lists, numeric contrasts, contrast tables/files and Seurat comparisons share a single `object` input with S3 dispatch. Results retain the exact contrast/design settings, reference checksums and provenance, and partial human-to-mouse mapping.

Prepare official portal references with `PrepareIREA()` or the existing `PrepareDB(db = "IREA_<cell type>")` entry point, using a checksum manifest in the selected cache. IREA entries use the existing species loop and result assembly alongside annotation databases; the standalone reference reader is internal. Source settings and limitations are documented on `PrepareIREA()`. Unversioned reference files stay outside the package.

Plots reuse `plot_type`, `padjustCutoff`, palette, custom colours and theme parameters. Explicit IREA diagnostics use `log_message()`; errors terminate and preparation progress follows `verbose`. Unit tests construct small deterministic inputs directly, without bundled fixtures or development assets. Generated help and the pkgdown reference index are synchronized. NEWS remains under the development version, with no Version/Date change.

## Scope

This PR contains only the 12 IREA feature/integration files. The shared database refactor was merged separately in ; this branch incorporates that main-branch state without including its changes in the IREA diff. `PrepareDB()` routes the IREA selectors through its shared source dispatcher and forwards only the common parameters accepted by each resource interface. The mixed model/annotation/IREA return contract is covered by a regression test.

## Validation

- At `0506aa56`, 236 focused expectations passed from source and the independently installed package: 112 IREA and 124 database preparation/regression expectations, with no failures, warnings or skips.
- The general refactor's fresh chromosome preparation was verified in #454, including the actual documented default example (202,107 mappings across 26 terms). The combined tests cover cached annotations, fresh independent/dispatcher equivalence and mixed model/annotation/IREA resources.
- Previously verified IREA examples and four plot types are unchanged. Generated help, 53 installed R bodies/formals, code/document consistency, the 12-file scope and `git diff --check` were verified after synchronization with main.
- The final-head NK comparison below passed all four archived portal rows and exactly matches the pre-cleanup `d497c926` implementation. Input checksums, source commit, report and the complete rerun script are pinned below. This run uses an independently installed package and compares installed R bodies/formals with the pinned source.
- Optional `R.cache` guards remain on the three preparation test groups; the prior missing-dependency check verified those groups skip without invoking preparation. All six CI checks passed for `0506aa56`, including macOS, Windows, Ubuntu, key optional-dependency contracts and pkgdown. Platform checks ran the full package suite with examples disabled. Existing RunSingleR documentation, velocity-header compilation and SummarizedExperiment import warnings, plus Makevars/environment notes, remain; R-code dependency and compiled-code checks are OK.

## Numerical validation limits

This remains an experimental reconstruction. Full numerical equivalence to official IREA is unestablished for cytokine scores, hypergeometric tests and matrix projection. Score/projection P values compare reference-cell distributions against PBS-treated reference cells and do not provide biological-replicate inference for user case/control samples. Human orthologue mapping is partial; expression references are mouse lymph-node cells. The NK comparison below covers only the nine-gene mouse score/polarization example, using archived portal rows; no new portal submission or whole-portal concordance result is claimed.

## Reproducible NK validation for `0506aa56`

Executed at 2026-10-02 12:19:46 UTC. Analysis commit: . Original implementation: . Entry points were loaded from an independently installed package built from the pinned checkout. The script also verifies installed R bodies and formals against the pinned analysis/preparation sources.

The expected four portal rows and reference MD5 come from the [historical fixture](https://github.com/hurry060215-tech/scop/blob/d497c92696611511439f8c7fd1b29fefe14c6b2c/tests/testthat/fixtures/irea/nk_polarization_score.rds), whose [provenance note](https://github.com/hurry060215-tech/scop/blob/d497c92696611511439f8c7fd1b29fefe14c6b2c/tests/testthat/fixtures/irea/README.md) records a portal capture on 2026-09-28. This run compares against those archived rows; it does not make a new portal submission or independently recapture the portal output.

Configuration: `PrepareDB(db = "IREA_NK_cell", species = "Mus_musculus")`, `RunIREA(genes, analysis = "cell_polarization", method = "score")`; RNA `data` layer; PBS controls; BH adjustment over exactly four states. All nine genes were present: `Ifitm3, Isg15, Ifit3, Bst2, Slfn5, Isg20, Phf11b, Zbp1, Rtp4`. Reference: 31,053 genes, 13,779 cells, including 594 PBS cells. On this macOS run, the installed-package validation took 11.73 seconds wall time and peaked at 2,395,308,032 bytes RSS (2.23 GiB), including package/reference loading and the baseline/sensitivity comparisons; this is not an analysis-only performance benchmark. Recomputed per-cell scores and sample/polarization labels match the archived fixture exactly.

| State | Effect absolute error | P relative error | FDR relative error | Original-code deltas | Result |
|---|---:|---:|---:|---|---|
| NK-a | 3.116e-11 | 9.187e-12 | 1.063e-12 | effect/P/FDR = 0 | PASS |
| NK-c | 2.812e-12 | 3.387e-09 | 2.38e-09 | effect/P/FDR = 0 | PASS |
| NK-e | 1.078e-11 | 3.002e-12 | 3.371e-11 | effect/P/FDR = 0 | PASS |
| NK-f | 3.052e-11 | 1.612e-11 | 1.612e-11 | effect/P/FDR = 0 | PASS |

Acceptance thresholds: effect absolute error ≤ `1e-8`, raw P and FDR relative error ≤ `1e-8`; no extra, missing or duplicated states. All four rows passed. Current and original implementations produce exactly identical effects, raw P values and FDR. As a sensitivity check, substituting `None` for PBS produces a maximum effect error of `0.432789779671093` and is rejected. The final-head comparison CSV and input-checksum CSV match the previous frozen `6c89e30a` report byte for byte.

Scope: the mouse NK nine-gene score/polarization example only. This establishes no whole-portal or other-mode equivalence. The comparison CSV below retains the stored expected numbers and computed values at 17-digit precision.

<details>
<summary>Full comparison CSV</summary>

```csv
"term","expected_effect","actual_effect","effect_abs_error","expected_p","actual_p","p_relative_error","expected_fdr","actual_fdr","fdr_relative_error","baseline_effect_delta","baseline_p_delta","baseline_fdr_delta","n_target","n_control","pass"
"NK-a","8.9754641709000005","8.9754641708688379","3.1162628033598594e-11","4.8782656361999997e-208","4.8782656362448154e-208","9.1868734841682453e-12","1.9513062545e-207","1.9513062544979262e-207","1.0628165014736624e-12","0","0","0","1035","594",TRUE
"NK-c","-0.60811125030000002","-0.60811125029718804","2.8119728767705965e-12","0.0086702554000000001","0.0086702554293657183","3.3869496096627927e-09","0.0115603406","0.011560340572487624","2.3798931714225091e-09","0","0","0","200","594",TRUE
"NK-e","0.081331894599999996","0.081331894610783051","1.0783055004459641e-11","5.4472855222999997e-06","5.44728552231635e-06","3.0015989693765732e-12","1.0894571045000001e-05","1.08945710446327e-05","3.3714142588792129e-11","0","0","0","941","594",TRUE
"NK-f","-0.3189909809","-0.31899098093052314","3.0523139571414504e-11","0.98174670409999998","0.98174670411582976","1.6123991031236073e-11","0.98174670409999998","0.98174670411582976","1.6123991031236073e-11","0","0","0","348","594",TRUE
```

</details>

<details>
<summary>Input provenance, sizes and checksums</summary>

The three reference assets are from the official Immune Dictionary static downloads. The archived expected rows and original R implementation are pinned to the historical Git commit. Input acquisition commands are provided below.

```csv
"file","bytes","md5","sha256"
"downloadableData_ligands-seurat-NK_cell.RDS",133591388,"f4eabfa734a61ad839879fd84aa7a8e9","4ffffa8babd6a32c849b5e6d5922c218f1fa3586ed617be30b2e453b78c3de59"
"dataFiles_SuppTable3_Cytokine_Signatures.xlsx",5015978,"776311e9f831c94fd73801ca8b87fb3e","c99ff0b3ac36c070a85883ba4f403e894c7afb0fb2b232fce3a2ddacf26c866c"
"dataFiles_SuppTable7_Polarization_Signatures.xlsx",1170754,"c5b4e7ef840bf6746030dabacee8a753","60c8670d4040c846c49db72c1095b4d147894dd903116ed3bfd67b1c5ba66569"
"nk_expected.rds",66684,"5868df82ac7f63c0bd0d5b0aca06ba99","3c486d65ac4ce70868f29e681c67df5709ce9bca1ca3c6aba924b6c17fca5168"
"baseline-IREA.R",20338,"5125e83d7d541491b1f970dceec6cdd7","e388282049c237aa70c836da234bea0d1d5b7e472a2708778d9032639868a325"
```

Current source SHA-256:

```text
R/RunIREA.R  d0b6448d9d9164983c3f8b4be00fc26858426fee18adf6d6aba4391d37ab4897
R/PrepareDB.R  47531a0bf2e4b11e4e3e8d0dfb995bd39265e9d77f70584edcffff7fdfca87a9
R/PrepareDBAnnotation.R  00e0abb81c1bbd4bc09945e4325e11bbc4ec845c6cf808127d230c321d35e02d
R/custom_db_utils.R  0ce4cf62b498f9223dc2f2f904dfcb306af34eb9a1233485ce4f31249a049b1a
```

The official static URLs are unversioned. The script checks SHA-256 before analysis and fails if a retrieved input differs, rather than silently using a changed reference. The exact inputs, source snapshots, script, comparison, checksums, metadata and session information are also preserved in an evidence archive outside the package. No fixture, data asset or validation script is added to the PR tree.

</details>

<details>
<summary>Runtime and complete rerun command</summary>

Recorded runtime: R version 4.5.3 (2026-03-11); Seurat 5.5.0, SeuratObject 5.4.0, Matrix 1.7.6, readxl 1.5.0, thisutils 0.5.2, digest 0.6.39, jsonlite 2.0.0, R.cache 0.17.0, scop 0.9.2. All `DESCRIPTION` Imports and the listed analysis packages must already be installed in the R library used by `Rscript`.

```sh
set -eu
# Run in an empty evidence directory, outside the package checkout.
# Save the validate_nk.R block below as ./validate_nk.R first.
git clone --no-checkout https://github.com/hurry060215-tech/scop.git source
git -C source checkout --detach 0506aa56f3782a7e53e80d1b87eeedd7264777ad
mkdir -p inputs reports library
git -C source show d497c92696611511439f8c7fd1b29fefe14c6b2c:tests/testthat/fixtures/irea/nk_polarization_score.rds > inputs/nk_expected.rds
git -C source show d497c92696611511439f8c7fd1b29fefe14c6b2c:R/IREA.R > inputs/baseline-IREA.R
curl --fail --location --retry 3 'https://www.immune-dictionary.org/static/downloadableData/ligands-seurat-NK_cell.RDS' --output 'inputs/downloadableData_ligands-seurat-NK_cell.RDS'
curl --fail --location --retry 3 'https://www.immune-dictionary.org/static/dataFiles/SuppTable3_Cytokine_Signatures.xlsx' --output 'inputs/dataFiles_SuppTable3_Cytokine_Signatures.xlsx'
curl --fail --location --retry 3 'https://www.immune-dictionary.org/static/dataFiles/SuppTable7_Polarization_Signatures.xlsx' --output 'inputs/dataFiles_SuppTable7_Polarization_Signatures.xlsx'
R CMD INSTALL --library="$(pwd)/library" source > reports/install.log 2>&1
Rscript validate_nk.R source inputs reports library > reports/run.log 2>&1
cat reports/run.log
```

Outputs: `reports/comparison.csv`, `input_checksums.csv`, `genes.txt`, `run_metadata.json`, `sessionInfo.txt` and `run.log`.

</details>

<details>
<summary>Complete validate_nk.R</summary>

```r
args <- commandArgs(trailingOnly = TRUE)
if (length(args) != 4L) stop("Usage: Rscript validate_nk.R SOURCE INPUTS REPORTS LIBRARY")
repo <- normalizePath(args[[1]], mustWork = TRUE)
inputs <- normalizePath(args[[2]], mustWork = TRUE)
output <- args[[3]]
dir.create(output, recursive = TRUE, showWarnings = FALSE)
commit <- "0506aa56f3782a7e53e80d1b87eeedd7264777ad"
started_at <- proc.time()
source_files <- c("R/RunIREA.R", "R/PrepareDB.R", "R/PrepareDBAnnotation.R", "R/custom_db_utils.R")
baseline_commit <- "d497c92696611511439f8c7fd1b29fefe14c6b2c"
library_path <- normalizePath(args[[4]], mustWork = TRUE)
.libPaths(c(library_path, .libPaths()))
packages <- c("scop", "Seurat", "SeuratObject", "Matrix", "readxl", "thisutils", "digest", "jsonlite", "R.cache")
for (package in packages) {
  if (!requireNamespace(package, quietly = TRUE)) stop("Missing package: ", package)
}
head <- system2("git", c("-C", shQuote(repo), "rev-parse", "HEAD"), stdout = TRUE)
stopifnot(identical(head, commit))
dirty <- system2("git", c("-C", shQuote(repo), "status", "--porcelain", "--",
  source_files), stdout = TRUE)
if (length(dirty)) stop("Analysis source files differ from the pinned commit.")
pinned <- c(
  "downloadableData_ligands-seurat-NK_cell.RDS" = "4ffffa8babd6a32c849b5e6d5922c218f1fa3586ed617be30b2e453b78c3de59",
  "dataFiles_SuppTable3_Cytokine_Signatures.xlsx" = "c99ff0b3ac36c070a85883ba4f403e894c7afb0fb2b232fce3a2ddacf26c866c",
  "dataFiles_SuppTable7_Polarization_Signatures.xlsx" = "60c8670d4040c846c49db72c1095b4d147894dd903116ed3bfd67b1c5ba66569",
  "nk_expected.rds" = "3c486d65ac4ce70868f29e681c67df5709ce9bca1ca3c6aba924b6c17fca5168",
  "baseline-IREA.R" = "e388282049c237aa70c836da234bea0d1d5b7e472a2708778d9032639868a325"
)
files <- file.path(inputs, names(pinned))
actual_hash <- vapply(files, digest::digest, character(1), file = TRUE, algo = "sha256")
if (!identical(unname(actual_hash), unname(pinned))) stop("Pinned input checksum mismatch.")
fixture <- readRDS(file.path(inputs, "nk_expected.rds"))
stopifnot(identical(unname(tools::md5sum(files[[1]])), fixture$reference_md5))
check_r <- thisutils::check_r
log_message <- thisutils::log_message
namespace <- loadNamespace("scop", lib.loc = library_path)
PrepareDB <- getExportedValue("scop", "PrepareDB")
RunIREA <- getExportedValue("scop", "RunIREA")
irea_score_table <- get("irea_score_table", envir = namespace, inherits = FALSE)
checked_functions <- character()
for (file in source_files) {
  for (definition in parse(file.path(repo, file))) {
    if (!is.call(definition) || !identical(definition[[1]], as.name("<-")) ||
        !is.symbol(definition[[2]]) || !is.call(definition[[3]]) ||
        !identical(definition[[3]][[1]], as.name("function"))) next
    name <- as.character(definition[[2]])
    expected_function <- eval(definition[[3]])
    installed_function <- get(name, envir = namespace, inherits = FALSE)
    stopifnot(identical(formals(installed_function), formals(expected_function), ignore.srcref = TRUE),
      identical(body(installed_function), body(expected_function), ignore.srcref = TRUE))
    checked_functions <- c(checked_functions, name)
  }
}
reference <- PrepareDB(db = "IREA_NK_cell", species = "Mus_musculus",
  data_dir = inputs, verbose = FALSE)[["Mus_musculus"]][["IREA_NK_cell"]]
genes <- c("Ifitm3", "Isg15", "Ifit3", "Bst2", "Slfn5", "Isg20", "Phf11b", "Zbp1", "Rtp4")
stopifnot(identical(genes, fixture$genes))
expression <- SeuratObject::LayerData(reference$object, assay = "RNA", layer = "data")
stopifnot(all(genes %in% rownames(expression)))
score <- unname(Matrix::colSums(expression[genes, , drop = FALSE]))
meta <- reference$object@meta.data[colnames(expression), , drop = FALSE]
stopifnot(identical(as.character(meta$sample), fixture$sample),
  identical(as.character(meta$polarization), fixture$polarization))
score_max_error <- max(abs(score - fixture$score))
stopifnot(score_max_error <= 1e-12)
result <- RunIREA(genes, reference = reference, analysis = "cell_polarization", method = "score")
actual <- result$table
expected <- fixture$expected
stopifnot(!anyDuplicated(actual$term), !anyDuplicated(expected$Polarization),
  setequal(actual$term, expected$Polarization))
expected <- expected[match(actual$term, expected$Polarization), ]
old <- new.env(parent = globalenv())
sys.source(file.path(inputs, "baseline-IREA.R"), envir = old)
baseline_reference <- old$PrepareIREAReference(inputs, "NK_cell", "Mouse")
baseline <- old$RunIREA(baseline_reference, genes = genes, analysis = "cell_polarization", method = "score")$table
stopifnot(setequal(actual$term, baseline$term))
baseline <- baseline[match(actual$term, baseline$term), ]
comparison <- data.frame(term = actual$term,
  expected_effect = expected[["Enrichment Score"]], actual_effect = actual$effect,
  effect_abs_error = abs(actual$effect - expected[["Enrichment Score"]]),
  expected_p = expected$pval, actual_p = actual$p_value,
  p_relative_error = abs(actual$p_value / expected$pval - 1),
  expected_fdr = expected$padj, actual_fdr = actual$fdr,
  fdr_relative_error = abs(actual$fdr / expected$padj - 1),
  baseline_effect_delta = actual$effect - baseline$effect,
  baseline_p_delta = actual$p_value - baseline$p_value,
  baseline_fdr_delta = actual$fdr - baseline$fdr,
  n_target = actual$n_target, n_control = actual$n_control)
comparison$pass <- comparison$effect_abs_error <= 1e-8 &
  comparison$p_relative_error <= 1e-8 & comparison$fdr_relative_error <= 1e-8 &
  comparison$baseline_effect_delta == 0 & comparison$baseline_p_delta == 0 &
  comparison$baseline_fdr_delta == 0
wrong <- irea_score_table(score, list(group = fixture$polarization,
  terms = actual$term, baseline = which(fixture$polarization == "None")))
wrong_effect_error <- max(abs(wrong$effect - expected[["Enrichment Score"]]))
stopifnot(wrong_effect_error > 0.4)
write_full_csv <- function(x, file) {
  values <- lapply(x, function(v) if (is.numeric(v)) sprintf("%.17g", v) else v)
  utils::write.csv(as.data.frame(values, check.names = FALSE), file, row.names = FALSE)
}
write_full_csv(comparison, file.path(output, "comparison.csv"))
checksums <- data.frame(file = names(pinned), bytes = file.info(files)$size,
  md5 = unname(tools::md5sum(files)), sha256 = unname(actual_hash))
utils::write.csv(checksums, file.path(output, "input_checksums.csv"), row.names = FALSE)
writeLines(genes, file.path(output, "genes.txt"))
metadata <- list(commit = commit, baseline_commit = baseline_commit,
  executed_at_utc = format(Sys.time(), tz = "UTC", usetz = TRUE),
  elapsed_seconds = unname((proc.time() - started_at)[["elapsed"]]),
  execution = "independently installed package from the pinned checkout; installed R bodies and formals matched against pinned sources",
  installed_library = library_path, verified_source_functions = checked_functions,
  expected_source = "Archived portal rows from the historical public fixture; no new portal submission",
  portal_capture_date_documented = "2026-09-28",
  r_version = R.version.string,
  package_versions = as.list(stats::setNames(vapply(packages,
    function(p) as.character(utils::packageVersion(p)), character(1)), packages)),
  source_sha256 = as.list(stats::setNames(vapply(file.path(repo, source_files),
    digest::digest, character(1), file = TRUE, algo = "sha256"), source_files)),
  configuration = list(db = "IREA_NK_cell", species = "Mus_musculus", analysis = "cell_polarization",
    method = "score", assay = "RNA", layer = "data", baseline = "PBS", fdr_adjustment = "BH across four terms"),
  reference_cells = ncol(expression), reference_genes = nrow(expression), query_genes = genes,
  pbs_cells = sum(meta$sample == "PBS"), score_max_error = score_max_error,
  wrong_none_baseline_max_effect_error = wrong_effect_error,
  tolerances = list(effect_absolute = 1e-8, p_relative = 1e-8, fdr_relative = 1e-8),
  passed_rows = sum(comparison$pass), total_rows = nrow(comparison),
  max_effect_abs_error = max(comparison$effect_abs_error),
  max_p_relative_error = max(comparison$p_relative_error),
  max_fdr_relative_error = max(comparison$fdr_relative_error),
  baseline_numerical_values_identical = all(comparison[, c("baseline_effect_delta", "baseline_p_delta", "baseline_fdr_delta")] == 0),
  scope = "Only the mouse NK nine-gene score/polarization example; no full-mode equivalence claim")
jsonlite::write_json(metadata, file.path(output, "run_metadata.json"), pretty = TRUE,
  auto_unbox = TRUE, digits = NA)
writeLines(capture.output(sessionInfo()), file.path(output, "sessionInfo.txt"))
stopifnot(all(comparison$pass))
print(comparison)
cat("All four archived portal rows passed; numerical values match the pre-cleanup baseline exactly.\n")
```

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7027f11368f4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.