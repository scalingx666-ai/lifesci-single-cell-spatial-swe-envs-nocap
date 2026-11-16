# Issue

**Title:** feat(singlecellagent): new /bio singlecellagent prompt + REPL wiring and UI support

## Description

This PR adds a dedicated SingleCellAgent experience in the CLI:

Highlights
- New prompt (phase-based, per Biology_toolsets_build_guide) to orchestrate the pipeline automatically.
- /bio singlecellagent handler: init (strict clear) and run <h5ad> with profile/question.
- Alias routing from SingleCellAgent/singlecell/sc and basic /bio scrna use-cases.
- UI displays SingleCellAgent tool calls with analysis_type.
- Tests for prompt content and REPL handler message.

Files
- pantheon_cli/cli/prompt/single_cell_agent.py (new)
- pantheon_cli/repl/bio_handler.py (wiring + aliases)
- pantheon_cli/repl/ui.py (tool call display)
- tests: test_singlecell_prompt.py, test_bio_handler_singlecellagent.py

Notes
- Pairs with the SingleCellAgent OmicVerse-first changes in pantheon-toolsets.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `264bea1c2825`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.