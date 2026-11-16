# Issue

**Title:** pkgdown needs to see the full path to external PNG files to embed in vignettes

## Description

`pkgdown` needs to see the full path to PNG files, to understand that it needs to copy them into the website

Deleted `SCREENSHOT()` and replaced by `knitr::include_graphics("screenshots/file.png")`

Sources:

- https://github.com/r-lib/pkgdown/blob/16231d9a2b2c47b6616ad32678917918b8621a62/R/build-articles.R#L86

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1232d03435a8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.