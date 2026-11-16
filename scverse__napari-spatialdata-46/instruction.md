# Issue

**Title:** Select coordinate system and elements in SpatialData widget

## Description

This PR allows:

<img width="263" alt="image" src="https://user-images.githubusercontent.com/22676591/226540007-25c857f0-3308-4355-8d00-0e37f3d03727.png">

In the top box, a coordinate system can be selected. This dynamically changes the bottom box, showing relevant elements. Selecting an element adds it to the viewer.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8a242b432302`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.