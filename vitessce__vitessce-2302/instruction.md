# Issue

**Title:** feat #2233: add SpatialDataFeatureLabelsLoader and integrate into file types

## Description

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->

<!-- For other PRs without open issue -->
#### Background
Spatialdata zarr stores do not currently support custom feature labels; this PR adds the appropriate loaders and additional logic necessary to support feature labels with the same schema used for anndata zarr stores.

#### Tested by
* Downloading the secondary_analysis.h5ad of this HuBMAP dataset https://portal.hubmapconsortium.org/browse/dataset/2817f3c327f632e70f8c7581265a4aba?redirected=True&redirectedFromId=HBM842.SQSV.255&redirectedFromPipeline=Salmon#section-salmon-published
* Copying the ensg-based index to a second column ("ensg_id") with `extra` appended to every value (to work around the automatic ENSG->HUGO remapping functionality)
* Creating a spatialdata zarr store with the resulting anndata file as its only table and serving it via `npx http-server --cors='*' --port 8000 .`
* Adjusting the view config from the HuBMAP dataset to use spatialdata file types/prefixes where necessary
* Loading the resulting config in the Vitessce docs' App view
* Confirming the resulting gene list uses the modified ENSG values

<img width="478" height="2019" alt="image" src="https://github.com/user-attachments/assets/3ccf9725-3cbb-45fe-a5de-48eba8bf218f" />


#### Change List
- Added support for featureLabels in SpatialData file configurations.
#### Checklist
 - [x] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d430998f79da`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.