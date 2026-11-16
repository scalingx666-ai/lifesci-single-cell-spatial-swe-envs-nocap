# Issue

**Title:** Fix overly broad conversion of warnings to errors

## Description

This avoids the following warning being converted to an error with recent versions of scikit-learn:

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "site-packages/scanpy/external/pp/_scanorama_integrate.py", line 121, in scanorama_integrate
    integrated = scanorama.assemble(
  File "site-packages/scanorama/scanorama.py", line 933, in assemble
    bias = transform(curr_ds, curr_ref, ds_ind, ref_ind, sigma=sigma,
  File "site-packages/scanorama/scanorama.py", line 762, in transform
    avg_bias = batch_bias(curr_ds, match_ds, bias, sigma=sigma,
  File "site-packages/scanorama/scanorama.py", line 723, in batch_bias
    weights = rbf_kernel(curr_ds, match_ds, gamma=0.5*sigma)
  File "site-packages/sklearn/metrics/pairwise.py", line 1294, in rbf_kernel
    X, Y = check_pairwise_arrays(X, Y)
  File "site-packages/sklearn/metrics/pairwise.py", line 155, in check_pairwise_arrays
    X = check_array(
  File "site-packages/sklearn/utils/validation.py", line 727, in check_array
    warnings.warn(
FutureWarning: np.matrix usage is deprecated in 1.0 and will raise a TypeError in 1.2. Please convert to a numpy array with np.asarray. For more information see: https://numpy.org/doc/stable/reference/generated/numpy.matrix.html

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2def73093ee8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.