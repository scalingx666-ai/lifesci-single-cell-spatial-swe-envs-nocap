# Issue

**Title:** Made relative imports explicit for python3 compatibility

## Description

Hey. I liked your preprint!

Just a quick bug fix, I'm trying to test out the package, but ran into errors on import:

```python3
In [1]: from scanorama import correct
---------------------------------------------------------------------------
ModuleNotFoundError                       Traceback (most recent call last)
<ipython-input-1-093a6fa274ef> in <module>()
----> 1 from scanorama import correct

/usr/local/lib/python3.6/site-packages/scanorama/__init__.py in <module>()
----> 1 from .scanorama import *

/usr/local/lib/python3.6/site-packages/scanorama/scanorama.py in <module>()
     11 import sys
     12 
---> 13 from t_sne_approx import TSNEApprox
     14 from utils import plt, dispersion, reduce_dimensionality
     15 from utils import visualize_cluster, visualize_expr

ModuleNotFoundError: No module named 't_sne_approx'
```

Looked like the issue was python3 [requiring explicit relative imports](https://docs.python.org/3/tutorial/modules.html#intra-package-references), so I changed that and now can run the examples.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f6489723caf8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.