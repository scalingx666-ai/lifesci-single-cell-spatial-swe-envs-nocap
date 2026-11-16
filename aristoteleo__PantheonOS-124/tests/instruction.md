# Issue

**Title:** Notebook cwd + skill resolution + template/file-viewer fixes

## Description

Five focused fixes from this session (each its own commit):

- **anthropic-adapter** — skip empty messages so a tool-approval-only turn no longer triggers Anthropic 400 `messages must have non-empty content`.
- **learning-system** — resolve nested skills by leaf/partial path (forgiving fallback across project → global → factory, refusing ambiguous matches), so an agent following a `SKILL.md`'s relative links (e.g. `database_access/SKILL.md`, `sc_best_practices/chromatin_accessibility.md`) resolves to the nested skill instead of "not found"; not-found errors now suggest the correct `skill_view(...)` call. +9 regression tests.
- **notebook** — start the kernel in the notebook's own directory, so a relative path like `savefig("figures/x.png")` lands next to the `.ipynb` instead of the workspace root (standard Jupyter behaviour; falls back to the workspace workdir when unset).
- **templates** — extract the default team leader's "Notebooks vs. Scripts" guidance into a shared `prompts/jupyter_notebook.md` (included via `{{jupyter_notebook}}`), plus the notebook file-path rule.
- **file-manager** — resolve `.pantheon/{prompts,teams,agents}/*.md` through layer precedence in `read_file`, so the file viewer (and agent) can open a prompt/team/agent that only lives in a higher layer instead of "File does not exist". Read-only, namespace-scoped, no path traversal; a project-level copy still wins.

Tests: learning-system 114 passed, file_manager 12 passed, notebook-cwd e2e verified.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f288f826808a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.