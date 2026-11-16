# Issue

**Title:** fix: moran's calculation parallelization

## Description

<!--
Thanks for opening a PR to scanpy!
Please be sure to follow the guidelines in our contribution guide (https://scanpy.readthedocs.io/en/latest/dev/index.html) to familiarize yourself with our workflow and speed up review.
-->

Was getting the following beginning with `numba>=0.66rc1`:

<details>
=================================== FAILURES ===================================
__________________ test_consistency[morans_i-single-threaded] __________________
[gw1] linux -- Python 3.14.5 /home/runner/.local/share/hatch/env/virtual/scanpy/B9PcT7QG/hatch-test.pre/bin/python3

metric = <function morans_i at 0x7fae9eda6140>

    @pytest.mark.usefixtures("_threading")
    def test_consistency(metric) -> None:
        pbmc = pbmc68k_reduced()
        pbmc.layers["raw"] = pbmc.raw.X.copy()
        g = pbmc.obsp["connectivities"]
        equality_check = partial(np.testing.assert_allclose, atol=1e-11)
    
        # This can fail
        equality_check(
            metric(g, pbmc.obs["percent_mito"]),
            metric(g, pbmc.obs["percent_mito"]),
        )
        equality_check(
            metric(g, pbmc.obs["percent_mito"]),
            metric(pbmc, vals=pbmc.obs["percent_mito"]),
        )
    
        equality_check(  # Test that series and vectors return same value
            metric(g, pbmc.obs["percent_mito"]),
            metric(g, pbmc.obs["percent_mito"].values),
        )
    
        equality_check(
            metric(pbmc, obsm="X_pca"),
            metric(g, pbmc.obsm["X_pca"].T),
        )
    
        all_genes = metric(pbmc, layer="raw")
        first_gene = metric(
            pbmc, vals=pbmc[:, pbmc.var_names[0]].layers["raw"].toarray().ravel()
        )
    
>       np.testing.assert_allclose(all_genes[0], first_gene, rtol=1e-9)
E       AssertionError: 
E       Not equal to tolerance rtol=1e-09, atol=0
E       
E       Mismatched elements: 1 / 1 (100%)
E       Max absolute difference among violations: 7.9750179849e-08
E       Max relative difference among violations: 1.8702209022e-07
E        ACTUAL: array(0.426421)
E        DESIRED: array(0.426421)

tests/test_metrics.py:72: AssertionError
__________________ test_consistency[morans_i-multi-threaded] ___________________
[gw1] linux -- Python 3.14.5 /home/runner/.local/share/hatch/env/virtual/scanpy/B9PcT7QG/hatch-test.pre/bin/python3
    data[i] -= regressor[i] @ coeff

tests/test_scaling.py::test_scale[mask-center-int64-array-csc_matrix]
tests/test_scaling.py::test_scale[mask-center-int64-anndata-csc_matrix]
tests/test_scaling.py::test_scale[mask-center-float32-anndata-csc_matrix]
tests/test_scaling.py::test_scale[mask-center-float32-array-csc_matrix]
  /home/runner/.local/share/hatch/env/virtual/scanpy/B9PcT7QG/hatch-test.pre/lib/python3.14/site-packages/scipy/sparse/_index.py:216: SparseEfficiencyWarning: Changing the sparsity structure of a csc_matrix is expensive. lil and dok are more efficient.
    self._set_arrayXarray(i, j, x)

tests/test_scaling.py::test_scale[mask-center-int64-anndata-csr_matrix]
tests/test_scaling.py::test_scale[mask-center-float32-array-csr_matrix]
tests/test_scaling.py::test_scale[mask-center-float32-anndata-csr_matrix]
tests/test_scaling.py::test_scale[mask-center-int64-array-csr_matrix]
  /home/runner/.local/share/hatch/env/virtual/scanpy/B9PcT7QG/hatch-test.pre/lib/python3.14/site-packages/scipy/sparse/_index.py:216: SparseEfficiencyWarning: Changing the sparsity structure of a csr_matrix is expensive. lil and dok are more efficient.
    self._set_arrayXarray(i, j, x)

-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html
- generated xml file: /home/runner/work/scanpy/scanpy/test-data/test-results.xml -
=========================== short test summary info ============================
FAILED tests/test_metrics.py::test_consistency[morans_i-single-threaded] - AssertionError: 
Not equal to tolerance rtol=1e-09, atol=0

Mismatched elements: 1 / 1 (100%)
Max absolute difference among violations: 7.9750179849e-08
Max relative difference among violations: 1.8702209022e-07
 ACTUAL: array(0.426421)
 DESIRED: array(0.426421)
FAILED tests/test_metrics.py::test_consistency[morans_i-multi-threaded] - AssertionError: 
Not equal to tolerance rtol=1e-09, atol=0

Mismatched elements: 1 / 1 (100%)
Max absolute difference among violations: 7.9750179849e-08
Max relative difference among violations: 1.8702209022e-07
 ACTUAL: array(0.426421)
 DESIRED: array(0.426421)
</details>

and suspect this could be the cause

<!-- Please check (“- [x]”) and fill in the following boxes -->
- [ ] Closes #
- [ ] [Tests][] included or not required because:
<!-- Only check the following box if you did not include release notes -->
- [x] [Release notes][] not necessary because: fix in preparation for upcoming release

[tests]: https://scanpy.readthedocs.io/en/stable/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/en/stable/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d66537fba529`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.