# Issue

**Title:** fix(frontend): bind the composer once Shell has rendered it

## Description

## Summary

Typing a message and pressing Enter in the workbench composer inserted a
newline and never sent anything; Cmd+Enter did nothing either, and the
composer has no send button. Only the dashboard example cards could start a
turn.

Cause: `frontend/src/features/send/index.ts` runs `installSend()` at module
import, which calls `bindComposer()`. That happens before `main.tsx` renders
`<App/>`, so `#composer`, `#plan-toggle` and `#explore-toggle` do not exist
yet; `bindComposer()` found nothing, bound nothing, and nothing ever tried
again. `bindComposerAutocomplete()` (`features/autocomplete/composer.ts`)
already handles exactly this ordering with a MutationObserver, which is why
`@`/`#`/`/` completion worked in the same textarea while Enter did not.

Fix: `bindComposer()` now mirrors that pattern. The first pass still binds
whatever is mounted; if `#composer` is not there yet, a MutationObserver on
`document.documentElement` (childList + subtree) retries on DOM changes and
disconnects once the composer carries the keydown handler. Repeat calls are
no-ops (module-level watch guard plus the existing `data-send-bound`
markers). No behaviour of the handler itself changed.

Introduced by the F-13 / F-11 port (`d28010ba` moved the composer into
`Shell.tsx`, `8ab17fb1` wired the send chain). No existing issue.

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
- [ ] Test / harness
- [ ] Documentation
- [ ] Security-related change
- [ ] Release / packaging

## Verification

Ran (against the current `main`, `e9370ef7`):

```text
npm test --prefix frontend                 # 61 files, 439 tests passed (3 new in send/bind.test.ts)
npm run build --prefix frontend            # strict tsc + vite; dist rebuilt, two consecutive builds byte-identical
uv run pre-commit run --files <changed files>  # end-of-file/line-ending/whitespace/merge-conflict/mypy passed
```

Manual, macOS 27.0 (26A5416b), Chromium-based browser, against a daemon
started with a fresh `OPENAI4S_DATA_DIR`:

- Before: `document.getElementById('composer').dataset.sendBound` is
  undefined after the workbench loads; a synthetic `keydown` Enter on the
  composer is not `defaultPrevented`; typing and pressing Enter only inserts a
  newline.
- After: `dataset.sendBound === "1"` on `#composer`, `#plan-toggle` and
  `#explore-toggle`; Enter in a session composer clears the box and issues
  `POST /api/v1/frames/<id>/message → 202 Accepted`, and the turn starts.

Not run:

```text
Full `uv run pytest` on this host
```

Reason:

```text
Only frontend sources and the committed dist changed. This branch is rebased
onto the current main; none of the six commits since the prior base touch
`frontend/src/features/send/`. The subset that reads the web UI / dist passes.
```

## Risk and Reviewer Focus

- `frontend/src/features/send/send.ts::bindComposer` / `bindComposerNow`:
  the observer's completion signal is "#composer is bound". The two mode
  toggles are rendered as static siblings of the composer in `Shell.tsx`, so
  they bind in the same pass; if they were ever moved into a later or
  conditional render they would need their own signal.
- Until the composer exists the observer sees every DOM mutation and runs
  three `getElementById` calls per batch; it disconnects on the first
  successful bind, same as the autocomplete watcher.
- A separate cosmetic issue (static labels stay as raw i18n keys when the
  locale chunk resolves after `Shell` mounts) was deliberately left out of
  this PR; a first attempt to re-apply `applyStaticI18n()` after load could
  clobber `#conv-title`, which `setTitle()` writes directly, so it needs its
  own change.
- Regression test: `frontend/src/features/send/bind.test.ts` (vitest, node
  environment, hand-made document/MutationObserver fakes in the style of
  `features/artifacts/boot.test.ts`).

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
      a documented smoke test. (n/a — none touched)

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or
      stdlib web server.
- [x] Optional science imports are guarded by `try/except ImportError` at every
      in-tree use site. (n/a — none added)
- [x] New dependencies, if any, are documented and justified. (none)

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model
      weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail,
      or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual
      verification notes. (n/a)
- [x] Docs do not overstate isolation, sandboxing, privacy, or security
      guarantees.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs or release notes where
      appropriate. (behavior now matches what the docs already describe)
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are
      affected. (n/a — untouched)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5f94e1c05197`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.