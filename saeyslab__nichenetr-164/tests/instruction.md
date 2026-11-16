# Issue

**Title:** Update differential_nichenet_plotting.R

## Description

Correct error that is generated when ligand is present in more than one niche: 
```
Error in `mutate()`:
! Problem while computing `ligand_ordered = factor(ligand, ordered = T, levels = ordered_ligands$ligand)`.
Caused by error in `levels<-`:
! factor level [31] is duplicated
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `acdaac1043af`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.