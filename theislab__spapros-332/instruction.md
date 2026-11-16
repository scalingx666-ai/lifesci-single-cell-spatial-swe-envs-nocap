# Issue

**Title:** [DEPENDABOT]: Bump actions/checkout from 4.1.2 to 4.1.3

## Description

Bumps [actions/checkout](https://github.com/actions/checkout) from 4.1.2 to 4.1.3.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/releases">actions/checkout's releases</a>.</em></p>
<blockquote>
<h2>v4.1.3</h2>
<h2>What's Changed</h2>
<ul>
<li>Update <code>actions/checkout</code> version in <code>update-main-version.yml</code> by <a href="https://github.com/jww3"><code>@​jww3</code></a> in <a href="">actions/checkout#1650</a></li>
<li>Check git version before attempting to disable <code>sparse-checkout</code> by <a href="https://github.com/jww3"><code>@​jww3</code></a> in <a href="">actions/checkout#1656</a></li>
<li>Add SSH user parameter by <a href="https://github.com/cory-miller"><code>@​cory-miller</code></a> in <a href="">actions/checkout#1685</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v4.1.2...v4.1.3">https://github.com/actions/checkout/compare/v4.1.2...v4.1.3</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/blob/main/CHANGELOG.md">actions/checkout's changelog</a>.</em></p>
<blockquote>
<h1>Changelog</h1>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>1d96c77</code></a> Add SSH user parameter (<a href="">#1685</a>)</li>
<li><a href=""><code>cd7d8d6</code></a> Check git version before attempting to disable <code>sparse-checkout</code> (<a href="">#1656</a>)</li>
<li><a href=""><code>8410ad0</code></a> Update <code>actions/checkout</code> version in <code>update-main-version.yml</code> (<a href="">#1650</a>)</li>
<li>See full diff in <a href="https://github.com/actions/checkout/compare/v4.1.2...v4.1.3">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/checkout&package-manager=github_actions&previous-version=4.1.2&new-version=4.1.3)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ecb19f0544f9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.