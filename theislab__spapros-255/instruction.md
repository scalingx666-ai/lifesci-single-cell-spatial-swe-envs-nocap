# Issue

**Title:** Metaclass bug

## Description

Redoing PR #254 now first into dev to trigger github actions when merging with main - oups.
 
**Description of changes**

- Adjusted class `_AxesSubplot` to fix metaclass issue #253 
(related: see scverse/scanpy#2414 fixed scverse/scanpy#2411)

**Relevant code snippets**

1.  `import spapros as sp` works again.  

2.   
```python
import spapros as sp
adata = sp.ut.get_processed_pbmc_data()
selector = sp.se.ProbesetSelector(adata, "celltype", n=30, verbosity=0)
selector.select_probeset()

sp.pl.masked_dotplot(adata,selector)
```
is not affected.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b61721007d9f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.