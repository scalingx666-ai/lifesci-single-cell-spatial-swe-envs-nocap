# Issue

**Title:** Added alternative go.env construction with biomaRt and GO.db

## Description

The biomaRt library directly connects to the Ensembl BioMart service and does not depend on updates for the org.Hs.eg.db library. Furthermore, for me it was easier to switch from gene names to Ensembl IDs as rownames(cd) with this code.

See preview here: http://jenzopr.github.io/scde/pagoda.html
Best,
Jens

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `73e4d114bb36`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.