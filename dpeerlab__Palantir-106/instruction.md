# Issue

**Title:** Palantir v1.2

## Description

This covers multiple changes @ManuSetty and I wrote up in preparation of our cell-state density manuscript.

 ### Version 1.2.0

 #### New Features
 * Enable an AnnData-centric workflow for improved usability and interoperability with other single-cell analysis tools.
 * Introduced new utility functions
     * `palantir.utils.early_cell` To automate fining an early cell based on cell type and diffusion components.
     * `palantir.utils.find_terminal_states` To automate finding terminal cell states based on cell type and diffusion components.
     * `palantir.presults.select_branch_cells` To find cells associated to each branch based on fate probability.
     * `palantir.plot.plot_branch_selection` To inspect the cell to branch association.
     * `palantir.utils.run_local_variability` To compute local gene expression variability.
     * `palantir.utils.run_density` A wrapper for [mellon.DensityEstimator](https://mellon.readthedocs.io/en/latest/model.html#mellon.model.DensityEstimator).
     * `palantir.utils.run_low_density_variability`. To aggregate local gene expression variability in low density.
 * Added input validation for better error handling and improved user experience.
 * Expanded documentation within docstrings, providing additional clarity for users and developers.

 #### Enhancements
 * Updated tutorial notebook to reflect the new workflow, guiding users through the updated processes.
 * Implemented gene trend computation using [Mellon](https://github.com/settylab/Mellon), providing more robust and efficient gene trend analysis.

 #### Changes
 * Replaced PhenoGraph dependency with `scanpy.tl.leiden` for gene trend clustering.
 * Deprecated the `run_tsne`, `determine_cell_clusters`, and `plot_cell_clusters` functions. Use corresponding implementations from [Scanpy](https://scanpy.readthedocs.io/en/stable/), widely used single-cell analysis library and direct dependecy of Palantir.

 #### Fixes
 * Addressed the issue of variability when reproducing results (), enhancing the reproducibility and reliability of Palantir.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d4f9fcdbfeb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.