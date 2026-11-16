# Issue

**Title:** Fix _current deprecation

## Description

From napari 0.5.0 onwards the use of `Selection._current` from a plugin would become deprecated. This currently gives warnings. The alternative would be to use `Selection.active`. The behaviour of this is slightly different from `Selection._current`, but this does not affect our code.

In short the difference in behaviour is that when having a `Selection` of multiple layers, there is no `Selection.active`, while there can be `Selection._current`.

## Reference
https://napari.org/stable/api/napari.utils.events.Selection.html

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `46cdd728795a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.