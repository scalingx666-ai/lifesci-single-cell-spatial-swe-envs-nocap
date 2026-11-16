# Issue

**Title:** docs: macOS DMG startup guide + README refresh (unblocks stale PyPI-publish governance tests)

## Description

## Summary

Adds a **bilingual (EN/ZH) startup guide** for the v0.1.0 macOS `.dmg` release and refreshes the READMEs so a first-time DMG user has a clear path from download to first result. It also **unblocks a pre-existing CI failure on `main`** (details below) so this branch — and every other branch — can go green.

### Docs (the main change)

- **New: `docs/startup-guide.md`** — a 6-step walkthrough in English and 简体中文:
  1. Install — drag `OpenAI4S` to Applications
  2. First launch — clear Gatekeeper (macOS 15+ / 12–14 / `xattr` paths)
  3. Configure the **model API** — Settings → Models → pick protocol → paste key → Set active (with a provider/key table incl. Volcengine Ark ¥9.9/mo)
  4. Configure the **web-search API** — Settings → Network → register at [tavily.com](https://tavily.com) → paste Tavily key
  5. (Optional) add the R kernel via the bundled CLI + `openai4s setup`
  6. First question + troubleshooting

  UI labels were verified directly against `openai4s/server/webui/app.js` so the Chinese wording matches the actual interface. Cross-language switching uses explicit `<a id>` anchors.

- **`README.md` / `README_zh.md`** — new `2026-07-15` News entry for the v0.1.0 macOS app; a compact "First run" block (model + Tavily search) plus a pointer to the full guide; a "Startup guide" row in the Documentation table; `README_zh` footer now carries the friend link (EN/ZH parity).
- **`docs/README.md` / `docs/README_zh.md`** — index the new guide.

A README currency audit against the codebase confirmed the rest is already accurate (32 bundled Skills, provider list, roadmap), so no other content was churned.

### Also in this PR — fix a stale governance gate

`main` has been red for every branch since #34: that PR intentionally switched the PyPI publish step to `pypa/gh-action-pypi-publish@release/v1` (a Docker-container action whose image PyPA only publishes tagged by *release* ref — a commit-SHA pin fails the image pull with `manifest unknown` before the OIDC exchange runs), but two governance tests still asserted the old SHA pin. They failed independently of this PR's docs (verified: the same two tests fail on `origin/main`). Bundled here to unblock merge:

- **`tests/test_governance.py`** — still requires every action to be SHA-pinned, but allows the single, exactly-specified `pypa/gh-action-pypi-publish@release/v1` line. Any other moving ref (including a different ref of the same action) still fails, so the security property is preserved.
- **`tests/test_release_gates.py`** — asserts the publish step is on `release/v1` instead of the removed commit SHA.

No workflow/production code changed; only the two test assertions were realigned with the already-merged, documented workflow decision. **Full offline suite passes locally** (1592+ passed).

## Area

- [x] Docs
- [x] Tests / harness / CI

## Change Type

- [x] Documentation
- [x] Test / harness
- [x] Security-related change

## Testing

`uv run pytest` — full offline suite green locally; `tests/test_governance.py` + `tests/test_release_gates.py` pass. Docs are inspection-verified: intra-doc anchors, cross-file links, EN/ZH parity, and pre-commit hooks (end-of-files, trailing-whitespace, black, isort, ruff, mypy).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c25f022c5f49`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.