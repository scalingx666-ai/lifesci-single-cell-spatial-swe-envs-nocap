# Issue

**Title:** feat(browser): a real Chromium, shared by the agent and the desktop

## Description

## What

A **real browser** in the sandbox, streamed to the Atrium desktop and driven by the agent — the same page for both. The agent can open a page for the user, the user logs in, the agent carries on authenticated.

No iframe: main-site anti-embedding (`X-Frame-Options`, CSP `frame-ancestors`) makes iframes a dead end. This is one headless Chromium (Playwright persistent context) rendered via CDP `Page.startScreencast` and streamed as JPEG frames.

## Pieces

- **`browser.py`** — `BrowserEngine` on its own daemon loop (Playwright objects are loop-bound; tool calls run on ephemeral per-call loops and endpoint handlers on the data-server loop, so both marshal in via `run_coroutine_threadsafe`). Two data-server endpoints:
  - `browser-frame` — long-poll: a request parks until the page next repaints (idle pages cost nothing), nav state in `X-Url`/`X-Title`/`X-Loading`/`X-Back`/`X-Fwd` headers.
  - `browser-input` — batched pointer/key/wheel/resize events.
  - Popups fold back into the same page (the streamed window is the user's only surface); persistent profile so logins survive a page close.
- **`toolset.py`** — agent tools `browser_open` / `browser_goto` / `browser_read` / `browser_click` / `browser_type` / `browser_screenshot` / `browser_pages` / `browser_close`; `browser_ui_*` (excluded) for the Atrium window. `browser_open` also opens the desktop Browser window via `desktop.open` state, so "show the user a page" is one call.
- **`Dockerfile`** — `fonts-noto-cjk` (CJK pages render, not tofu). Playwright + Chromium already install (crawl4ai pulls `playwright`; `playwright install chromium --with-deps` is an existing layer) — so no image-size surprise beyond the fonts.
- **desktop `SKILL.md`** — a section on the shared browser.

The Atrium `Browser` app that consumes this is in `pantheon-atrium` (companion change).

## Verification

Engine tested off-sandbox against real Chromium: thread marshal, screencast frames (15KB JPEG), click-navigation (example.com → iana.org), back, keyboard typing, viewport-resize re-negotiation — all green. Full end-to-end (agent + streamed desktop window) verified on staging after the image builds.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3142434b9b3a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.