# Issue

**Title:** fix(webui): preserve BED coordinates during genome format detection

## Description

## Summary

. The genome-track viewer treated BED8–12 records as VCF or GFF, changing their coordinates or dropping them. A recognised extension now determines the format for the whole file, so `example.bed` retains the interval `[100, 200)`, its label, strand, and score.

For missing or unknown extensions, format inference requires VCF reference bases and quality fields, or GFF integer coordinates and strand. This also preserves BED6+N records with a missing score, base-like name, or strand-like custom columns. Regression tests cover those cases, consecutive records, numeric-source GFF, and VCF quality spellings supported by the [VCF specification](https://github.com/samtools/hts-specs/blob/master/VCFv4.4.tex).

The shared parser is served as a classic script; no frontend source or compiled bundle changed. The bilingual web UI docs explain the filename policy and the limits of content inference.

## Area

- [x] Web UI / frontend
- [ ] Agent / loop / delegation
- [ ] Kernel / host RPC / runtime
- [ ] Server / gateway / API
- [ ] Store / provenance / artifacts
- [ ] Skills / science runtime
- [ ] Compute / remote execution
- [ ] CLI / config / packaging
- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [x] Bug fix
- [ ] Feature
- [ ] Refactor
- [x] Test / harness
- [x] Documentation
- [ ] Security-related change
- [ ] Release / packaging

## Verification

Ran on macOS with Node 24 and Python 3.13 after merging current `main` (`4af99ba2`):

```text
node tests/scientific_renderers_smoke.cjs
# Passed. The added custom-BED regression fails on the previous PR head.
# Independently removing each of the four new format checks makes the smoke fail.

uv run pre-commit run --all-files
# Passed, including strict mypy and CSS checks.
uv run --no-sync python scripts/check_directory_readmes.py
# 171 maintained directories: complete bilingual coverage.
.venv/bin/python scripts/source_secret_scan.py
# Passed.
uv run --no-sync python -m harness.cli run --tier pr --offline
# 38 passed (26 contract-only, 12 production-backed), 0 failed.
uv run --no-sync python scripts/capture_response_contract.py --check
# 215/215 routes, up to date.

node tests/browser_smoke.mjs
# Passed against an isolated local daemon started through ./start.sh.
```

Additional real Chromium workbench validation uploaded and opened seven artifacts: BED8, BED12, custom BED6+N, VCF, numeric-source GFF3, GTF, and bedGraph. Asserted rendered format, coordinates, feature type, label, SVG feature count, and no page errors. Three unnamed custom-BED regressions also passed using the parser actually loaded by the browser.

`uv run --no-sync pytest -n auto --maxprocesses=4 --dist loadfile`: **11,382 passed, 34 skipped**, 2 warnings from platform-simulation tests, in 554.41 seconds. The suite ran with normal macOS process/sandbox capabilities and temporary application data.

Hosted checks on `13c49c8c`: **34 successful, 0 failures, 0 pending**. This includes all four Python versions (3.10/3.12/3.13/3.14), frozen response shapes, all three browser engines, lint, CodeQL, packaging, the container smoke, and both Linux sandbox jobs. Three scheduled-only jobs were skipped. Cursor Bugbot was neutral because its usage limit prevented a run; it is not counted as a successful review. [CI run](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/38230894226)

Merge readiness: synchronized with current `main`, no conflicts or unresolved review threads. GitHub still reports `BLOCKED` and no approving reviews; the required Code Owner review remains outstanding.

Not run locally: the frontend unit suite/rebuild (no frontend source or dist changes), frozen response-schema capture (no route/serializer changes), and Linux-only sandbox/container jobs. Hosted CI covers these independent gates. The legacy UI was not separately driven in a browser.

## Risk and Reviewer Focus

- Review `genomeFormatFromName`, `sniffGenomeFormat`, and the format-selection gate in `parseGenome`. Existing BED/VCF/GFF coordinate projection code is unchanged.
- Recognised filename extensions are authoritative, including when content disagrees with the name.
- Content inference remains a heuristic: custom fields can resemble another format. Use a recognised extension for ambiguous input. This change is not a complete format validator.
- The parser regression is Node-only and uses synthetic data. No new runtime dependencies, live scientific services, or credentials are involved.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched. None were touched by this fix.
- [x] Workbench changes respect the frontend boundary. Only the shared classic parser changed; no legacy `app.js` or Vite source/dist changes were needed.
- [x] Vendored assets and captured fixtures were not reformatted.

### Tests

- [x] Relevant tests and manual checks are listed above.
- [x] New tests require no live network, LLM, GPU, SSH, Docker, lab hardware, or secrets.
- [x] No tests were deleted.
- [x] No kernel / host-RPC / gateway behavior changed.

### Core Dependency Policy

- [x] No hard third-party import was added to core.
- [x] No optional science import sites changed.
- [x] No dependencies were added.

### Public Disclosure and Security

- [x] No secrets, real credentials, private data, weights, or local absolute paths are included.
- [x] No unpublished research plans or experimental results are disclosed.
- [x] Regression data is synthetic.
- [x] Docs make no additional security or isolation claims.

### Docs

- [x] Docs match actual behavior and describe the content-inference limitation.
- [x] User-facing filename behavior is documented.
- [x] English and Chinese documentation stay in sync.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4af99ba25abd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.