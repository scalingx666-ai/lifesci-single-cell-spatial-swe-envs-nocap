# Issue

**Title:** docs: Fix installation instruction

## Description

Since a long time, the PyQt5 wheels have been available on PyPi. This part of instruction is no longer relevant. 

Also specify PyQt5 dependency using `napari[pyqt5]` to enforce version constraints from napari (to not install incompatible version of `PyQt5`)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `66b655567799`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.