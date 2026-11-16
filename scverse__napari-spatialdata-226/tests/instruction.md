# Issue

**Title:** Avoid exception when key binding collides with existing

## Description

This avoids raising an error on key binding collision when napari-spatialdata is opened/closed multiple times (or the keymap has bin registered by another plugin).

Sorry, my previous fix was in the wrong direction and too permissive. There is no way to "register only if not yet in use", but one can only force override any previous shortcut. Without `override=True`, the error is raised.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e23ec7120e80`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.