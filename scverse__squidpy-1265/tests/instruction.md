# Issue

**Title:** fix: avoid obs_vector FutureWarning in spatial_scatter

## Description

anndata >=0.13 deprecates `AnnData.obs_vector`, which `_set_color_source_vec` calls on every `spatial_scatter` coloring by an obs column or gene, surfacing a `FutureWarning` to users.

Route both lookups through a `get_vector` shim that delegates to `scanpy.get.obs_df` (already a dependency), preserving the original `use_raw`/`layer` precedence and `Categorical` dtype.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4344d165d6bf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.