# Issue

**Title:** Adds openslide backend

## Description

This is adding the openslide backend for reading WSIs. It is using a modified version of the OpenSlideStore class from  [manzt/napari-lazy-openslide/napari_lazy_openslide/store.py](https://github.com/manzt/napari-lazy-openslide/blob/main/napari_lazy_openslide/store.py) to do so. 

The issue related to stergioc/sopa#3 has been solved. At the moment, the feature extraction excecution time is x3 faster with the openslide backend (related to stergioc/sopa#2).

I let you @quentinblampey do the final checks :)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af6df1ffbc95`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.