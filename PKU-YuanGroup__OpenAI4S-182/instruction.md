# Issue

**Title:** feat(science): add BindingDB drug-target binding affinity connector

## Description

### Summary
Adds a dedicated science database connector for **BindingDB** (`bindingdb.org`), enabling biological and chemical agents to search for experimentally measured drug-target binding affinities ($K_i, K_d, IC_{50}, EC_{50}$) and active ligand chemical structures.

### Changes
- `openai4s/host/science.py`: Registered `"bindingdb"` in `DATABASES`, added `"cutoff"` (affinity threshold in nM) and `"affinity_type"` (`Ki`, `IC50`, `Kd`, `EC50`) filters, implemented `_search_bindingdb` with auto-routing between UniProt accession (`getLigandsByUniprots`) and 4-character PDB code (`getLigandsByPDBs`), and normalized results into standard `bioactivity` records with SMILES, numerical values, and literature citations.
- `openai4s/host/connector_manifest.py`: Declared `ConnectorManifest` with load-bearing required path `monomerid` and expected property paths.
- `openai4s/tools/science.py`: Added `"bindingdb"` to `ScienceSearchTool` enum and updated filter parameters schema.
- `docs/science-connectors.md`: Documented BindingDB in supported databases table and added detailed query routing and filter usage documentation.
- `tests/test_science_connectors.py`: Added offline mock fixtures, parameterized connector test, and 3 dedicated unit tests for metadata parsing, PDB routing, affinity filtering, and input validation.
- `tests/test_connector_manifests.py`: Added `"bindingdb"` probe for mutation testing.

### Verification
- Zero new external runtime dependencies (pure Python standard library).
- `pytest tests/test_science_connectors.py tests/test_connector_manifests.py tests/test_science_control_tools.py`: 171 passed, 1 skipped.
- `mypy`: 0 type issues found.
- `python scripts/check_directory_readmes.py`: All directory bilingual READMEs check passed.
- `python scripts/source_secret_scan.py`: 3923 files scanned, passed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b61dd7e9e095`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.