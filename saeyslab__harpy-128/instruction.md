# Issue

**Title:** visium wrapper around spatialdata-io reader

## Description

This PR add a wrapper function around spatialdata.io.readers.visium.visium with the option of reading in the fullres microscopy image.

The PR also updates the visium_hd wrapper so that it takes 'filtered_counts_file', 'fullres_image_file' and 'load_all_images' and passes them on to the spatialdata-io visium_hd reader. Note that spatialdata-io places the full image and cystassist image in the 'global' coordinate system, while all other data is placed in the dataset-id coordinate system. This results in, for example, issues when plotting (tested with spatialdata-plot) and does not seem like the desired behavior. A fix was added here, but it should probably be addressed in the spatialdata-io visium_hd reader itself.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ec9e34143cc0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.