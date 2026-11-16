# Issue

**Title:** Fixes performance with multiscale, fixes docs

## Description

* Fixes performance issue with multiscale images. Performance tested on the Xenium + Visium dataset (the one where the performance problem got reported)
	* closes 
	* closes 
* Refactor the name and the docstring of `_transform_to_rgb()`, now called `_adjust_channels_order()`, as the name was misleading. The function is not transforming to RGB, but it's swapping the dims and telling if the image is RGB or not. Also the swap of the dims is done all the time a `c` dimension is present and not just when an RGB image is passed, as the old docstring suggested.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e1d308d16a8d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.