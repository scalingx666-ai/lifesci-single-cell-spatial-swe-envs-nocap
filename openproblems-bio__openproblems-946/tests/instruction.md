# Issue

**Title:** Fix splitting results by paramset

## Description

## Describe your changes

`get_results` merged all parameter sets of a method into a single row for runs that follow the `paramset_name` convention of `common/nextflow_helpers` (e.g. `task_predict_modality`).

* `get_results`: read `paramset_name` from the scores instead of `paramset_id`.
* `get_results`: parse the paramset from the process tag (`<dataset>.<method>[.<paramset>][.<metric>]`), so that paramset rows get their run stats and metric components, and failed paramset runs show up.
* `render_report`: show each paramset as a separate method (`<method>.<paramset>`). The report crashed on multiple rows per method.
* `task_results_v4.sh`: the dummy paramsets in the test resources now use `paramset_name` and have matching trace rows.

To do:

- [ ] Regenerate `resources_test/openproblems/task_results_v4` with `scripts/create_resources/task_results_v4.sh` and upload to S3 -- until then the dummy paramsets in the test data are ignored.

## Issue ticket number and link
n/a

## Checklist before requesting a review
- [ ] I have performed a self-review of my code

- Check the correct box. Does this PR contain:
  - [ ] Breaking changes
  - [ ] New functionality
  - [ ] Major changes
  - [ ] Minor changes
  - [x] Bug fixes
  - [ ] Documentation

- [x] Proposed changes are described in the CHANGELOG.md

- [ ] CI Tests succeed and look good!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fea93433ae83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.