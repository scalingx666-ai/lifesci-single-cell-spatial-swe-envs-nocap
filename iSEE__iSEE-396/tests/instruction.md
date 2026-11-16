# Issue

**Title:** Restores use of SCREENSHOT() in vignettes

## Description

The `SCREENSHOT` alias is necessary to allow each Rmarkdown file to be used both for vignette building as well as for screenshot compilation in https://github.com/iSEE/screenshots. When building the vignette, the alias simply diverts to `knitr::include_graphics`, whereas upon compiling the screenshots, the alias is overwritten to call **webshot2** functions to compile the vignettes. This approach avoids duplicating the code required to create the screenshots in a separate file/repo.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d23ebb5a3a7b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.