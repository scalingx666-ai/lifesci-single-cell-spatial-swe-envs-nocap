# Issue

**Title:** ci: fix workflow security and announce future container deprecation

## Description

GPU and package-build jobs inherited repository-default token permissions, while `/test-docker` could check out PR code in a privileged `issue_comment` job. This restricts CI tokens and removes the privileged comment checkout to address all nine CodeQL alerts. It also announces future container deprecation while continuing container builds and release publishing.

- Set empty default permissions for GPU tests and wheel/sdist builds, granting only `contents: read` to checkout jobs. Keep the existing GPU label gate and separately scoped label-removal and PyPI publishing jobs.
- Remove `/test-docker` comment execution and its custom commit-status updates. Docker validation remains available through normal PR/push events and manual dispatch; registry login is limited to releases. Use `role_name` in the manual-dispatch check so maintainers are recognized.
- Announce that project-provided container images will be deprecated in a future release, with no date set. Add advance notices and migration guidance to the installation/contributor docs, container directory, and 0.17.1 release notes. Container builds and publishing continue for now; users can plan migration to Conda or prebuilt CUDA wheels with CUDA-X Data Science dependencies.
- Disable persisted checkout credentials in all three workflows and pass dynamic shell arguments through quoted environment variables. Python packages and the manylinux images used for wheel builds remain supported.

Validation: actionlint passed on all three workflows; pre-commit hooks passed; the local container build script passes `bash -n`; migration references were checked. A full Sphinx build was not run. GPU CI requires the existing `run-gpu-ci` label. The default-branch alerts will remain open until the changes are merged and rescanned.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3fbe2a865238`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.