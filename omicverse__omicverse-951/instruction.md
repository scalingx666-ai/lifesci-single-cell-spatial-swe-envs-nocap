# Issue

**Title:** fix(pl): add CJK font fallback to plot_set

## Description

. plot_set now accepts fallback_font_path, resolves custom fonts by file path or family name, keeps the requested font first, and appends SimHei / Microsoft YaHei / Noto Sans CJK SC fallbacks for missing Chinese glyphs. Scanpy defaults also keep a CJK fallback chain.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c30f9a6ef7a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.