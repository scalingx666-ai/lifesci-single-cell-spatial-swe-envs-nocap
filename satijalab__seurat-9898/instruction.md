# Issue

**Title:** Add arguments to kmeans call in BuildNicheAssay function

## Description

### Summary

This PR adds support for passing additional arguments to the `kmeans` function within `BuildNicheAssay`. The goal is to help address convergence issues such as the warning:

```
Warning: did not converge in 10 iterations
```

In some cases, the default settings of `kmeans` may not be sufficient for convergence, particularly with complex or noisy datasets. By allowing users to specify parameters like `iter.max`, `nstart`, and `algorithm`, the clustering behavior can be tuned for better performance.

With the added flexibility, I was able to resolve the convergence warning using the following code:

```r
set.seed(1)
xobj <- BuildNicheAssay(
    xobj,
    fov = "fov",
    group.by = "cell_type_res_l2",
    niches.k = 10, neighbors.k = 10,
    algorithm = "Lloyd", iter.max = 1000, 
    nstart = 1
)
```

Addresses #9543

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9ec4b2cc3f7b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.