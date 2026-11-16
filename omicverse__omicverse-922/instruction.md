# Issue

**Title:** fix(single): tell users when CopyKAT's genome tables are missing

## Description

.

## Root cause — it is a pycopykat packaging bug

`pycopykat/io/annotation.py` resolved its reference tables as

```python
Path(__file__).resolve().parents[2] / "data"
```

From a source checkout (`<repo>/pycopykat/io/annotation.py`) that is the repo root, where `data/` really lives. From an installed package (`site-packages/pycopykat/io/annotation.py`) it is **`site-packages/data/`** — which is why the reporter saw

```
FileNotFoundError: .../site-packages/data/hg20_gene_anno.parquet
```

and why "查看 omicverse 目录也没有 data 文件夹" — the tables were never in omicverse, and were not in the pycopykat wheel either (`packages = ["pycopykat"]`, `data/` outside it).

Upstream fix: **omicverse/py-CopyKAT#4** moves the four tables to `pycopykat/data/` so the wheel carries them. Merge that first; this PR is the omicverse-side half.

## What this PR changes

`_check_dep("copykat")` now probes for the tables right where the backend is imported and raises

```
ImportError: pycopykat is installed but its genome reference tables
(hg20/mm10 *_gene_anno.parquet) are missing — looked in .../pycopykat/data.
Installs predating pycopykat 0.1.0.dev2 did not ship them. Reinstall with:
  pip install -U git+https://github.com/omicverse/py-CopyKAT.git
```

instead of letting `CNV.run()` start work and then die inside `pandas.read_parquet` with a path nobody can act on. The probe accepts both layouts — `pycopykat/data/` (fixed wheel) and `<repo>/data/` (existing editable checkouts) — so it mirrors pycopykat's own resolution exactly and never fires on a working install.

## Verification

- Reproduced the original failure mode: the environment here had `site-packages/data/` hand-copied as a workaround, i.e. the exact layout the old `parents[2]` expression needs. Deleting that assumption is what the guard now detects.
- Built the fixed pycopykat wheel, unpacked into a clean `site-packages`-shaped directory, and confirmed the guard passes against it and `_data_dir()` resolves to `.../pycopykat/data`.
- New `tests/single/test_cnv_copykat_data.py` — 4 tests covering the packaged layout, the legacy checkout layout, the broken install, and that the message names the reinstall command.
- `pytest tests/single` → **155 passed**.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01VVqVNig3oV6wz42YiQ9obZ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `23a4ebe3e19f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.