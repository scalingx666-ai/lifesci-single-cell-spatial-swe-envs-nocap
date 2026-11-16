# Issue

**Title:** feature/Pre-initialize zip stores and pass them in to data loaders

## Description

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->

#### Background

This PR updates loader initialization to initialize zip-zarr stores at the top level and merges them into the `stores` prop. On config changes, the cache evicts irrelevant stores.

I've verified the impact of this change by running the same spatialdata visium config through my local instance and through vitessce.io and using Firefox dev tools to measure total time.

* On `localhost`, the conf loaded in ~27 seconds across 5 runs
* On `vitessce.io`, the conf loaded in ~30 seconds across 5 runs
* All runs were performed with caching disabled in the browser

#### Change List
- Added pre-initialization logic for zip-zarr stores to improve loading times.
#### Checklist
 - [x] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable

Not opening this for final review yet since I'd like to update the original issue etc to reflect these findings.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `78cc6775267b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.