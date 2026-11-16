# Issue

**Title:** Add element api

## Description

This is a follow up PR of #169 and should finish the last task of #159. When adding an element now the element will always be visible even when the element is not present in the current `coordinate_system`. However, if `view_element_system` is set to `True`, it is switched to the `coordinate_system` specified by the user for viewing the element.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa6f1d4a02e8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.