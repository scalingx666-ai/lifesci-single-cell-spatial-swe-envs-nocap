# Issue

**Title:** Quick patch of InteractiveSpatialPlot CRAN check NOTES

## Description

Small patch to fix CRAN check NOTES: ```InteractiveSpatialPlot: no visible global function definition``` for uiOutput, renderUI, reactiveVal, and tags global variables. These function names are now loaded in via @importFrom from the miniUI and shiny packages in InteractiveSpatialPlot roxygen comments.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a5ad88756d3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.