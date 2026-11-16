# Issue

**Title:** NickAkhmetov/Fix cell set expression plot crash on empty obs set selection

## Description

<!-- Credit (as a starting template): https://github.com/visgl/deck.gl/blob/master/.github/pull_request_template.md -->
<!-- For feature, feature enhancement or bug fix, create an issue first and finish To Do List there -->
<!-- Anything doesn't work as expected is a bug, including code, doc and test -->
 
<!-- For other PRs without open issue -->
#### Background
Slightly malformed confs with empty datasets experienced crashes due to CellSetExpressionPlot receiving undefined obssetselections.

Before a gene is selected, the subscriber renders `<span>Select a {featureType}.</span>` and the plot isn't mounted. Selecting a gene makes `histogramData` truthy, which mounts `CellSetExpressionPlot` for the first time — and any stale/placeholder entry in the coordination-space `obsSetSelection` now flows into this reducer. The config at issue doesn't declare an obsSetSelection scope on the obsSetFeatureValueDistribution view, so it picks up whatever default is in the shared store.

The fix makes the reducer ignore paths whose tail segment is missing (treat their length as 0) instead of crashing. Same behavior for well-formed selections; graceful for malformed ones.

The same issue was present in the ticks, which now explicitly fall back to an empty string if `d` has no `.at(-1)`.

#### Change List
- Adjusted maxCharactersForLabel to gracefully handle malformed labels.
#### Checklist
 - [x] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable

<img width="1868" height="931" alt="image" src="https://github.com/user-attachments/assets/4a08ad77-4b65-462b-81e8-549b8cf36e32" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e4e694df70e7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.