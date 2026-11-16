# Issue

**Title:** Barebone annotate

## Description

This PR serves to provide a barebone annotation widget. At the moment only shape annotations are supported but I am to extend this to points and perhaps labels as well. Furthermore, at a later stage also a table widget will be provided.

Currently, the user can annotate using and also reload shape annotations. The `description` column at the moment serves no purpose but this will come with the table widget.

@LucaMarconato maybe before putting this in we need to discuss a little bit about UI experience.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `025c5cfdd94c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.