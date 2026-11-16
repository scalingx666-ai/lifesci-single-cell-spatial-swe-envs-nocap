# Issue

**Title:** add color by in adata view

## Description

This issue removes the points in `QtAdataViewWidget` and replaces it by a `QLabel` indicating by which column a layer is being colored. Furthermore the construct of `:column_name` is not added anymore to the layer name. As a result the layer name is not changed when running any operation. 

Furthermore, because of this the removal of elements after coloring operations have been performed is fixed. Previously this would return an error due to the layer name having changed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `495d7629ffa2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.