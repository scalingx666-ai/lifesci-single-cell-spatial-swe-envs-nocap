# Issue

**Title:** use rustworkx instead of networkx except the plotting

## Description

This is part of my larger goal to replace process based parallelization. I found rustworkx easy to install and fast. That's why I made a PR long ago.

This pull request migrates the group centrality computation in `centrality_scores` from NetworkX to the high-performance `rustworkx` library, and introduces a custom, Numba-accelerated clustering coefficient kernel. It also ensures that the results remain numerically consistent with the previous implementation by adding parity tests. The main changes are as follows:

**Dependency and Documentation Updates:**
* Added `rustworkx>=0.18.0` as a dependency in `pyproject.toml` and included a corresponding citation in `references.bib`. [[1]](diffhunk://#diff-50c86b7ed8ac2cf95bd48334961bf0530cdc77b5a56f852c5c61b89d735fd711R67) [[2]](diffhunk://#diff-9e696d253e1559081cbc14060ab857b33b9c7847a6b6a572f1e473d479718500R43-R53)
* Updated docstrings to reference `rustworkx` for group centrality measures and clarified citations for both `rustworkx` and `networkx`. [[1]](diffhunk://#diff-b0f880b8a8accb2572d8e7c94512c48a8ebc1d2b47c43542eefc3762525f4d31L269-R270) [[2]](diffhunk://#diff-672a2b0857d1d2167dc6f22d1bfe7c4c37229cf26d603ab41631d5f80b79b75aL216-R216)

**Core Implementation Changes:**
* Replaced NetworkX-based group centrality calculations in `centrality_scores` with `rustworkx` equivalents, and replaced the clustering coefficient computation with a custom, parallelized Numba kernel for improved performance. [[1]](diffhunk://#diff-b0f880b8a8accb2572d8e7c94512c48a8ebc1d2b47c43542eefc3762525f4d31L299-R316) [[2]](diffhunk://#diff-b0f880b8a8accb2572d8e7c94512c48a8ebc1d2b47c43542eefc3762525f4d31R432-R493)
* Added a new `_build_graph` utility to convert connectivity matrices into both `rustworkx.PyGraph` and a CSR matrix for use in centrality and clustering calculations.

**Testing:**
* Introduced a test to verify numerical parity between the new `rustworkx`/Numba implementation and the original NetworkX-based results for all group centrality measures.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ca07e649344d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.