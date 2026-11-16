# Issue

**Title:** chore(deps): bump smol-toml from 1.7.0 to 1.8.0 in /website

## Description

Bumps [smol-toml](https://github.com/squirrelchat/smol-toml) from 1.7.0 to 1.8.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/squirrelchat/smol-toml/releases">smol-toml's releases</a>.</em></p>
<blockquote>
<h2>v1.8.0</h2>
<h2>What's Changed</h2>
<ul>
<li>feat: stringify temporal objects by <a href="https://github.com/Gouvernathor"><code>@​Gouvernathor</code></a> and <a href="https://github.com/cyyynthia"><code>@​cyyynthia</code></a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/squirrelchat/smol-toml/compare/v1.7.2...v1.8.0">https://github.com/squirrelchat/smol-toml/compare/v1.7.2...v1.8.0</a></p>
<h2>v1.7.2</h2>
<h2>What's Changed</h2>
<ul>
<li>refactor: improve performance of the parser by <a href="https://github.com/cyyynthia"><code>@​cyyynthia</code></a></li>
<li>chore: revert sourcemap publishing by <a href="https://github.com/cyyynthia"><code>@​cyyynthia</code></a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/squirrelchat/smol-toml/compare/v1.7.1...v1.7.2">https://github.com/squirrelchat/smol-toml/compare/v1.7.1...v1.7.2</a></p>
<h2>v1.7.1</h2>
<p>This release includes flagging internal functions as <code>@internal</code> to strip them from the emitted type declarations.</p>
<p>⚠️ <strong>Includes a fix for GHSA-7w5x-hrqm-74c2</strong></p>
<p><strong>Full Changelog</strong>: <a href="https://github.com/squirrelchat/smol-toml/compare/v1.7.0...v1.7.1">https://github.com/squirrelchat/smol-toml/compare/v1.7.0...v1.7.1</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>6d0f477</code></a> chore: bump version</li>
<li><a href=""><code>97e9713</code></a> docs: mention temporal api</li>
<li><a href=""><code>7a3068d</code></a> perf: ubench opt for <code>instanceof Date</code></li>
<li><a href=""><code>7e8c09a</code></a> feat: stringify temporal</li>
<li><a href=""><code>19239d0</code></a> chore: bump version</li>
<li><a href=""><code>5f55c3a</code></a> chore: revert sourcemap publishing</li>
<li><a href=""><code>5c26f1b</code></a> chore: update benchmarks</li>
<li><a href=""><code>92832d2</code></a> refactor: better logic orchestration in structs</li>
<li><a href=""><code>2fb9ab8</code></a> refactor: ctx object instead of pointer arg + tuple returns</li>
<li><a href=""><code>e6017c4</code></a> ci: use staged publish</li>
<li>Additional commits viewable in <a href="https://github.com/squirrelchat/smol-toml/compare/v1.7.0...v1.8.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=smol-toml&package-manager=npm_and_yarn&previous-version=1.7.0&new-version=1.8.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/COMBINE-lab/salmon/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3be8b31d312`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.