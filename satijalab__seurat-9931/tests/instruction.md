# Issue

**Title:** Add option to use igraph for leiden clustering

## Description

Hi Seurat Team,

This is PR following up on issue #9800 that I posted.  This PR contains:  
- Update to `RunLeiden` to support use of igraph `cluster_leiden`.  
- Updates `FindClusters.default` & `FindClustres.Seurat` to allow passing of `leiden_method` parameter (default remains leidenbase for now as suggested by @rsatija )  
- Adds two internal utility functions from BPCells `get_seed` and `restore_seed` so that seed can be appropriately set for igraph leiden and then restored to environment seed prior to running function.


If you have any questions or additional changes need please let me know!
Best,
Sam

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9051ad473116`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.