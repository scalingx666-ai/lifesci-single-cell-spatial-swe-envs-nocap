# Issue

**Title:** Fix travis issues

## Description

This PR should make slingshot build on travis again 🙂 

* Vignette could not be built since it could not find the bib file due to it being listed in .Rbuildignore; problem was solved by removing the bib entry from the .Rbuildignore (c8cd422). The html that was in the repository is unneeded and was removed (b6bb33f).
* Remove .travis_init1.yml and instead let travis build in stages, so no manual intervention of warming the caches will have to be done in the future (2554725, dac1b13, 84bfa16, a0c3449, 1e7fdcb, 02f03cb).
* Since BiocStyle and HSMMSingleCell are used in the vignette, they need to be added to the Suggests in the DESCRIPTION (f1573e1, e085b35, e869e7e, 1243abd, cb6ecde).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b8d23b09deb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.