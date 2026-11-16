# Issue

**Title:** Dev

## Description

- ignore negative values for histogram lower and upper bound while retaining the ability to pan below 0. Will need to explicitly write in the documentation that negative values can be drawn but not used.  
- Fix the number of clicks required to change a filter.  
- Fix the ability to upload multiple tiff files. Each tiff is parsed against the first and assumes the same number of tiff pages (aka the same panel). Any upload that is different is ignored.  
- Fixed the viewer clearing logic when a new dataset is chosen.  
- Fix error when multi tiff uploads were not accepting more than 2 uploads due to unique channel names. Partially  (will migrate second portion to new issue)
- Ensure that the channel order is maintained on reupload from h5.  
- Fix reset of the histogram on new drag and drop upload.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b8183c853a12`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.