# Issue

**Title:** Ensure consistent coloring by gene when ordering changes.

## Description

Simplifies `gene` and `reqGene` so that they now contain the same value - the latter triggers a fresh request for expression values, the former triggers a recolor of the scatter plot.

Not sure about some of the React-ish parts:

- Did I do the right thing in the second argument of `useEffect` in `ScatterPlot.js`?
- In various parts, I put `let tmp = [...selectedClusterSummary];` before assigning `setSelectedClusterSummary(tmp);`. Can't we just modify `selectedClusterSummary` in place and then call `setSelectedClusterSummary(selectedClusterSummary)`?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e290eac049d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.