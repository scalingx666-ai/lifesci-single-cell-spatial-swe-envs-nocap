# Issue

**Title:** Add protein mutation enhancement workflow skill

## Description

## Summary

Adds a new Code-as-Action workflow skill for protein gain-of-function mutation design.

This PR introduces `protein-mutation-enhancement`, a deterministic orchestration layer for:

- building single, double, and higher-order mutant libraries;
- assigning stable variant IDs such as `A12V+G47D`;
- merging ESM sequence-effect scores, ESMFold-class structure metrics, property heuristics, and optional functional proxy scores;
- ranking candidates with weighted normalized scoring;
- deciding whether a design loop should stop or continue into the next round.

The heavyweight model work remains in existing skills such as `fair-esm2` and `esmfold2`; this skill only adds stdlib-only workflow helpers and documentation.

## Area

- [ ] Web UI / frontend
- [ ] Agent / loop / delegation
- [ ] Kernel / host RPC / runtime
- [ ] Server / gateway / API
- [ ] Store / provenance / artifacts
- [x] Skills / science runtime
- [ ] Compute / remote execution
- [ ] CLI / config / packaging
- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [ ] Bug fix
- [x] Feature
- [ ] Refactor
- [x] Test / harness
- [x] Documentation
- [ ] Security-related change
- [ ] Release / packaging

## Verification

Ran:

```text
uv run pytest tests/test_protein_mutation_enhancement_skill.py -q
uv run pytest tests/test_skills.py -q
uv run pytest tests/test_protein_mutation_enhancement_skill.py tests/test_skills.py -q
uv run pytest
uv run pre-commit run --all-files
```

Results:

```text
tests/test_protein_mutation_enhancement_skill.py: 6 passed
tests/test_skills.py: 21 passed
combined focused tests: 27 passed
full offline suite: 1456 passed, 5 skipped, 1 deselected
pre-commit: passed
```

Not run:

```text
Live GPU ESM / ESMFold inference
Live LLM, network, SSH, Docker, or lab-hardware tests
```

Reason:

```text
This PR adds the deterministic stdlib workflow layer. Heavy model execution remains delegated to existing GPU/model skills and is intentionally outside the default offline test suite.
```

## Risk and Reviewer Focus

Risk is limited to skill discovery and the new workflow sidecar. No core engine, kernel protocol, host RPC, gateway, store, or web UI files are modified.

Please review:

- `skills/protein-mutation-enhancement/SKILL.md`
  - whether the workflow contract matches the intended protein mutation design loop;
  - whether the docs avoid overclaiming biological validation.
- `skills/protein-mutation-enhancement/kernel.py`
  - mutation parsing and 1-indexed position validation;
  - deterministic library enumeration and seeded expansion;
  - score normalization, weighting, thresholding, and next-round seed selection.
- `tests/test_protein_mutation_enhancement_skill.py`
  - offline coverage for enumeration, ranking, loop continuation, and next-position suggestion.
- `docs/skills.md`
  - bundled skill count and workflow catalog entry.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: `gateway.py`,
      `host_dispatch.py`, `store.py`, `app.js`, `worker.py`, `manager.py`.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not
      reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware,
      or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway changes include focused contract coverage or
      a documented smoke test.

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or
      stdlib web server.
- [x] Optional science imports are guarded by `try/except ImportError` at every
      in-tree use site.
- [x] New dependencies, if any, are documented and justified.

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model
      weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail,
      or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual
      verification notes.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security
      guarantees.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs or release notes where
      appropriate.
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are
      affected.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `97cfb34a7de7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.