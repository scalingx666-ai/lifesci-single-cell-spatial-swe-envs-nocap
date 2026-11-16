# Issue

**Title:** Allow name access to multiple embeddings in conclass

## Description

Related to this issue: 

* stores multiple embeddings in a list, allowing users to access them by name. 

> What would be the expected behavior for multiple embeddings? For instance, if you run plotGraph(), would it use the latest embedding? The first one? Should the current $embedding slot be updated with the latest calculated embedding?

I believe this is implemented so that if the name provided is `NULL`, then `plotPanel()` and `plotGraph()` will access the last-added embedding. 

I haven't tried this yet, so there could be issues. Have a look :)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `61524c0f78d5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.