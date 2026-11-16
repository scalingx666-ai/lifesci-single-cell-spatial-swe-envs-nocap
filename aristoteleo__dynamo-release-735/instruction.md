# Issue

**Title:** Added tutorial of external velocity calculation and integration

## Description

This pull request introduces several improvements and new features to the tracking and reporting of data changes in the `dynamo` package, as well as minor updates to tutorials and submodules. The main focus is on enhancing the monitoring of function calls and improving the detail and clarity of change reports for AnnData objects. Additionally, new monitoring decorators are applied to core functions, and tutorial documentation is updated.

**Tracking and reporting enhancements:**

* Improved the `_track.py` monitoring system to capture and display column data types in `obs` and `var` instead of just column names, providing more informative reports on data changes. This includes a new `_get_column_type` helper and updates to `_snapshot` and `_print_report` to show type information. (`dynamo/tools/_track.py`) [[1]](diffhunk://#diff-f63fda4c46993582395a1008ef93647daf8dde3937a459c4e31855f454d3bb5fR67-R83) [[2]](diffhunk://#diff-f63fda4c46993582395a1008ef93647daf8dde3937a459c4e31855f454d3bb5fL149-R161)
* Enhanced the change report for `uns` keys to include a `✚` symbol for added keys, making additions more visually distinct. (`dynamo/tools/_track.py`)

**Monitoring and function instrumentation:**

* Added the `@monitor` decorator to the `extvelo` and `pseudotime_velocity` functions, enabling automatic tracking of changes to AnnData objects during their execution. (`dynamo/tools/_extvelo.py`, `dynamo/tools/pseudotime_velocity.py`) [[1]](diffhunk://#diff-ea55e3df53e730545639315187ce9737149c08f1adeec403617b55aed4362120R4-R7) [[2]](diffhunk://#diff-eb2bc1eb1f8113012c15a9c8e9c721b1920f1db067825261c2bd513c7558ebf8R13-R18)

**Functionality improvements:**

* Updated `pseudotime_velocity` to automatically set `use_for_dynamics` and `use_for_transition` in `adata.var`, copying from `use_for_pca` if present, or defaulting to `True` otherwise, ensuring downstream compatibility. (`dynamo/tools/pseudotime_velocity.py`)

**Documentation and tutorials:**

* Added a new tutorial notebook `202_extvelo` to the conventional index, and updated the `notebooks` submodule to the latest commit. (`docs/tutorials/index_conventional.md`, `docs/tutorials/notebooks`) [[1]](diffhunk://#diff-25662e0f97f617cb4298197d401202faa1a79627967a5becf1457f6277ee505fR8) [[2]](diffhunk://#diff-fb0b1ba8378643c7ec6e8f7cfb299156f2f52246de14f4d8bafd0a0d35b044e1L1-R1)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ced638059666`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.