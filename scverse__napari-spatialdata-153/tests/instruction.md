# Issue

**Title:** Change RGB detection to be based on channel names

## Description

See 

To give users more control over whether a 3/4-channel image is interpreted and visualized as RGB, channel names now need to be explicitly set to ["r", "g", "b"]. Therefore,  would have a new argument `rgb=True` to override the channel names (or auto-detect with `rgb=None`).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `39768254a59d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.