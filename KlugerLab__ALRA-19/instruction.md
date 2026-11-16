# Issue

**Title:** modify if statement for R 4.2.0

## Description

Related to #18

From the R 4.0.0,
```
CHANGES IN R 4.0.0
SIGNIFICANT USER-VISIBLE CHANGES:
• matrix objects now also inherit from class "array", so e.g., class(diag(1))
is c("matrix","array"). This invalidates code incorrectly assuming that
class(matrix_obj)) has length one.
S3 methods for class "array" are now dispatched for matrix objects.
```

The class function will return not only 'matrix' but 'array'
So if comparing as 1d like `if (class(A_norm) != 'matrix')` does not work.
Here, I tried to implement if the class(A_norm) contains a matrix, return true.

### Checklist 
- [x] Work correctly

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7636de81d66d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.