# Issue

**Title:** PR into support on demand mesh loading branch

## Description

This PR contains changes for the support on demand mesh loading branch in #2470

Since we already have `geneSelection` which colors cells using a quantitative colormap, I think it is best if we reuse this, and for the points, infer whether it means to use a categorical colormap (when each point represents a transcript) vs. a quantitative colormap (when points are segmentation centroids) based on checking for a match between the point and segmentation `obsType` values. I also removed the `useForSegmentationCulling` option, replacing it with the same `obsType` matching logic.

The main remaining question I have is regarding `quantitativeColorProp` and `quantitativeColorMax`. If the quantitative values correspond to gene expression quantities, then we do not want to hard-code a single gene and its maximum value in the config. Instead, can we make assumptions about how the data has been normalized and about the `prop_something()` naming conventions (e.g., how the `prop_{featureId}` can be derived from the selected gene names, to convert `MX1_SPOTS` to `prop_mx1spots`), based on the logic in `tissue-map-tools` and the output ng-annotations files it generates? If we cannot make assumptions about how the data has been normalized, then perhaps we could compute the min/max from the corresponding obsFeatureMatrix column upon loading it when a user has selected a gene. These are both probably questions for @EricMoerthVis and @LucaMarconato regarding `tissue-map-tools`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c6366a8cfa54`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.