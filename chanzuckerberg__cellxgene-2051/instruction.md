# Issue

**Title:** Fix indexing bug in user-specified colors

## Description

Internal color tables for user-specified colors (loaded from the AnnData object) were incorrectly indexed, causing them to display out of order (or to drop color swatches entirely in the LSB). Colors should be indexed by category display order, as specified in the internal schema.  Prior to PR #1929 they were indexed incorrectly (by another index).  An incorrect fix in PR #1929 modified this order, and added a second bug by attempting to index the color by label value.  This PR reverts the incorrect fix, and fixes both #1901 and #2007, which are essentially the same issue, by indexing colors by their display order.

In addition, while testing this fix, @signechambers1 found an additional repaint bug in the categorical (LSB) display.  When adding new user-created categories, the CategoryValue component would fail to repaint labels that had a color change. This was due to an overly aggressive `shouldComponentUpdate` function, which has been made more conservative.

 
 
Reverts changes made PR #1929

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e6281baa39b0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.