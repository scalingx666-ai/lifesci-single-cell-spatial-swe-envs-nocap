# Issue

**Title:** test: bump the pre-commit group with 4 updates

## Description

Bumps the pre-commit group with 4 updates: [https://github.com/biomejs/pre-commit](https://github.com/biomejs/pre-commit), [https://github.com/tox-dev/pyproject-fmt](https://github.com/tox-dev/pyproject-fmt), [https://github.com/astral-sh/ruff-pre-commit](https://github.com/astral-sh/ruff-pre-commit) and [https://github.com/zizmorcore/zizmor-pre-commit](https://github.com/zizmorcore/zizmor-pre-commit).

Updates `https://github.com/biomejs/pre-commit` from v2.5.11 to 2.5.12
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>922fba1</code></a> build(deps): bump <code>@​biomejs/biome</code> to 2.5.12</li>
<li><a href=""><code>f559a3c</code></a> Fix typo (<a href="">#127</a>)</li>
<li><a href=""><code>fae863d</code></a> Fix typo</li>
<li><a href=""><code>cb10d5a</code></a> build(deps): bump <code>@​biomejs/biome</code> to 2.5.11 (<a href="">#126</a>)</li>
<li>See full diff in <a href="https://github.com/biomejs/pre-commit/compare/v2.5.11...v2.5.12">compare view</a></li>
</ul>
</details>
<br />

Updates `https://github.com/tox-dev/pyproject-fmt` from v2.29.3 to 2.29.4
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/tox-dev/pyproject-fmt/releases">https://github.com/tox-dev/pyproject-fmt's releases</a>.</em></p>
<blockquote>
<h2>v2.29.4</h2>
<!-- raw HTML omitted -->
<p><strong>Full Changelog</strong>: <a href="https://github.com/tox-dev/pyproject-fmt/compare/v2.29.3...v2.29.4">https://github.com/tox-dev/pyproject-fmt/compare/v2.29.3...v2.29.4</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>59e7b26</code></a> Mirror: 2.29.4</li>
<li><a href=""><code>fe1222b</code></a> Mirror: 2.29.4</li>
<li>See full diff in <a href="https://github.com/tox-dev/pyproject-fmt/compare/v2.29.3...v2.29.4">compare view</a></li>
</ul>
</details>
<br />

Updates `https://github.com/astral-sh/ruff-pre-commit` from v0.16.5 to 0.16.6
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ruff-pre-commit/releases">https://github.com/astral-sh/ruff-pre-commit's releases</a>.</em></p>
<blockquote>
<h2>v0.16.6</h2>
<p>See: <a href="https://github.com/astral-sh/ruff/releases/tag/0.16.6">https://github.com/astral-sh/ruff/releases/tag/0.16.6</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>321478e</code></a> Mirror: 0.16.6</li>
<li>See full diff in <a href="https://github.com/astral-sh/ruff-pre-commit/compare/v0.16.5...v0.16.6">compare view</a></li>
</ul>
</details>
<br />

Updates `https://github.com/zizmorcore/zizmor-pre-commit` from v1.30.0 to 1.30.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/zizmorcore/zizmor-pre-commit/releases">https://github.com/zizmorcore/zizmor-pre-commit's releases</a>.</em></p>
<blockquote>
<h2>v1.30.1</h2>
<p><a href="https://github.com/sponsors/woodruffw/">Sponsorship is appreciated!</a></p>
<h2>Bug Fixes 🐛<a href="https://docs.zizmor.sh/release-notes/#bug-fixes">🔗</a></h2>
<ul>
<li>
<p>Fixed a bug where zizmor would crash on pre-commit inputs that reference a GitHub URL with an explicit .git suffix (<a href="">#2363</a>)</p>
</li>
<li>
<p>Fixed a bug where <a href="https://docs.zizmor.sh/audits/#self-repository">self-repository</a> auto-fixes were incorrectly marked as &quot;safe&quot; instead of &quot;unsafe&quot; (<a href="">#2373</a>)</p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>fa41207</code></a> Mirror: 1.30.1</li>
<li><a href=""><code>7361a0b</code></a> fix: include pre-commit files in hook (<a href="">#59</a>)</li>
<li><a href=""><code>34c5ce3</code></a> Bump zizmorcore/zizmor-action from 0.6.2 to 0.6.3 in the github-actions group...</li>
<li>See full diff in <a href="https://github.com/zizmorcore/zizmor-pre-commit/compare/v1.30.0...v1.30.1">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5f2accbe77cb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.