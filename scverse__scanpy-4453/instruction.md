# Issue

**Title:** test: bump the pre-commit group with 2 updates

## Description

Bumps the pre-commit group with 2 updates: [https://github.com/astral-sh/ruff-pre-commit](https://github.com/astral-sh/ruff-pre-commit) and [https://github.com/zizmorcore/zizmor-pre-commit](https://github.com/zizmorcore/zizmor-pre-commit).

Updates `https://github.com/astral-sh/ruff-pre-commit` from v0.17.0 to 0.17.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ruff-pre-commit/releases">https://github.com/astral-sh/ruff-pre-commit's releases</a>.</em></p>
<blockquote>
<h2>v0.17.1</h2>
<p>See: <a href="https://github.com/astral-sh/ruff/releases/tag/0.17.1">https://github.com/astral-sh/ruff/releases/tag/0.17.1</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>38bfb07</code></a> Mirror: 0.17.1</li>
<li>See full diff in <a href="https://github.com/astral-sh/ruff-pre-commit/compare/v0.17.0...v0.17.1">compare view</a></li>
</ul>
</details>
<br />

Updates `https://github.com/zizmorcore/zizmor-pre-commit` from v1.30.1 to 1.31.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/zizmorcore/zizmor-pre-commit/releases">https://github.com/zizmorcore/zizmor-pre-commit's releases</a>.</em></p>
<blockquote>
<h2>v1.31.1</h2>
<p><a href="https://github.com/sponsors/woodruffw/">Sponsorship is appreciated!</a></p>
<h2>Bug Fixes 🐛<a href="https://docs.zizmor.sh/release-notes/#bug-fixes">🔗</a></h2>
<ul>
<li>Fixed a regression in <a href="https://docs.zizmor.sh/release-notes/%5B#1310%5D()">1.31.0</a> where some ignore comments/configurations would no longer apply to the <a href="https://docs.zizmor.sh/audits/#dangerous-triggers">dangerous-triggers</a> audit (<a href="">#2450</a>)</li>
</ul>
<h2>v1.31.0</h2>
<p><a href="https://github.com/sponsors/woodruffw/">Sponsorship is appreciated!</a></p>
<h2>Enhancements 🌱<a href="https://docs.zizmor.sh/release-notes/#enhancements">🔗</a></h2>
<ul>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#typosquat-uses">typosquat-uses</a> audit now supports pre-commit config inputs (<a href="">#2437</a>)</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#self-hosted-runner">self-hosted-runner</a> audit is now significantly more precise (<a href="">#2350</a>)</p>
<p>Many thanks to <a href="https://github.com/ubiratansoares"><code>@​ubiratansoares</code></a> for proposing and implementing this enhancement!</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#dangerous-triggers">dangerous-triggers</a> audit now considers the issue_comment trigger fundamentally dangerous (<a href="">#2396</a>)</p>
</li>
<li>
<p>zizmor is now aware of the image_version workflow trigger (<a href="">#2397</a>)</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#dangerous-triggers">dangerous-triggers</a> audit now produces more precise finding/diagnostic spans (<a href="">#2402</a>)</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#cache-poisoning">cache-poisoning</a> audit is now aware of <a href="https://github.com/pnpm/setup">pnpm/setup</a> (<a href="">#2409</a>)</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#unpinned-images">unpinned-images</a> audit now produces more precise findings when the user's workflow contains an indirect matrix (<a href="">#2395</a>)</p>
<p>Many thanks to <a href="https://github.com/ubiratansoares"><code>@​ubiratansoares</code></a> for proposing and implementing this enhancement!</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#cache-poisoning">cache-poisoning</a> audit is now aware of GitHub's new cache-mode: setting, and will skip any findings that would occur when a job has an effective cache-mode: none (<a href="">#2418</a>)</p>
</li>
<li>
<p>The <a href="https://docs.zizmor.sh/audits/#cache-poisoning">cache-poisoning</a> audit now flags usages of cache-mode: write and cache-mode: write-only with dangerous triggers, i.e. triggers that give an attacker privileged code execution (<a href="">#2426</a>)</p>
</li>
<li>
<p>zizmor now uses a tree-sitter grammar for PowerShell that's more precise/capable of capturing more non-trivial PowerShell expressions (<a href="">#2444</a>)</p>
</li>
</ul>
<h2>Bug Fixes 🐛<a href="https://docs.zizmor.sh/release-notes/#bug-fixes">🔗</a></h2>
<ul>
<li>
<p>Fixed a class of false positives/imprecisions in <a href="https://docs.zizmor.sh/audits/#adhoc-packages">adhoc-packages</a> that caused some pnpm and yarn invocations to be misclassified as package installations (<a href="">#2386</a>)</p>
<p>Many thanks to <a href="https://github.com/marcalexiei"><code>@​marcalexiei</code></a> for implementing this improvement!</p>
</li>
<li>
<p>Fixed a bug where zizmor would fail to honor Git submodules and worktrees when discovering configuration files relative to a repo root (<a href="">#2390</a>)</p>
</li>
<li>
<p>Fixed a bug where the <a href="https://docs.zizmor.sh/audits/#ref-version-mismatch">ref-version-mismatch</a> audit would crash on unusually placed version comments (<a href="">#2394</a>)</p>
</li>
<li>
<p>Fixed a bug where zizmor would fail to handle some pre-commit inputs that use prek extensions to the language_version and default_language_version keys (<a href="">#2413</a>)</p>
</li>
<li>
<p>Fixed a bug where the <a href="https://docs.zizmor.sh/audits/#use-trusted-publishing">use-trusted-publishing</a> audit would fail to detect certain true-positive patterns inside of PowerShell blocks (<a href="">#2444</a>)</p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>c92afdf</code></a> Mirror: 1.31.1</li>
<li><a href=""><code>d25b2b1</code></a> Mirror: 1.31.0</li>
<li><a href=""><code>04df6d7</code></a> chore: drop Python 3.10 support (EOL) (<a href="">#65</a>)</li>
<li><a href=""><code>fe0957c</code></a> Bump astral-sh/setup-uv from 10.1.0 to 10.2.0 in the github-actions group (<a href="">#64</a>)</li>
<li><a href=""><code>de807da</code></a> Bump the github-actions group with 2 updates (<a href="">#63</a>)</li>
<li>See full diff in <a href="https://github.com/zizmorcore/zizmor-pre-commit/compare/v1.30.1...v1.31.1">compare view</a></li>
</ul>
</details>
<br />

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
- `@dependabot ignore <dependency name> major version` will close this group update PR and stop Dependabot creating any more for the specific dependency's major version (unless you unignore this specific dependency's major version or upgrade to it yourself)
- `@dependabot ignore <dependency name> minor version` will close this group update PR and stop Dependabot creating any more for the specific dependency's minor version (unless you unignore this specific dependency's minor version or upgrade to it yourself)
- `@dependabot ignore <dependency name>` will close this group update PR and stop Dependabot creating any more for the specific dependency (unless you unignore this specific dependency or upgrade to it yourself)
- `@dependabot unignore <dependency name>` will remove all of the ignore conditions of the specified dependency
- `@dependabot unignore <dependency name> <ignore condition>` will remove the ignore condition of the specified dependency and ignore conditions

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `45a5607d424b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.