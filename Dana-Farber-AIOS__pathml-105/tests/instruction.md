# Issue

**Title:** Moves generate_tiles logic to backend

## Description

Moves tile generation logic from SlideData to the backend. That's better because the logic will be different for different backends. `SlideData.generate_tiles()` calls the `generate_tiles()` method of the backend internally, and then tries to add corresponding Masks to each tile. Also adds the slide-level labels to each tile. 

Implemented `generate_tiles()` for `OpenSlideBackend` and added some tests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7f5ca099ffd0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.