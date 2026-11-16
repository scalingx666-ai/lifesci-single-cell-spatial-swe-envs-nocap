# Issue

**Title:** [DEPENDABOT]: Bump rich from 10.3.0 to 10.4.0

## Description

Bumps [rich](https://github.com/willmcgugan/rich) from 10.3.0 to 10.4.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/willmcgugan/rich/releases">rich's releases</a>.</em></p>
<blockquote>
<h2>Auto Rich Repr</h2>
<p>The highlight of this release is a decorator to automatically create a Rich repr for any class.</p>
<!-- raw HTML omitted -->
<!-- raw HTML omitted -->
<h2>[10.4.0] - 2021-06-18</h2>
<h3>Added</h3>
<ul>
<li>Added Style.meta</li>
<li>Added rich.repr.auto decorator</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Fixed error pretty printing classes with special <strong>rich_repr</strong> method</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/willmcgugan/rich/blob/master/CHANGELOG.md">rich's changelog</a>.</em></p>
<blockquote>
<h2>[10.4.0] - 2021-06-18</h2>
<h3>Added</h3>
<ul>
<li>Added Style.meta</li>
<li>Added rich.repr.auto decorator</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Fixed error pretty printing classes with special <strong>rich_repr</strong> method</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>e524643</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1300">#1300</a> from willmcgugan/pretty-classes</li>
<li><a href=""><code>6e97016</code></a> test fix</li>
<li><a href=""><code>56b4c53</code></a> auto import</li>
<li><a href=""><code>3281af6</code></a> auto repr</li>
<li><a href=""><code>41cc6a6</code></a> added meta to Style</li>
<li><a href=""><code>6ac54d0</code></a> fix for pretty printing classes</li>
<li><a href=""><code>56e7158</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1291">#1291</a> from cclauss/codepsell</li>
<li><a href=""><code>194e638</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1293">#1293</a> from willmcgugan/dependabot/pip/sphinx-copybutton-0.3.3</li>
<li><a href=""><code>52af9f1</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1292">#1292</a> from willmcgugan/dependabot/pip/types-dataclasses-0.1.4</li>
<li><a href=""><code>a3164a2</code></a> Bump sphinx-copybutton from 0.3.1 to 0.3.3</li>
<li>Additional commits viewable in <a href="https://github.com/willmcgugan/rich/compare/v10.3.0...v10.4.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=rich&package-manager=pip&previous-version=10.3.0&new-version=10.4.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot merge` will merge this PR after your CI passes on it
- `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
- `@dependabot cancel merge` will cancel a previously requested merge and block automerging
- `@dependabot reopen` will reopen this PR if it is closed
- `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7b8bb236a7b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.