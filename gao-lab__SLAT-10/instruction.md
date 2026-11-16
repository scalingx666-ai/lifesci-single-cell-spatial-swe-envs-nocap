# Issue

**Title:** 🎨 Drawing 3D plot keeping the original colours

## Description

Dear SLAT Authors,

I noticed that when we use the `build_3D` function to visualize the alignment effects, the original idle annotation colors are discarded. It seems this is done to unify the color information of annotations at the same spatial location.

In this pull request, I have preserved the color information. I believe that unifying the color information of annotations at the same spatial location should be done during annotation, not at the final visualization stage.

Additionally, it seems that after using `build_3D`, `plt.savefig()` cannot be used to save the image. I have made `ax` a return value to address this issue.

<img width="372" alt="image" src="https://github.com/gao-lab/SLAT/assets/46667721/c8bd2458-742a-4236-949d-913b3df05fed">

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d49e76d5784`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.