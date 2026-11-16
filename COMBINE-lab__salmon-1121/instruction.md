# Issue

**Title:** chore(deps): bump js-yaml from 4.3.0 to 4.3.1 in /website

## Description

Bumps [js-yaml](https://github.com/nodeca/js-yaml) from 4.3.0 to 4.3.1.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/nodeca/js-yaml/blob/4.3.1/CHANGELOG.md">js-yaml's changelog</a>.</em></p>
<blockquote>
<h2>4.3.1 - 2026-07-31</h2>
<h3>Security</h3>
<ul>
<li>[backport] Remove quadratic complexity from <code>!!omap</code> duplicate key detection.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>86e91b8</code></a> 4.3.1 released</li>
<li><a href=""><code>c3cc4b0</code></a> Backport quadratic complexity fix for !!omap</li>
<li>See full diff in <a href="https://github.com/nodeca/js-yaml/compare/4.3.0...4.3.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=js-yaml&package-manager=npm_and_yarn&previous-version=4.3.0&new-version=4.3.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f772526b10c9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.