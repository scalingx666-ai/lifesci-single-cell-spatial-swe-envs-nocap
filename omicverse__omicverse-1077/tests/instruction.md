# Issue

**Title:** ov.tl: clinical record error audit and meta-analysis effect extraction (tbs2/ehrmdd)

## Description

TBS RSI branch `tbs2/ehrmdd` at a179fe4a (the commit on which ehr-error-detection, mdd-executive-function and the held-out covmem / ehr-audit tasks reached reward 1).

- `ov.tl.audit_clinical_tables` (+ `load_clinical_tables`, `infer_clinical_schema`, `drug_sex_reference`): rule-family audit of linked clinical / EHR tables for data-entry errors, writes a (table, row id) deliverable.
- Meta-analysis effect extraction: `extract_group_stats`, `group_comparisons`, `meta_effect_sizes`, `hedges_g`, `sd_from_summary`, `to_mean_sd`, `apply_selection_rules`, `comparison_workbook`, `reconstruct_study_effects`, `write_study_effects` (guarded, fingerprinted writer), `verify_deliverable`.
- Tests: `tests/tl/test_clinical_audit.py`, `tests/tl/test_meta_analysis.py` (24 passed on this branch merged with current master).

Generic statistics only; no task constants, labels or answers.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b760a67bd7fc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.