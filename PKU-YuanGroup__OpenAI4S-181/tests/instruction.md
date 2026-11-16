# Issue

**Title:** feat(science): add STRING protein-protein interaction database connector

## Description

## Summary

Adds STRING interaction-partner searches to `science_search` and `host.science.search`, with species selection, a 0–1000 confidence threshold, and explicit functional or physical networks. Newline-separated protein identifiers survive request normalization. Results retain both STRING endpoints and all seven evidence-channel scores, with stable interaction IDs derived from the endpoint pair.

STRING is included in scientific-domain egress policy and progressive tool discovery. Invalid thresholds and species are rejected before a request; blank, null, and malformed responses remain errors. All eight returned confidence fields are checked for finite values in the 0–1 range: non-finite strings, booleans, nonnumeric values, and out-of-range scores produce a bounded connector error instead of invalid JSON or misleading evidence. Missing optional scores remain omitted. The connector returns at most `limit` records in upstream order and does not claim to retrieve a complete induced subnetwork. Its manifest, native schema, and documentation match these behaviors.

## Verification

- `uv run python scripts/capture_response_schemas.py --check`: the full offline suite on commit `b59ed076` passed (10096 passed, 30 skipped on macOS); all 213 routes were exercised, with 1174 route/status shapes and no breaking change to the frozen response shapes.
- Connector, manifest, native-tool, discovery, and egress regression tests: 191 passed, 1 skipped, including malformed-score rejection across all eight confidence fields and the native tool's error envelope.
- `uv run pre-commit run --all-files`: passed, including strict mypy.
- `uv run python -m harness.cli run --tier pr --offline`: all 38 scenarios passed.
- `uv run python scripts/check_directory_readmes.py`: passed.
- `uv run python scripts/source_secret_scan.py`: passed.
- `uv run python scripts/capture_response_contract.py --check`: 213/213 routes current.
- Separate live API smoke: a TP53 physical-network query returned two records through the real fetch path with egress allowlisting enabled and a recorded response hash; the result also serialized with `allow_nan=False`. Default tests remain offline.

## Reviewer focus

GitHub Actions for the latest commit still require fork-workflow approval: [CI](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/35623920485) and [Protocol fuzzing](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/35623920561).

Review `openai4s/host/science.py` for query and interaction semantics, `openai4s/tools/catalog.py` for discovery, and `openai4s/egress.py` for the domain boundary. Lookalike STRING hosts remain blocked. Validation was performed on macOS; Linux/container/browser gates were not run for this connector-only change.

## Checklist

- [x] Full diff reviewed; changes remain scoped to the STRING connector and its integration.
- [x] No hard third-party core dependency, real credential, or private data added.
- [x] No hotspot facade rewrite, vendored-file reformatting, or test deletion.
- [x] Default tests are offline, and stubbed connector tests carry `stubbed_backend`.
- [x] Documentation matches the implemented query, limit, score, and failure semantics; no translated root README section changed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6c9a15c75092`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.