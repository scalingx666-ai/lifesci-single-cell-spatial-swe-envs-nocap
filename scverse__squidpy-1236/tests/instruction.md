# Issue

**Title:** Fix 870: Significant memory and runtime improvements for Ripley's L

## Description

## Description

<!-- Clearly and concisely describe your changes. This section will be shown in the docs. -->

Headline number: at 250,000 cells in a single cluster, memory usage drops from **~1.8tb to 0.2gb**, and runtime drops from probably something like 40 minutes (extrapolated because I don't have 1.8tb of ram lol) to **6 minutes** on a GCP `n2-highmem-8`.

**Peak memory**

| n (cells) | `main` (pdist) | `branch` (KDTree) | reduction |
| --------: | -------------: | ----------------: | --------: |
| 20,000    | 11.5 GB        | 0.13 GB           | ~90x      |
| 30,000    | 25.6 GB        | 0.13 GB           | ~200x     |
| 40,000    | 45.4 GB        | 0.13 GB           | ~350x     |
| 100,000   | ~290 GB*       | 0.13 GB           | ~2,200x   |
| 250,000   | ~1.8 TB*       | 0.14 GB           | ~13,000x  |
| 500,000   | ~7.2 TB*       | 0.15 GB           | ~50,000x  |

**Runtime**

| n (cells) | `main` (pdist) | `branch` (KDTree) | speedup |
| --------: | -------------: | ----------------: | ------: |
| 20,000    | 15.5 s         | 5.7 s             | 2.7x    |
| 30,000    | 34.0 s         | 10.8 s            | 3.2x    |
| 40,000    | 60.1 s         | 19.2 s            | 3.1x    |
| 100,000   | ~6.4 min*      | 77.5 s            | ~5x     |
| 250,000   | ~40 min*       | 6.0 min           | ~7x     |
| 500,000   | ~2.7 hr*       | 20.8 min          | ~8x     |

(* for Claude extrapolated because the process OOMed on main)

Previously, ripley's L calculation materialized O(n^2) pairwise distances (via `pdist`) and then broadcast that across the number of steps in `support`. In issue #870, at 250,000 cells, this is `n * (n - 1) / 2 = 31,249,875,000` unordered pairs, multiplied by 50 steps means `distances < support.reshape(-1, 1)` would be a 2D bool array of `50 * 31,249,875,000` bytes, so roughly **1.5tb of memory** (excluding the `pdist` intermediate, which would still exist and add another ~250gb on top of that), assuming all cells are in the same cluster. This would OOM on pretty much any reasonable hardware.

Fortunately, we can skip all of that by using a [KDTree](https://en.wikipedia.org/wiki/K-d_tree). Long story short once we build the binary tree once, using O(n) memory, and then [two_point_correlation](https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KDTree.html#sklearn.neighbors.KDTree.two_point_correlation) traverses this structure to find the number of points within each radius without materializing every pairwise distance. This gives us O(n) memory usage instead of O(n^2).

One thing to note: this narrows the list of valid metrics down to:

```
>>> KDTree.valid_metrics
['euclidean', 'l2', 'minkowski', 'p', 'manhattan', 'cityblock', 'l1', 'chebyshev', 'infinity']
```

whereas previously `pdist` would have accepted any of

```
[‘braycurtis’, ‘canberra’, ‘chebyshev’, ‘cityblock’, ‘correlation’, ‘cosine’, ‘dice’, ‘euclidean’, ‘hamming’, ‘jaccard’, ‘jensenshannon’, ‘mahalanobis’, ‘matching’, ‘minkowski’, ‘rogerstanimoto’, ‘russellrao’, ‘seuclidean’, ‘sokalsneath’, ‘sqeuclidean’, ‘yule’]
```

but I don't think any of the dropped ones were valid / sensical metrics for the kind of spatial stats that are happening here.

## How has this been tested?

<!-- Describe in detail how you've tested your changes. -->

- Running existing tests
- Extensive benchmarking (both memory and runtime) across various problem sizes while verifying correctness against`main`.

## Closes

closes 

<!-- If applicable, type `closes #XXXX` in your comment to auto-close the issue that this PR fixes. -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `69a2b12749f7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.