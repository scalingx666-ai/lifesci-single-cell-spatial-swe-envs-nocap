# Issue

**Title:** Have gr._utils._check_tuple_needles error message report correct string if invalid cluster name supplied

## Description

## Description
`squidpy.gr._ligrec._check_tuple_needles` has an error message when invalid cluster names are passed to it through `squidpy.gr._ligrec`, which reads ""Invalid cluster `<Bad Cluster>`.", but if the invalid one is the second object of the tuple, the error message will print the first object of the tuple. This fix should give the correct error message now.

## How has this been tested?
```
from itertools import product
clusters = list(map(str, adata_parent.obs["leiden_coarse"].cat.categories))
clusters.append("bad one")
clusters = list(product(clusters, repeat=2))  # type: ignore[no-redef,assignment]
clusters = sorted(
            sp.gr._ligrec._check_tuple_needles(
                clusters,  # type: ignore[arg-type]
                adata_parent.obs["leiden_coarse"].cat.categories,
                msg="Invalid cluster `{0!r}`.",
                reraise=True,
            )
        )
```
Before: ValueError: Invalid cluster `'APC'`. [ this is a real cluster in my data ]
After: ValueError: Invalid cluster `'bad one'`.

This is a re-submission of a previous one in "dev" brach, hopefully it will work this time.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1988b078994e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.