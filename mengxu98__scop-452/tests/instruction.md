# Issue

**Title:** fix: restore SCENIC network style and prevent zero-sized viewports

## Description

SCENIC network PDFs can fail with `Viewport has zero dimension(s)` when hundreds of TF legend entries consume the plotting panel. The `network_graph` branch also ignored `network_tf`, and the generic renderer discarded label selections and reciprocal edge rows.

Restore the historical SCENIC renderer: colored TF circles, gray genes, source-TF edge colors, centered TF labels, radial single-TF labels, and the top RSS group legend. Keep the existing weighted layouts and full-network display by default.

- Honor `network_tf` before `features`, including selected SCENIC+ triplet neighborhoods.
- Respect label budgets and explicit all/none settings; preserve reciprocal directed edges and complete annotation tables.
- Omit legends above 20 TFs to prevent zero-sized viewports; retain explicit TF/regulon legend modes.
- Add opt-in `network_display_targets` for top targets plus shared targets and TF-to-TF links. Return the exact display tables separately from the complete selected graph; selected regions retain downstream genes.

Validation:
- Complete `test-scenic-plot.R` suite: 167 passing assertions, no failures or errors.
- Supplied plotting data: full 555-node/674-edge graph and 243-node/250-edge focal-TF view exported successfully, with unchanged retained edge rows. PDF previews were inspected locally.
- R source parsing, Rd validation, and `git diff --check` passed.

The original customer Seurat object and a full local `R CMD check` were not run. No package version or dependency changes are included.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `86506370d34a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.