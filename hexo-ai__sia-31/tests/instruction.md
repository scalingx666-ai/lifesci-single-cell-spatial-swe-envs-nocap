# Issue

**Title:** fix(gpqa): write evaluator output to results.json

## Description

## Summary
- make the bundled GPQA evaluator write `results.json` by default
- keep explicit `--output` overrides unchanged
- add a regression test for the SIA evaluator artifact contract

## Why
`run_evaluation()` treats `gen_*/results.json` as the canonical evaluator artifact. GPQA previously wrote `evaluation_results.json` by default, so evaluation could complete but the orchestrator would still report that `results.json` was missing.

## Test plan
- `python3 -m pytest tests/test_gpqa_evaluator.py -q`
- `python3 -m pytest tests/test_gpqa_evaluator.py tests/test_run_evaluation.py tests/test_run_evaluation_outcomes.py -q`
- `python3 -m ruff check .`
- `python3 -m pytest -q`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6ad5ad7bc953`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.