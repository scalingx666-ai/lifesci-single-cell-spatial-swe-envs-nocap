# Issue

**Title:** Clonalcluster bcr chains

## Description

Per issue #587 

`clonalCluster(chain = "both")` hardcoded c("TRA", "TRB"). getIR() parses the V(D)J(C) block by chain name, so BCR data was read with the TCR layout: the heavy slot took the D gene as its J call and the light slot took the C gene. With use.J = TRUE, the default for `combineBCR()`, the J filter was matching on the wrong gene in both slots. Resolve the chain
names from the data with a new `.detectReceptor()` helper.

`clonalCluster(group.by =)` renamed the cluster column by position. Once group.by is set the vertex attributes are name, group, cluster, so position 2 is the grouping variable and the .Cluster column came back holding group labels, with the real IDs left in a trailing cluster column. Select by name instead.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a3116982ecc8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.