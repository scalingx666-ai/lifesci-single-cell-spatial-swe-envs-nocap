# Issue

**Title:** feat(preprocessing): add optimal shifted CLR (PFlog) normalization

## Description

<!-- Please check (“- [x]”) and fill in the following boxes -->
- [ ] Closes #
- [x] [Tests][] included or not required because: 34 comprehensive parametrized unit tests covering memory layouts, alpha calibration, and zero-depth guards have been appended to `tests/test_normalization.py`.
- [ ] [Release notes][] not necessary because: (A release note fragment has been provided).

[tests]: https://scanpy.readthedocs.io/en/stable/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/en/stable/dev/documentation.html#adding-to-the-docs

---

### Summary & Paper Context

This PR introduces `sc.pp.normalize_clr` to implement the optimal shifted Centered Log-Ratio transform.

* **Reference Publication:** This implementation is based directly on the paper *"Depth normalization for single-cell genomics count data"* (Booeshaghi et al., 2022, 2026).
* **bioRxiv Link:** [https://www.biorxiv.org/content/10.1101/2022.05.06.490859v3](https://www.biorxiv.org/content/10.1101/2022.05.06.490859v3)
* **Code Attribution:** The core mathematical processing engine and memory-saving array optimizations are adapted directly from the Pachter Lab reference repository: [https://github.com/pachterlab/bhgp_2022](https://github.com/pachterlab/bhgp_2022)

The paper demonstrates that the shifted CLR (conceptually known as the $\text{PFlog1pPF}$ family) satisfies four essential preprocessing criteria, unlike most other common normalization methods:

* **Variance Stabilization:** Balances gene variance independent of expression magnitude.
* **Scale (Sequencing Depth) Invariance:** Erases technical read-depth variations across cells, preventing cells from clustering based on library size.
* **Strict Rank Monotonicity:** Preserves the exact relative abundance rankings of genes within a cell, avoiding the artifacts introduced by regression-based methods like `sctransform`.
* **Perturbation Additivity:** Fully compatible with linear downstream dimensionality reduction (PCA) because changes act additively in log-space.

See publication for extensive validation benchmarks across hundreds of datasets.

---

### Implementation Details & Files Changed

1. **`src/scanpy/preprocessing/_normalization.py`**
   * Implemented the public `normalize_clr` function and a private `_normalize_clr_helper` backend engine.
   * Utilizes the author's **sparse "offset trick"** to isolate log operations exclusively to non-zero indices, preventing premature matrix densification and keeping memory usage minimal.
   * Supports negative-binomial overdispersion (`alpha`) data overrides to automatically calibrate target scale factors via the delta method.
2. **`src/scanpy/preprocessing/__init__.py`**
   * Registered `normalize_clr` inside the preprocessing namespace and appended it to the global `__all__` list.
3. **`docs/references.bib`**
   * Appended the cleaned, structured, and properly aligned `Booeshaghi2022` BibTeX entry.
4. **`docs/api/preprocessing.md`**
   * Registered the function for inclusion in the Sphinx-generated documentation summary table.
5. **`docs/release-notes/4160.feat.md`**
   * Created the required markdown fragment documenting this change for the next release.
6. **`tests/test_normalization.py`**
   * Added 9 test functions (yielding 34 parametrized cases) evaluating standard in-memory arrays (`ARRAY_TYPES_MEM`) for sparse-dense equivalence, delta-method overrides, empty cell handling, and hyperplane invariants.
6. **`tests/test_package_structure.py`**
   * Registered `sc.pp.normalize_clr` into the `copy_sigs` chained assignment exemption list. This explicitly informs the global `test_sig_conventions` runner that the function is permitted to return a `dict[str, np.ndarray]` when `inplace=False`, resolving the administrative signature enforcement failure.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `17f25cd52357`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.