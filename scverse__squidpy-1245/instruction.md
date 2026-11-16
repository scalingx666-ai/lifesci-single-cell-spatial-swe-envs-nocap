# Issue

**Title:** Initial framework of the niche refactor

## Description

## Description
Niche refactor improving the current implementation giving the user facing functions a more explicit API, more flexibility through embedder and clusterer classes and possibility of using combinations of them using `calculate_niche_custom`. Postprocessor classes allow more organized and flexible postprocessing actions like masking and min_niche_size filtering of niches.
The core idea is similar to the spatial_neighbors refactor in #1147 and builds on top of the relatively smaller fix in #1229. 

The below graph demonstrates the code flow planned (read children of a node from left to right). This allows usage of different combinations of embeddings and clusterings to obtain niches, and also exposing easy to use and explicit user facing functions for the different flavors. Brown nodes are user-facing functions.
<img width="1646" height="843" alt="Screenshot 2026-07-21 at 1 50 05 AM" src="https://github.com/user-attachments/assets/ba5cfb5b-641b-4fe7-9973-69c7c1bba499" />


## How has this been tested?
Keeping the API of function `calculate_niche` same, for i) backward compatibility and ii) being able to validate results being same before and after refactor for some test cases that I wrote for the purpose of this refactor, for the different flavors. Though later on, I think `calculate_niche` should be deprecated as its not clear how arguments of it interact with different values of `flavor` argument.

## Closes
, where this was initially discussed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0bc86926a095`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.