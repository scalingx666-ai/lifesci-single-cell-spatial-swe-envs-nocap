# Issue

**Title:** chore(master): release alevin-fry 0.6.0

## Description

:robot: I have created a release *beep* *boop*
---

## 0.1.0 (2022-06-01)

### ⚠ BREAKING CHANGES

* **cmd_interface:** Add a (hidden) --umi-edit-dist option that take a value informing the underlying resolution algorithm of which edit distances to consider for collapse among potentially colliding UMIs. Right now, 0 works with all methods, while 1 only works with parsimony(-gene) and parimony(-gene)-em. The default remain as before, 1 for parsimony(-gene) and parsimony(-gene)-em, and 0 for all other methods. If the user attempts to set an unsupported edit distance for a method, the program will complain and exit.

### Features

* add hidden large PUG threshold cmd line option ()
* add release-please ()
* add toy run in github actions ()
* add toy run in github actions ()
* cmdline file and directory validation ()
* **resolution:** Add exact UMI only dedup mode to parsimony ()
* **resolution:** Add parsimony-gene and parsimony-gene-em modes ()
* **resolution:** add USA support to parsimony and parsimony-em ()
* **resolution:** Improve parsimony in USA mode ()
* toy run in github actions ()
* toy run in github actions ()
* toy run in github actions ()

### Bug Fixes

* autobump is wrong ()
* bump libradicl patch ()
* **resolution:** Fix indexing in alternative resolution for usa parsimony ()
* **resolution:** revert prefer splicing heuristic ()
* update compare_counts.py to user newer pyroe ()
* version number ()

### Code Refactoring

* **cmd_interface:** remove --pug-exact-umi add --umi-edit-dist ()

---
This PR was generated with [Release Please](https://github.com/googleapis/release-please). See [documentation](https://github.com/googleapis/release-please#release-please).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `151e81a1384d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.