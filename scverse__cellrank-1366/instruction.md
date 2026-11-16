# Issue

**Title:** Fix Lineage.__repr__

## Description

## Changes
<!-- Clearly and concisely describe your changesremove this section if this PR does not implement any changes -->

* Updated `Lineage.__repr__`

Now

```py
import numpy as np
from cellrank import Lineage

L = Lineage(
    np.array([[0.6, 0.4], [0.3, 0.7], [0.9, 0.1]]),
    names=["foo", "bar"],
    colors=["#ff0000", "#0000ff"],
)

print(L)
```

yields
```
[[0.6 0.4]
 [0.3 0.7]
 [0.9 0.1]]
 names=[foo, bar]
```
## Bug fixes
<!-- Clearly and concisely describe your bug fixes; remove this section if this PR does not implement any bug fixes -->

*

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `34c2f43b7d9d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.