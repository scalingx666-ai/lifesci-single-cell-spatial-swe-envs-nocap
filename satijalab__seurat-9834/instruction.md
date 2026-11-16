# Issue

**Title:** Fix FindTransferAnchor for integrated SCT references

## Description

This PR enables `FindTransferAnchors` to work with `SCTransform` references that have been preprocessed using `IntegrateLayers`. Handing an integrated reference to `FindTransferAnchors` is a routine operation and represents the core of the `Azimuth` package's workflow. Unfortunately, it has not been possible to use an SCT reference from `IntegrateLayers` since (as opposed to the v3 `FindIntegrationAnchors` + `IntegrateData` workflow) it does not generate an integrated assay. When starting from multiple SCT references, `FindTransferAnchors` assumes that `IntegrateData` has already picked a single model and outputted it in the integrated assay, so the function throws an error if multiple models are present. 

This PR resolves the issue by teaching `FindTransferAnchors` to pick the biggest SCT model (i.e., the one with the most cells) when given a reference with more than one.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55e3ae6e2a1e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.