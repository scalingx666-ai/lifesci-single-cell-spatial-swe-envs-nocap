# Issue

**Title:** comprehensive support for SCFM (Single Cell Foundation Model) workflows in the CLI and REPL, enabling foundation model-based single-cell analysis

## Description

This pull request introduces comprehensive support for SCFM (Single Cell Foundation Model) workflows in the CLI and REPL, enabling foundation model-based single-cell analysis. It adds a new prompt generator, expands the REPL command routing, updates help and suggestions, and includes robust test coverage for the new functionality.

SCFM Workflow Integration:

* Added `scfm_workflow.py` prompt generator for SCFM analysis, supporting multiple foundation models (scGPT, scBERT, Geneformer, scFoundation, UCE) and user analysis goals. (`pantheon_cli/cli/prompt/scfm_workflow.py`)
* Implemented `/bio scfm` command routing in the REPL, including subcommands for `init`, `run`, and `list_models`, with detailed help and model selection logic. (`pantheon_cli/repl/bio_handler.py`) [[1]](diffhunk://#diff-1ab2f5fbee44a24a3cc325ab1850f606d24451efc24d15bb43e449c1c8cb7c7aR121-R124) [[2]](diffhunk://#diff-1ab2f5fbee44a24a3cc325ab1850f606d24451efc24d15bb43e449c1c8cb7c7aR294-R426)

User Experience Improvements:

* Updated REPL help output and command suggestions to include SCFM commands, making them discoverable and easy to use. (`pantheon_cli/repl/bio_handler.py`) [[1]](diffhunk://#diff-1ab2f5fbee44a24a3cc325ab1850f606d24451efc24d15bb43e449c1c8cb7c7aR59-R61) [[2]](diffhunk://#diff-1ab2f5fbee44a24a3cc325ab1850f606d24451efc24d15bb43e449c1c8cb7c7aR1352-R1354)

Command Mapping:

* Added SCFM entries to the `BIO_COMMAND_MAP` for proper routing and integration with the existing command system. (`pantheon_cli/repl/bio_handler.py`)

Testing:

* Added a new test suite covering SCFM routing, prompt generation, integration with existing commands, and command mapping, ensuring robust functionality and preventing regressions. (`tests/test_scfm_router.py`)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `549ab406ab15`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.