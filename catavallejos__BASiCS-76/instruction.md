# Issue

**Title:** Add diagPlot and diagHist functions

## Description

Add functions for visualising diagnostic measures from coda
(currently only effectiveSize and geweke.diag)
across multiple parameters simultaneuously.
geweke.diag is probably an odd inclusion and might be removed.
Also some incidental refactoring.

Resolve #69

Diagnostic plot (in this case mu vs delta with mu ESS)
![p](https://user-images.githubusercontent.com/10779688/54835364-d94eed80-4cb9-11e9-8fa6-390a7e84fa14.png)


ESS across all parameters
![h_all](https://user-images.githubusercontent.com/10779688/54835176-8ffe9e00-4cb9-11e9-99dc-8243ed2c9c44.png)

ESS for mu only
![h_mu](https://user-images.githubusercontent.com/10779688/54835178-912fcb00-4cb9-11e9-8f17-60dbbd3ad27a.png)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c893281aa34c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.