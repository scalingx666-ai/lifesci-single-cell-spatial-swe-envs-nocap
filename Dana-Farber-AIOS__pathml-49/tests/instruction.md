# Issue

**Title:** Add postprocessing step and tests for PanNuke

## Description

When PanNuke dataset is downloaded, it comes in 3 folds and each fold is a single .npy file for the images and a single .npy file for the maks and a third .npy file for the tissue type labels. There are ~2500 images per fold, so these .npy files for the images and masks are pretty big. 

The current implementation calls np.load() on the big .npy files, and then slices them to get the right images/masks. Loading these arrays can be somewhat slow though, and they also take up memory.

I added a postprocessing step to write each individual image to .png and each individual mask to .npy. I also modified the PanNukeDataset as needed. Tissue type and fold labels are in the filenames.

This setup is more intuitive and hopefully will be faster since we avoid loading the big .npy arrays during training.

I also added tests

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ecd27059c257`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.