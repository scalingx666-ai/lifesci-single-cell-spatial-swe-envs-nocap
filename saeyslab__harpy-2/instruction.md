# Issue

**Title:** SC_2 preprocessing update proteomics

## Description

- refactor preprocessing functions (`sp.tb.preprocess_proteomics` and `sp.tb.preprocess_transcriptomics`)
- workflow as follows:
```
from sparrow.table._clustering import leiden
from sparrow.table._preprocess import preprocess_proteomics
sdata_multi_c = preprocess_proteomics(sdata_multi_c, labels_layer="masks_whole")
sdata_multi_c = leiden(sdata_multi_c, labels_layer="masks_whole", key_added="leiden", random_state=100)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `28a730c7fd4b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.