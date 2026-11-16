# Issue

**Title:** Add sf as weak dependency as suggested by sp package

## Description

(see also https://r-spatial.org/r/2023/05/15/evolution4.html). Here is similar info that we see when nichenetr loads sp internally:

> library(nichenetr)
The legacy packages maptools, rgdal, and rgeos, underpinning the sp package, which was just loaded, will retire in October 2023. Please refer to R-spatial evolution reports for details, especially https://r-spatial.org/r/2023/05/15/evolution4.html. It may be desirable to make the sf package available; package maintainers should consider adding sf to Suggests:. The sp package is now running under evolution status 2
     (status 2 uses the sf package in place of rgdal)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `311ef43c7c23`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.