# Issue

**Title:** Speed up anndata writing speed after define_clonotype_clusters

## Description

The writing speed of the anndata object after the define_clonotype_clusters function is too slow which is currently one of the biggest bottlenecks in scirpy's analysis pipeline. The reason for that is the clonotype_id -> cell_ids mapping (dict[str, np.ndarray[str]) that gets stored to the anndata.uns attribute. Now I implemented a version where this mapping has the datatype dict[str, list[str]) and gets converted to a json object before storing it. This is quite fast and is very similar to the previous implementation such that only minor changes in the rest of the code were necessary.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `339609d9bcb2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.