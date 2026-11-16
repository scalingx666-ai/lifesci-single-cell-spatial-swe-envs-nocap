# Issue

**Title:** NickAkhmetov/Add support for zipped genomic profiles Zarr stores

## Description

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->
Fixes ##2482

<!-- For other PRs without open issue -->
#### Background

The zarr stores powering the genomic profile view are not currently possible to zip up due to the necessary constants/mappings not being defined. This PR adds the necessary mappings to enable using zipped genomic profile zarr stores.

#### Change List
- Added `GENOMIC_PROFILES_ZARR_ZIP` constant, corresponding relationship in `constant-relationships`, and plugin.

#### Checklist
 - [x] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `00ae354607af`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.