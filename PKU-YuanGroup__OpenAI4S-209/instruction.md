# Issue

**Title:** fix(workbench): keep focus a control already took inside a modal

## Description

## Summary

CI run [37190167862](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/37190167862/job/111400498789) (`next` @ `b7240802`) failed `Browser workbench E2E (chromium)` in the C5 diagnostics scene of `tests/browser_smoke.mjs`: the cleanup's `#cust-close` click waited 30s. Playwright's call log only says `waiting for locator('#cust-close')`, never "resolved to", so the button was not in the page at all. The same SHA was green twice on `main`. This is a timing flake, not a regression from #207.

I looped the real C5 scene locally, after C1/C3/C7, with a copy of the smoke file instrumented with a request/navigation timeline and original-error logging. That turned up two separate races.

**1. A modal's first focus stole a key press (product bug, ~3% of loops).** `openModalEl()` focuses the modal's first control, Settings' General tab, one animation frame late. Playwright's `press()` focuses the target and then sends the key as a separate step. When the frame landed between the two, Enter went to the General tab and remounted the pane, so Run checks never sent its request. The timeline shows no `/diagnostics/checks` POST, and the tab's GETs appear only once because Preact drops the pending effects of the instance it unmounted. A user whose focus reaches the modal before that frame hits the same thing. `frontend/src/features/chrome/modal.ts` now leaves focus alone when it is already on a control inside the modal.

**2. The cleanup reopened Settings just to close it (the failure CI hit).** After the reload, Settings is already closed, but the inner `finally` called `window.openCust()` again so the outer `finally` had a `#cust-close` to click. `openCust` returns before its lazily loaded chunk mounts the modal. Occasionally the modal never mounted, failing a scene whose assertions had all passed. I reproduced this once locally, but a stripped-down replay of just the cleanup sequence did not trigger it in 250 runs, so the precise mechanism is unconfirmed; the fix removes the path entirely. The cleanup no longer reopens Settings and closes it only if it is open.

`openai4s/server/webui/dist/` is rebuilt. The crosswalk row citing `browser_smoke.mjs` (R7/P1-04, the Notebook export selector) is re-recorded: this diff touches only the C5 scene, and those Notebook export assertions are unchanged.

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
- [ ] Docs

## Change Type

- [x] Bug fix
- [ ] Feature
- [ ] Refactor
- [x] Test / harness
- [ ] Documentation
- [ ] Security-related change
- [ ] Release / packaging

## Verification

Ran:

```text
# Reproduction: the real C5 block looped after C1/C3/C7, against a credential-less daemon
original C5, old dist   ~10 failures / ~300 iterations (focus race 9x, cleanup #cust-close 1x)
original C5, new dist   0 / 200   (cleanup still reopening Settings, so this isolates the modal fix)

npx vitest run src/features/chrome/modal.test.ts    # new case fails with the guard removed, passes with it
npm test --prefix frontend                          # 1402 passed
npm run build --prefix frontend                     # dist committed
node tests/browser_smoke.mjs                        # modified smoke, passed 2/2 against the rebuilt dist
uv run pre-commit run --all-files                   # passed
uv run python scripts/check_directory_readmes.py    # complete bilingual coverage
uv run python scripts/reaudit_crosswalk.py --check  # up to date after re-record
uv run pytest -n auto --maxprocesses=4 --dist loadfile   # 11311 passed, 34 skipped
```

Not run:

```text
node tests/browser_matrix.mjs (firefox / webkit), browser_admission_fault, browser_p1_controls,
browser_sandbox_preview, container smoke, harness tier, response schema/contract capture
```

Reason:

```text
No route, serializer, harness or packaging code changed; the other browser files do not exercise
the C5 scene. CI runs all of them on this PR.
```

## Risk and Reviewer Focus

- `modal.ts`: the first focus is now skipped when `document.activeElement` is a control inside the modal (not the modal or its `.modal-box`). Before this change it always moved focus to the default control. The only change in behaviour is that a control focused inside the modal before the frame keeps its focus. When a modal opens, focus starts outside it, because a hidden modal cannot hold focus.
- `browser_smoke.mjs` C5 cleanup: the scene now ends with Settings closed by the reload instead of reopened and closed. Nothing after C5 depends on Settings having been mounted.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: `gateway.py`,
      `host_dispatch.py`, `store.py`, `worker.py`, `manager.py`. (none touched)
- [x] Workbench changes were made in `frontend/` (not legacy `app.js`)
      and `openai4s/server/webui/dist/` was rebuilt and committed with the
      source.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not
      reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware,
      or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway changes include focused contract coverage or
      a documented smoke test. (not applicable)

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or
      stdlib web server.
- [x] Optional science imports are guarded by `try/except ImportError` at every
      in-tree use site. (none added)
- [x] New dependencies, if any, are documented and justified. (none)

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model
      weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail,
      or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual
      verification notes. (not applicable)
- [x] Docs do not overstate isolation, sandboxing, privacy, or security
      guarantees.

### Docs

- [x] Docs match actual code behavior. (`frontend/src/features/chrome/README.md` / `README_zh.md` rows for `modal.ts` and `modal.test.ts` updated)
- [x] User-facing behavior changes are reflected in docs or release notes where
      appropriate.
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are
      affected.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- CURSOR_SUMMARY -->
---

> [!NOTE]
> **Low Risk**
> Focused UX and test-harness changes in modal focus and browser smoke; rebuilt dist only reflects the modal fix.
>
> **Overview**
> Fixes modal focus stealing and a flaky browser smoke cleanup that caused CI timeouts.
>
> **Modal focus:** `openModalEl` still defers initial focus by one animation frame for async content, but it **no longer moves focus** when `document.activeElement` is already a control inside the modal. That prevents Enter intended for Settings diagnostics “Run checks” from landing on the first tab instead.
>
> **E2E (C5):** The diagnostics scene cleanup **stops reopening Settings** after reload and only clicks `#cust-close` when `#cust` is visible, avoiding waits on a lazily mounted close button.
>
> Also adds a `modal.test.ts` case, updates chrome README rows, rebuilds `webui/dist`, and re-records the crosswalk `evidence_digest` for the `browser_smoke.mjs` row.
>
> <sup>Reviewed by [Cursor Bugbot](https://cursor.com/bugbot) for commit d26af25247c9c925db4fd2b66906bd941a095e37. Configure [here](https://www.cursor.com/dashboard/bugbot).</sup>
<!-- /CURSOR_SUMMARY -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b7240802dc0f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.