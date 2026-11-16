# Issue

**Title:** Fix `cell_transition` bug

## Description

Hi @MUCDK ,

Related  This used to give an error but now it doesn't
```python
import pandas as pd

adata_sc = datasets.drosophila(spatial=False)
adata_sp = datasets.drosophila(spatial=True)
adata_sc, adata_sp

if "test_col_1" in adata_sp.obs:
    del adata_sp.obs["test_col_1"]
if "test_col_2" in adata_sc.obs:
    del adata_sc.obs["test_col_2"]
if "test_col_1" in adata_sc.obs:
    del adata_sc.obs["test_col_1"]
if "test_col_2" in adata_sp.obs:
    del adata_sp.obs["test_col_2"]

adata_sc.obs["test_col_2"] = pd.Categorical(np.random.choice(["a", "b"], size=len(adata_sc)))
adata_sp.obs["test_col_1"] = pd.Categorical(np.random.choice(["a", "b"], size=len(adata_sp)))

mp = MappingProblem(adata_sc, adata_sp)
mp = mp.prepare(
    sc_attr={"attr": "obsm", "key": "X_pca"}, xy_callback="local-pca"
).solve(epsilon=10.0)


mp.cell_transition("src", "tgt", 
                   "test_col_1", "test_col_2")

```

I just separated the key used for storing the result and the key to push/pull.

I have some extra notes on function for future refactoring though:
- `other_keys` is always None from what I understand.
- Instead of a separate argument for cell aggregation I think user can just set `source_groups=None`.  (I am still not sure about this I am reading the code more atm)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c981a05af55c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.