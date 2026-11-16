# Issue

**Title:** Upgrade min versions of dependencies [zh2426]

## Description

https://app.zenhub.com/workspaces/single-cell-5e2a191dad828d52cc78b028/issues/chanzuckerberg/cellxgene/2426

* Removed restriction on Flask 2.0 since Flask-Restful now supports it
* Removed jinja requirement since Flask 2.0 enforces it (we were not using it, just in there to avoid a vuln)
* Add arg in setup.py to~enforce py3.6+

# Testing
Tested flask 2.0 on py3.7 and py3.9

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f49c3d8fe7d8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.