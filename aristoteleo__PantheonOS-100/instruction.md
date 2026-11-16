# Issue

**Title:** feat: add rare disease ontology-first skill with bundled scripts

## Description

## Summary

Add a rare disease ontology-first skill with self-contained CLI scripts shipped inside the skill directory. Uses `~/.pantheon/rd_ontology/` as the global shared database path. No framework-level changes — agents invoke scripts via the `shell` toolset.

Supersedes #99.

## What changed from v1

| v1 (closed) | v2 (this PR) |
|---|---|
| `rd_ontology` ToolSet registered in framework | Scripts live in `skills/rare_disease/scripts/` |
| Changed `pantheon/toolsets/__init__.py` | No framework changes |
| Changed `pantheon/endpoint/toolsets.py` | No framework changes |
| DB at `data/rd_ontology_store/` (project-local) | DB at `~/.pantheon/rd_ontology/` (global, shared) |
| Agents use toolset API calls | Agents use `shell` to invoke Python CLI |

## Files

### New
- `skills/rare_disease/scripts/build_rd_ontology.py` — ETL pipeline (Orphanet/OMIM/HPO → SQLite)
- `skills/rare_disease/scripts/query_rd_ontology.py` — CLI: resolve, disease, find_by_hpo, hpo_term, stats

### Modified
- `skills/rare_disease/rd_ontology_first.md` — updated for shell-based usage, global DB path
- `agents/rare_disease/evidence_researcher.md` — `rd_ontology` → `shell` toolset
- `agents/rare_disease/phenotype_structurer.md` — `rd_ontology` → `shell` toolset

### Unchanged from upstream
- `agents/rare_disease/leader.md`, `auditor.md`, `genotype_analyst.md`, `reporter.md`
- `teams/rare_disease_team.md`
- All framework code

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `69b6bc1deaf3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.