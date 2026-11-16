# Issue

**Title:** mark edits on imaging chapters

## Description

Here are some extra notes that I didn't do anything about but came to mind:
- in the imaging QC section, there are some cells at the bottom of the slide that were all deemed low-quality .. I wonder if it's worth making a remark about reducing the window size
- should we remove the CCC chapter for now? It would be nice-to-have, of course, but right now it's not evaluated
- I would like a bit more explanation of `plotColocal` in the neighbourhood analysis section (as in, just what is being correlated with what); unfortunately, I wasn't able to easily find this in their docs. Do you know offhand what is being correlated, or should I read the paper?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3ef050ed8a5c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.