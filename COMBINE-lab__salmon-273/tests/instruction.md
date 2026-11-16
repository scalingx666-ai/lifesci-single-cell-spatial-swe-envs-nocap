# Issue

**Title:** Update .travis.yml to add test case easily.

## Description

This is related to 

* Now there are 2 test cases on Travis CI, adding one case.
* Added code for speed up such as `git - depth: 1`, `make -j 4`.
* Refactoring. Removed tailing spaces.

Notes:
* I added `gcc-5`'s case as maybe it is minimal support version of gcc for this project.
* I want to replace current case `gcc-7` to latest version `gcc-8` if you like.
* Total running time ("Ran for" on the Travis page.) becomes faster than current situation. In my repository, total running time is "15 min 11 sec", seeing current master branch's test is around 17 min+. See [1]
* Removed `travis_wait`. Without the command, the default behavior is "when a long running command or compile step regularly takes longer than 10 minutes without producing any output". [2] I have not faced the situation when I  did debug. 
* There are commented out area at the bottom of `.travis.yml`. However as we can run `git log -p .travis.yml` to check past modification, shall we remove the commented out "whitelist" area?

[1] https://travis-ci.org/junaruga/salmon/builds/417976633
[2] https://docs.travis-ci.com/user/common-build-problems/#build-times-out-because-no-output-was-received

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7f392bc5436e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.