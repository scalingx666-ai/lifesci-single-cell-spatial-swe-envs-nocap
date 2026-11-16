# Issue

**Title:** Added script to generate plots.

## Description

This will create an R script from the Rmd file to generate plots.
This allows the handling of parallel processing which Rstudio doens't
handle well.
There is also a full gene list for generating the full gene list of plots.

This commit just sets up the basic tooling but doens't yet handle only generating images
if there is some count for at least one of the cell lines. That will come next.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f255832aee62`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.