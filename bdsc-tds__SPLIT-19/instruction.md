# Issue

**Title:** Add `reconstruct_rctd_from_rctdpy()`: rctd-py parquet -> RCTD S4 bridge

## Description

### Summary
Adds a new function that reads the parquet/HDF5 output produced by the Python `rctd-py` package and assembles a `spacexr` S4 `RCTD` object compatible with `run_post_process_RCTD(lite = TRUE)`, enabling users who run RCTD in Python to use the full SPLIT post-processing pipeline.

### Changes
- **`R/reconstruct_rctd_from_rctdpy.R`** — new exported function with full roxygen2 documentation, including an embedded Python snippet showing exactly how to save `rctd-py` output for compatibility
- **`DESCRIPTION`** — version bump `0.2.0 → 0.2.1`; added `arrow` and `rhdf5` to `Imports`

### Details
The function handles the following format differences between rctd-py and spacexr:
- `spot_class` integer codes (0–3) are mapped to spacexr factor levels (`reject`, `singlet`, `doublet_certain`, `doublet_uncertain`)
- `weights_doublet` columns are renamed from `w_1`/`w_2` to `first_type`/`second_type`
- Reference profiles are transposed from cell_types × genes (Python) to genes × cell_types (R)
- A minimal `SpatialRNA` placeholder is constructed so `lite = TRUE` post-processing works without raw counts
- `internal_vars$class_df` defaults to an identity mapping (each cell type maps to itself); a custom mapping can be supplied via the `class_df` argument

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d5bc38890672`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.