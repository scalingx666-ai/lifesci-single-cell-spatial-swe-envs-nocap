# Issue

**Title:** Relocate gene names to the main thread.

## Description

Handles the second point in #27.

The main change is that the main thread primarily operates with the matrix row indexes (`.row`). This contains the index to the row in the count/normalized/filtered matrix. (Doesn't matter which, as the rows are the same for all of them.) You don't have to worry about the permutations - that's strictly a worker-side problem.

Turned `selectedClusterSummary` into an array, to avoid issues with ordering when trying to store numeric keys in a map. As a result, each entry also has an `index` entry that refers to the index of itself in the full ordered array. This is needed in case filtering is done and you need some way to refer back to the original array. Don't confuse `.index` with `.row`; the former refers to the  _sorted array index_ while the latter refers to the _matrix row index_. 

`reqGene` and `gene` need to be renamed to something a bit more explicit. Currently we store `.row` in `reqGene` (i.e., the row of the matrix on the worker side), while we store `.index` in `gene` (i.e., the index in the `selectedClusterSummary` array on the main thread's side).

Also had to put in a few minor fixes here and there to account for the fact that a gene of zero evaluates to false, so the first gene's expression wasn't being plotted before I figured it out.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a92e088d620`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.