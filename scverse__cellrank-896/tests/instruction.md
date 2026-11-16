# Issue

**Title:** Feature/update repr

## Description

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description
<!-- Clearly and concisely describe your changes. This section will be shown in the docs. -->
Updates kernels/estimators ``__str__/__repr__`` and allows for better method chaining.

## How has this been tested?
<!-- Describe in detail how you've tested your changes. -->
TODO

## Closes
<!-- If applicable, type `closes #XXXX` in your comment to auto-close the issue that this PR fixes. -->



@Marius1311 currently for GPCCA, the repr/str looks like, e.g.,
```python
GPCCA[kernel=ConnectivityKernel[n=2531], terminal_states=['0', '1'], macrostates=['0', '1']]
``` 
Please let me know is this is ok or how would you improve this.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c42056b57454`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.