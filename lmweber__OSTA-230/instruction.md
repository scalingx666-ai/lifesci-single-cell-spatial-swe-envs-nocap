# Issue

**Title:** +`SpaceTrooper` in "img-quality-control"

## Description

PR consolidating "img-quality-control_SpaceTrooper.qmd" into "img-quality-control.qmd", with some simplifications and restructuring. This was originally drafted by D.Risso and D.Righelli during/post the Zurich hackathon top of the year (still kept a backup, for now).
- CosMx QC now includes IF markers, border effects, FOV visualization, polygon plots, etc.
- Xenium data is only QCed using `scuttle`, with the final object (for consecutive chapeters) identical to before
- Still awaiting `SpaceTrooper` updates, e.g., interop with `SpaExpIO`, an equation for the score, preprint reference

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `73c8df870743`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.