# Issue

**Title:** Correcting the function - wrong argument

## Description

overlap <- length(intersect(df.i_unique[,call], df.j_unique[,call]))
              coef_matrix[i,j] <- overlap/min(length(df.i_unique[,call]), length(df.j_unique[,call]))

- replacing the "CTgene" argument with the value of the call argument defined by the user when calling the function

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `61e3b0871fee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.