# Issue

**Title:** Add tooltipObsSetsMode coordination type to limit obs sets in tooltips

## Description

#### Background
Hover tooltips list every obs set group that contains the hovered observation. Datasets with many set groups (for example, HuBMAP CODEX datasets with about 30 K-Means groupings) produce tooltips taller than the view, so they get clipped.

This PR adds a `tooltipObsSetsMode` coordination type:
- `all` (default): lists every set that contains the observation, the same as before.
- `selected`: lists only sets within the top-level groups of the current `obsSetSelection`. If nothing is selected, no sets are listed; the ID and obs labels still show.

Filtering keeps whole groups, not only the selected sets. For example, if clusters 1 and 2 of `Cell K-Means [tSNE_All_Features]` are selected and you hover a cell in cluster 3, the tooltip still shows `Cell K-Means [tSNE_All_Features]: 3`.

Example usage:
```json
"coordinationSpace": { "tooltipObsSetsMode": { "A": "selected" } }
```

#### Change List
- Add the `TOOLTIP_OBS_SETS_MODE` constant and register it (default `'all'`, `z.enum(['all', 'selected'])`).
- Add it to the `scatterplot`, `dualScatterplot`, `spatial`, `spatialBeta` and `heatmap` coordination types. In `spatialBeta`, it is read per segmentation channel, like `tooltipsVisible`.
- Add a pure `filterObsMembershipForTooltip` helper to `@vitessce/sets-utils`, with unit tests.
- Apply the helper in the shared `useGetObsInfo` hook (used by scatterplot, spatial and heatmap) and in the `spatial-beta` tooltip's local `getObsInfo`.
- Document the type in `coordination-types.mdx` and add a changeset.

Not included: a toggle in the view options menus. It can be added if users need to switch modes at runtime.

#### Checklist
 - [ ] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable
 - [x] New subpackage(s) manually published to NPM and trusted publishing enabled, or not applicable

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ede6544a181`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.