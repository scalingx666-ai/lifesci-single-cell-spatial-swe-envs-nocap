# Issue

**Title:** feat: add spatial CCC slice network plot

## Description

## Summary  - Add CCCNetworkPlot(plot_type = spatial) for stored slice-level CCC overlays. - Support SpatialCellChat, SpaTalk, and COMMOT payloads with strict coordinate/ID validation. - Render spot/cell layers, abundance-scaled group centroids, sender-coloured directed edges, labels, and composition pies. - Add producer payload storage, tests, Rd documentation, NEWS, and spatial workflow guidance.  ## Validation  - pkgload::load_all(..., compile=FALSE) passed. - Targeted SpatialCellChat, SpaTalk, COMMOT, spatial renderer, and coordinate-contract tests passed. - tools::Rd2ex() plus parse() for man/CCCNetworkPlot.Rd passed. - Local no-manual/no-examples/no-tests rcmdcheck: 0 errors, 0 notes; one inherited Rd usage warning remains. - --as-cran was attempted but blocked at CRAN incoming feasibility in this Windows environment.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `68ae45aacdd1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.