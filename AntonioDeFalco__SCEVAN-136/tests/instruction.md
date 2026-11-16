# Issue

**Title:** Add output_dir functionality

## Description

I've added the `output_dir` functionality and done some limited testing - all files do seem to end up in the correct folder as given to `pipelineCNA`, while also retaining the base functionality of writing to ./output in the case that no `output_dir` is given retaining the default behaviour for users that update to a new version of the package and don't make changes to their code. The changes mostly come down to moving from `paste0("./output/", variables)` to `file.path(output_dir, paste0(variables)`.

One thing I did notice - it seems the segmentation of subclones runs twice, with _slightly_ different results between runs - One of the subclones gets merged into another one, and all the .seg files get recreated in this step. I've attached a .txt file showing my console output of this happening. It's outside the scope of this PR to figure out exactly why that's happening, but might be an important avenue to pursue if you see the same effects.

There furthermore seem to be some functions that never get called anywhere - I've deleted one of those, others I've kept around because they seem to be required for testing that isn't included in this repo. Apologies if that causes trouble somewhere down the road.

Feel free to get in touch for clarification!

[SCEVAN_seg_bug.txt](https://github.com/user-attachments/files/19163925/SCEVAN_seg_bug.txt)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f2ca335e1804`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.