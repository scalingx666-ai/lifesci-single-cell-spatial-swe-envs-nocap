# Issue

**Title:** feat: add networkit flavor for parallel Leiden clustering

## Description

This PR adds NetworKit's ParallelLeiden as a new flavor option for `scanpy.tl.leiden`, enabling multithreaded Leiden community detection via `scanpy.tl.leiden(adata, flavor="networkit")`. The motivation behind is that scanpy's current Leiden backends (igraph, leidenalg) are single-threaded. For atlas-scale datasets (500k+ cells), clustering becomes a bottleneck. NetworKit's ParallelLeiden is a C++ parallel implementation available via pip with no additional compilation, making it the lowest-friction path to parallel Leiden in scanpy.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `707fe784ff0c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.