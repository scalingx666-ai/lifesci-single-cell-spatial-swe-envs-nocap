# Issue

**Title:** feat(sandbox): preinstall the analysis stack in the image, keep what users install on the Volume

## Description

The stack the built-in skills import — scanpy, scvi-tools, Seurat, Bioconductor and about 800 other packages — now ships in the image. A user's own environment sits on the Volume and inherits from it, so `conda install`, `pip install` and `install.packages()` all persist while the heavy shared stack is never downloaded per workspace.

Before this, a workspace that wanted scanpy downloaded it. Every workspace. Every time one was created.

## What ships where

```
/opt/pantheon/envs/pantheon-base   the analysis stack, read-only, in the image
/opt/pantheon/envs/pyscenic        pySCENIC, which cannot share (numpy==1.23.5)
<volume>/.local/micromamba/envs/analysis   yours: writable, persistent, active
```

The personal environment is deliberately thin — pip and nothing else — and borrows the rest through a `.pth` bridge. That is what keeps first boot at ~70 s instead of the minutes a full R install was costing.

Named `pantheon-base` rather than `analysis`: two environments with one name left conda unable to show either by name and made `conda activate analysis` ambiguous.

## Measured on staging

| | |
|---|---|
| cold start | 26-32 s (1.64 GB image: 21 s) |
| image | 1.64 → 4.38 GB |
| keystroke latency | 44-46 ms |
| `conda env list` | base, analysis*, pantheon-base, pyscenic |
| `import scanpy, scvi, torch` | works from the personal env |
| `library(Seurat)` | 5.5.1 |
| `conda run -n pyscenic` | numpy 1.23.5, isolated |

**Cold start did not change.** Modal serves a prewarmed image from cache, so size does not enter that path — which is worth stating plainly, because the existing Dockerfile excludes squidpy and scvi-tools on the assumption that it does.

## Every build checks itself

Three checks, each from something that shipped broken:

- **the yml parses** — a colon in `--only-binary=:all:` made micromamba unable to read the file, and the error came from a YAML library with no filename in it
- **wheels only for dask-image and cython** — pip chose an sdist and died inside a build backend that never named which package it was building; three builds were spent not knowing
- **every listed module imports** — squidpy and decoupler both *solved* cleanly and then failed on import. It has since caught a package that silently failed to install and one that an edit had deleted from the list. It is the only check here that has been reliably right.

## Reconciled, not just created

Four things had to learn the same lesson: a marker saying "already set up" says nothing about being set up *the way this image sets things up*. The package set, the `.pth` bridge, the conda channels and `envs_dirs` are all now compared against what they should be on every boot, so an existing workspace repairs itself instead of staying on whatever the design was when it was created.

## Two crashes worth recording

**The agent died on every boot** with `cloudpickle` unable to parse conda's `sys.version`. The system python was loading conda's `libpython` — same binary, same md5, different library — because an `activate.d` hook an earlier version of this script had written *onto the Volume* was still running long after the code that wrote it was gone. Deleting code does not delete artifacts.

**Keystroke latency went from 64 ms to 220-515 ms** once a conda environment existed on the Volume. The workspace disk-usage walk traverses everything under `/workspace`, and one conda env is ~11k files on network storage. That walk had already been given a yield once; a yield bounds cost per entry and cannot bound an entry count that grew by two orders of magnitude. It now skips `.local`, which holds installed packages and never held anything a disk-usage figure was about.

**The baseline's lib directory is on no search path at all.** Exposing it broke two different things two different ways — the agent's libpython, then htop's ncurses. It holds a second copy of half the system's libraries. Only the libraries the loader actually reports missing are linked into the personal environment, found by asking rather than by denylist.

Also here: the `pantheon` CLI, which the image never had — `uv sync --no-install-project` means console scripts are never written, so the command did not exist in a terminal.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01BhPiGNfkhLZ89Sqhoz9ebP

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `24efe2593c59`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.