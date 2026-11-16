# Issue

**Title:** Add new tutorial notebooks

## Description

This PR:
(1) Adds a new section, "Analysing Nanostring data in the Scatter Widget" to the tutorial notebook on using napari-spatialdata. Related tutorial: https://squidpy.readthedocs.io/en/stable/external_tutorials/tutorial_nanostring.html
(2) Removes self.model.scale
(3) Removes examples relying on AnnData and replaces with SpatialData examples

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5b893f4cbcff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.