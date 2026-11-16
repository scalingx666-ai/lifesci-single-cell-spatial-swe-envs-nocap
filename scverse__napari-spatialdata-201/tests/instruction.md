# Issue

**Title:** Avoid exception when registering shortcut

## Description

Napari does not allow registering an existing shortcut.

This can occur when:
- Another plugin or Napari itself or the user has registered "Shift-L", "Shift-E" before opening napari-spatialdata
- The user opened and closes napari-spatialdata multiple times in the same Napari session

As a consequence, Napari raises an exception and all code after shortcut registration cannot be used anymore.

This PR adds the optional argument `override` to silence the error. If you prefer `override=True`, I can change that (should have the same effect on avoiding the error).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `880eda1ee14e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.