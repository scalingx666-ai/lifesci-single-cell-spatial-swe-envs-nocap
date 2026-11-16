# Issue

**Title:** Test loading elements without viewer

## Description

This PR introduces the ability to add elements to the Interactive class without opening the Napari viewer. 

Other minor changes:
- The previous `test_interactive.py` file has been renamed to `test_widgets.py`, and the new tests have been added to `test_interactive.py`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cd14f9c747f7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.