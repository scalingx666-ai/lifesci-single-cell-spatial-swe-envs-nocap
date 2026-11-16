# Issue

**Title:** re-export expression2List() with deprecation message

## Description

@ncborcherding People reading old tutorials / with old code may need a way to figure out why things are not working like in #440 and likely dont read `NEWS.md`

Also the current approach is that an error is thrown when trying to use the exported function, but if the user is persistent on using it, they are forced by details to read the documentation, leading to them seeing the deprecation reason. If they are still persistent then I've given them an option to set the `force` argument to TRUE. It may be even helpful psychologically to make the process even harder by forcing users to use scRepertoire:::.expression2List() after they read the docs but I think people who get to this point probably just need it for something quick...

Also note that the documentation is tagged with `@keywords internal` so no need to worry about people re-discovering it. pkgdown should either just straight up not display it in reference of it will have the deprecation tag graphic next to it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bda1cb5ddeb1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.