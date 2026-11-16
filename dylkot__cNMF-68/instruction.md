# Issue

**Title:** Raise error if zero components meet density threshold

## Description

If density_threshold is too low, a very confusing error is raised:

```
Traceback (most recent call last):
  File "/Users/scottgigante/envs/immunaISR/lib/python3.8/site-packages/sklearn/utils/_param_validation.py", line 192, in wrapper
    return func(*args, **kwargs)
  File "/Users/scottgigante/envs/immunaISR/lib/python3.8/site-packages/sklearn/decomposition/_nmf.py", line 1106, in non_negative_factorization
    est._validate_params()
  File "/Users/scottgigante/envs/immunaISR/lib/python3.8/site-packages/sklearn/base.py", line 600, in _validate_params
    validate_parameter_constraints(
  File "/Users/scottgigante/envs/immunaISR/lib/python3.8/site-packages/sklearn/utils/_param_validation.py", line 97, in validate_parameter_constraints
    raise InvalidParameterError(
sklearn.utils._param_validation.InvalidParameterError: The 'n_components' parameter of NMF must be an int in the range [1, inf) or None. Got 0 instead.

The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "/Users/scottgigante/envs/immunaISR/lib/python3.8/site-packages/cnmf/cnmf.py", line 739, in consensus
    rf_usages = self.refit_usage(norm_counts.X, median_spectra)
  File "/Users/scottgigante/envs/immunaISR/lib/python3.8/site-packages/cnmf/cnmf.py", line 658, in refit_usage
    _, rf_usages = self._nmf(X, nmf_kwargs=refit_nmf_kwargs)
  File "/Users/scottgigante/envs/immunaISR/lib/python3.8/site-packages/cnmf/cnmf.py", line 551, in _nmf
    (usages, spectra, niter) = non_negative_factorization(X, **nmf_kwargs)
  File "/Users/scottgigante/envs/immunaISR/lib/python3.8/site-packages/sklearn/utils/_param_validation.py", line 203, in wrapper
    raise InvalidParameterError(msg) from e
sklearn.utils._param_validation.InvalidParameterError: The 'n_components' parameter of non_negative_factorization must be an int in the range [1, inf) or None. Got 0 instead.
```

This PR makes the error more comprehensible.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f04db6bc797d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.