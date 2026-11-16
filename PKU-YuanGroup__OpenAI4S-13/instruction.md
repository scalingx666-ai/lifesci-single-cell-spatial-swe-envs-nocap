# Issue

**Title:** add retrosynthesis planning skill

## Description

## Summary

Adds a new `retrosynthesis_planning` science Skill for industrial-style retrosynthesis route review.

This PR includes:

* AiZynthFinder command construction and route JSON loading.
* Route normalization and ranking helpers.
* Molecule brief extraction for targets, intermediates, stock precursors, and unresolved precursors.
* Optional conversation-LLM annotations for route-level, molecule-level, and reaction-level chemistry interpretation.
* A self-contained HTML dashboard with:

  * route ranking
  * molecule structure visualization
  * interactive retrosynthesis knowledge graph
  * route cards
  * reaction detail panels
* An aspirin example dashboard under the Skill directory.
* Offline tests covering:

  * Skill discovery
  * route normalization
  * HTML rendering
  * LLM annotation behavior
  * molecule visualization fallback
  * the aspirin example

## Area

* [ ] Web UI / frontend
* [ ] Agent / loop / delegation
* [ ] Kernel / host RPC / runtime
* [ ] Server / gateway / API
* [ ] Store / provenance / artifacts
* [x] Skills / science runtime
* [ ] Compute / remote execution
* [ ] CLI / config / packaging
* [x] Tests / harness / CI
* [x] Docs

## Change Type

* [ ] Bug fix
* [x] Feature
* [ ] Refactor
* [x] Test / harness
* [x] Documentation
* [ ] Security-related change
* [ ] Release / packaging

## Verification

### Ran

```text
uv run python -X faulthandler -m pytest -p no:capture tests/test_retrosynthesis_planning.py -vv

uv run pre-commit run --files \
  skills/retrosynthesis_planning/SKILL.md \
  skills/retrosynthesis_planning/kernel.py \
  skills/retrosynthesis_planning/examples/aspirin_retrosynthesis.html \
  tests/test_retrosynthesis_planning.py
```

### Not run

```text
Full test suite
Live AiZynthFinder search in CI
Live LLM annotation call
```

### Reason

The focused offline test suite covers the new Skill behavior without requiring live LLM access, network access, GPU, SSH, Docker, lab hardware, or secrets.

Live AiZynthFinder execution and LLM annotation depend on local user configuration and are documented as runtime paths rather than default CI tests.

## Risk and Reviewer Focus

### Main reviewer focus

#### `skills/retrosynthesis_planning/kernel.py`

* Route normalization across backend export shapes.
* HTML escaping and self-contained rendering.
* LLM annotation parsing and fallback behavior.
* RDKit optional import handling.

#### `skills/retrosynthesis_planning/SKILL.md`

* Whether the workflow documentation matches actual code behavior.
* Whether caveats around LLM-generated conditions and yields are clear enough.

#### `tests/test_retrosynthesis_planning.py`

* Whether offline coverage is sufficient.
* Whether tests remain independent of live services.

### Potential risks

* AiZynthFinder export schemas may vary beyond the normalized shapes covered here.
* LLM annotation quality depends on the configured conversation model.
* Route, condition, and yield annotations are treated as hypotheses, not validated experimental facts.
* RDKit is optional. If unavailable, the dashboard uses transparent local SVG placeholders rather than real molecule depictions.

## Checklist

### Diff Readiness

* [x] I reviewed and understand the full diff.
* [x] This PR is small and single-purpose.
* [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
* [x] Hotspot files were edited surgically if touched: `gateway.py`, `host_dispatch.py`, `store.py`, `app.js`, `worker.py`, `manager.py`.
* [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted.

### Tests

* [x] Relevant tests or manual checks were run and listed above.
* [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets in the default offline suite.
* [x] No tests were deleted without tracked replacements.
* [x] Kernel / host-RPC / gateway changes include focused contract coverage or a documented smoke test, where applicable.

### Core Dependency Policy

* [x] No hard third-party import was added to the core engine, LLM client, or stdlib web server.
* [x] Optional science imports are guarded by `try/except ImportError` at every in-tree use site.
* [x] New dependencies, if any, are documented and justified.

### Public Disclosure and Security

* [x] No secrets, API keys, tokens, real credentials, private data, model weights, or local absolute paths are included.
* [x] No unpublished research roadmap, internal assignment, benchmark detail, or unreleased experimental result is disclosed.
* [x] No security-sensitive behavior is changed in this PR.
* [x] Docs do not overstate isolation, sandboxing, privacy, or security guarantees.

### Docs

* [x] Docs match actual code behavior.
* [x] User-facing behavior changes are reflected in docs or release notes where appropriate.
* [x] `README.md` and `README_zh.md` stay in sync where translated sections are affected.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `19154c769a7a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.