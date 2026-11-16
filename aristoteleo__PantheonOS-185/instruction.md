# Issue

**Title:** fix(live_view): expose browser frame X-* headers to cross-origin JS

## Description

. The Browser app reads each page's nav state (`X-Url` / `X-Title` / `X-Loading` / `X-Back` / `X-Fwd`, and the frame `X-Seq`) off the `browser-frame` response headers. Cross-origin JS can't read custom response headers unless the server lists them in `Access-Control-Expose-Headers` — and browsers do **not** honour a bare `*` there — so they arrived invisible and in-page navigation never updated the address bar or back/forward state.

Lists them explicitly in the data server's CORS middleware. Initial url/title were unaffected (they ride the same-origin `browser_ui_page` RPC response). Verified on staging: real Chromium page renders + streams; this makes the toolbar follow in-page navigation too.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3dc2a5833212`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.