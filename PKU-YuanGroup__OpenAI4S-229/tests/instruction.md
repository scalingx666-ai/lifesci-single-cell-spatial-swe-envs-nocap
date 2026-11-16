# Issue

**Title:** build(deps): bump source-map-js from 1.2.1 to 1.2.2 in /frontend

## Description

## Summary

Updates the build-only Vite/PostCSS dependency `source-map-js` from 1.2.1 to 1.2.2, including the upstream fix for malformed and deeply nested indexed source maps ([upstream changelog](https://github.com/7rulnik/source-map-js/blob/v1.2.2/CHANGELOG.md)). The package URL and integrity match npm's published 1.2.2 metadata.

The branch includes `main` at `c41b2c3f`. The net diff is still only three replacement lines in `frontend/package-lock.json`. Review found no additional product defect requiring a code change; rebuilding with the updated dependency leaves the committed workbench byte-identical.

## Area

- [x] Web UI / frontend build dependencies

## Change Type

- [x] Bug fix
- [x] Security-related dependency update

## Verification

Validated commit: `b9cbcf97de591a4715bcb2af9981dfd47c808e6a`.
Local runtime: Node 24.21.0 and Python 3.13.15.

```text
npm ci --prefix frontend --no-audit --no-fund
npm ls --prefix frontend source-map-js
npm test --prefix frontend
npm run build --prefix frontend
git diff --exit-code -- openai4s/server/webui/dist
uv run --no-sync pytest -n auto --maxprocesses=4 --dist loadfile
uv run --no-sync pre-commit run --all-files
uv run --no-sync python scripts/check_directory_readmes.py
uv run --no-sync python3 -m harness.cli run --tier pr --offline
uv run --no-sync python scripts/capture_response_contract.py --check
uv run --no-sync python scripts/capture_response_schemas.py --check
uv run --no-sync python scripts/source_secret_scan.py
node tests/browser_smoke.mjs
git diff --check
```

- Frontend: **1,555 tests passed in 144 files**; both TypeScript checks and the production build passed; no committed-dist drift.
- Full offline Python suite: **11,424 passed, 34 skipped, 0 failed**. Two expected warnings exercise mocked unsupported-platform sandbox paths.
- All pre-commit hooks passed, including strict mypy. Documentation coverage, all 38 offline harness scenarios, all 215 route contracts, and the source credential scan passed.
- Full local response capture passed with **1,198 route/status shapes and 215/215 routes covered**; the full suite again passed 11,424 tests with no breaking change to frozen response shapes.
- Real Chromium workbench smoke passed against a disposable loopback daemon with an isolated data directory, including immutable artifact versions, figures, error recovery, and session isolation. The daemon was stopped afterward.
- A one-off dependency smoke passed source-map round trips, sorting with dynamic code generation disabled, invalid and cumulative section offsets, deeply nested sections, and PostCSS source-map integration.

Latest hosted checks: **33 successful, 4 skipped, 0 pending or failed** ([CI run](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/38583648012)). The skips are the Dependabot branch-name exemption and three nightly-only jobs. Python 3.10/3.12/3.13/3.14 suites, Chromium/Firefox/WebKit, packaging, Linux sandbox checks, CodeQL, and automated security review passed.

The first hosted response-capture attempt stopped before comparison when the existing 50-session attention latency test recorded p95 456.7 ms against its 200 ms budget. No code or threshold was changed. Three capture-enabled local repetitions passed at p95 6.0, 10.1, and 8.4 ms, followed by the successful full local capture above. The [unchanged-head hosted retry](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/38583648012/job/115930832627) passed: **11,380 passed, 78 skipped; 1,198 captured shapes; 215/215 routes; no breaking schema change**. The initial timing failure remains documented here rather than being represented as a code fix.

Not run locally: hosted-only Linux/Windows checks, container/wheel packaging, and the full Firefox/WebKit matrix. Their results are covered by the linked CI run.

## Risk and Reviewer Focus

Review `frontend/package-lock.json`: version, registry URL, integrity, and the retained `dev: true` classification. The dependency remains confined to the frontend build toolchain. No application source, Python core dependency, user-facing behavior, or committed build output changes are introduced.

## Checklist

- [x] Full diff reviewed; small and single-purpose, with no unrelated edits or broad rewrites.
- [x] Hotspot facades were not modified; legacy UI, vendored files, and captured fixtures were not reformatted.
- [x] Workbench build was regenerated and verified identical to committed output.
- [x] Full offline tests, relevant frontend/browser checks, lint, and strict type checks passed; no tests were deleted.
- [x] No live LLM, external-service, GPU, SSH, or hardware dependency was added to the default suite.
- [x] No hard third-party import was added to the core; optional science import behavior is unchanged.
- [x] Dependency update is justified above; no secrets, credentials, private data, local paths, or unpublished plans are included.
- [x] Documentation and translated README behavior remain accurate; no user-facing documentation changes are required.

Code Owner approval remains required by repository policy. No approval or merge is claimed by this verification record.

<details>
<summary>Original Dependabot release details</summary>

Bumps [source-map-js](https://github.com/7rulnik/source-map-js) from 1.2.1 to 1.2.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/7rulnik/source-map-js/releases">source-map-js's releases</a>.</em></p>
<blockquote>
<h2>v1.2.2</h2>
<ul>
<li>
<p>Fix crash when executing in browser with CSP script-src that don't permit unsafe-eval (<a href="">#29</a>) <a href="https://github.com/xfournet"><code>@​xfournet</code></a></p>
</li>
<li>
<p>Fix denial of service from malicious indexed source maps (CVE-2026-93749) (<a href="">#79</a>)</p>
<p>Reported by <a href="https://github.com/waydeshi"><code>@​waydeshi</code></a> in <a href="">#76</a>. A fix was also proposed by <a href="https://github.com/aniebiet"><code>@​aniebiet</code></a> in <a href="">#78</a>.</p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/7rulnik/source-map-js/blob/main/CHANGELOG.md">source-map-js's changelog</a>.</em></p>
<blockquote>
<h2>1.2.2</h2>
<ul>
<li>
<p>Fix crash when executing in browser with CSP script-src that don't permit unsafe-eval (<a href="">#29</a>) <a href="https://github.com/xfournet"><code>@​xfournet</code></a></p>
</li>
<li>
<p>Fix denial of service from malicious indexed source maps (CVE-2026-93749) (<a href="">#79</a>)</p>
<p>Reported by <a href="https://github.com/waydeshi"><code>@​waydeshi</code></a> in <a href="">#76</a>. A fix was also proposed by <a href="https://github.com/aniebiet"><code>@​aniebiet</code></a> in <a href="">#78</a>.</p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>0a1d334</code></a> 1.2.2</li>
<li><a href=""><code>4c6fa26</code></a> Update changelog</li>
<li><a href=""><code>cf76580</code></a> Fix denial of service from malicious indexed source maps (CVE-2026-93749) (<a href="">#79</a>)</li>
<li><a href=""><code>7899a86</code></a> Fix crash when executing browser with CSP script-src that don't permit unsafe...</li>
<li>See full diff in <a href="https://github.com/7rulnik/source-map-js/compare/v1.2.1...v1.2.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=source-map-js&package-manager=npm_and_yarn&previous-version=1.2.1&new-version=1.2.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

Dependabot will resolve any conflicts with this PR as long as you don't alter it yourself. You can also trigger a rebase manually by commenting `@dependabot rebase`.

[//]: # (dependabot-automerge-start)
[//]: # (dependabot-automerge-end)

---

<details>
<summary>Dependabot commands and options</summary>
<br />

You can trigger Dependabot actions by commenting on this PR:
- `@dependabot rebase` will rebase this PR
- `@dependabot recreate` will recreate this PR, overwriting any edits that have been made to it
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/PKU-YuanGroup/OpenAI4S/network/alerts).

</details>

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c41b2c3f7a74`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.