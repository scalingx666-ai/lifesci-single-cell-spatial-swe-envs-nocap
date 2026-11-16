# Issue

**Title:** Fix 10X contigs filename

## Description

This PR fix the filename pattern for the 10X's contigs from `filtered_contig_annotation.csv` to `filtered_contig_annotations.csv`. 

This fix a bug in `loadContigs()` where the 10X format wasn't recognised correctly when `input` is a directory.

```
    format.list <- list("WAT3R" = "barcode_results.csv",
                        "10X" =  "filtered_contig_annotations.csv",
                        "AIRR" = "airr_rearrangement.tsv",
                        "Immcantation" = "_data.tsv",
                        "MiXCR" = "clones.tsv",
                        "JSON" = ".json",
                        "TRUST4" = "barcode_report.tsv",
                        "BD" = "Contigs_AIRR.tsv",
                        "Omniscope" =c("_OSB.csv", "_OST.csv"))
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ff08088ab835`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.