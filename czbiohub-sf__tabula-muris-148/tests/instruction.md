# Issue

**Title:** Load tiss to object and cleanup Trachea

## Description

Fixes Rmds that weren't saving the output of `load_tissue_{droplet,facs}` to an object

```
(tabula-muris-env)  ✘  ~/code/tabula-muris/00_data_ingest/02_tissue_analysis_rmd   master  grep '^load_tissue' *.Rmd
Marrow_droplet.Rmd:load_tissue_droplet(tissue_of_interest)
Marrow_facs.Rmd:load_tissue_facs(tissue_of_interest)
Trachea_facs.Rmd:load_tissue_facs(tissue_of_interest)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d060f2da8530`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.