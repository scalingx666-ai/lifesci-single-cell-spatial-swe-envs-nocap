# Issue

**Title:** #2410 update compatibility test matrix

## Description

#### Reviewers
**Functional:** 
@MDunitz 
@danieljhegeman 

**Readability:** 
n/a (no source code changes)

---

## Changes

Github Actions Workflow updates compatibility matrix:
- Added MacOS Catalina and Big Sur to test compat matrix
- Added Python 3.9 to test compat matrix, but avoid running 3.9 for matrix jobs that do not have `tables` pypi build available for the given env
- Maintains running tests on both cellxgene main branch and latest pypi release.
- Add explicit matrix exclusions for matrix combinations that will never pass (see comments).
- Numerous refactorings to the workflow config to simplify matrix. Basically a rewrite.
- The anndata pkg is now tested at a pinned release and at latest release, but no longer using `master` branch version. To limit cross-product explosion of matrix jobs, the pinned anndata version is only tested on py3.8 and cellxgene latest release.
- Run unit and smoke tests in a single job, to improve speed, reduce workflow complexity and the number of jobs. Also fixes the redundant testing of unit tests. Within each job, the unit and smoke tests are run in separate steps for ease of troubleshooting. 
- Fixed termination of backend server to allow both smoke tests to run within a single job (both attempt to use 5005 port, sequentially, but first server was not being terminated).
- ~Run `npm ci` setup to address jest failures. This was a shot-in-the-dark fix, and I'm not 100% confident about it.~ [I removed the existing `make ci` by accident, and then rediscovered it's necessity 🤦 ]
- Replaced `continue-on-error: true` with `fail-fast: false`, which allows all matrix jobs to run independently, while also ensuring the that entire workflow is flagged as failed if any matrix job fails

N.B.: **Failures are still occurring!** All failures occur for `smoke-test-annotations` and they appear to be intermittent. I recommend we fix this as a [separate story](https://app.zenhub.com/workspaces/single-cell-5e2a191dad828d52cc78b028/issues/chanzuckerberg/cellxgene/2433), since the essential work for updating the compatibility testing matrix is otherwise complete.

## Validation
Passing run (`smoke-test-annotations` disabled): https://github.com/chanzuckerberg/cellxgene/runs/3654109451?check_suite_focus=true

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3ebbb0ccbf91`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.