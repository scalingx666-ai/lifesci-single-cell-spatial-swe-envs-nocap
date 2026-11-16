# Issue

**Title:** [DEPENDABOT]: Bump actions/setup-python from 2 to 2.2.2

## Description

Bumps [actions/setup-python](https://github.com/actions/setup-python) from 2 to 2.2.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/setup-python/releases">actions/setup-python's releases</a>.</em></p>
<blockquote>
<h2>v2.2.2</h2>
<p>Address PyPy installation issues on Windows: <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/196">actions/setup-python#196</a></p>
<h2>v2.2.1</h2>
<ul>
<li>Fix PyPy3 issues with Windows</li>
</ul>
<h2>v2.2.0</h2>
<ul>
<li>Support for PyPy 3.7 in addition to the current 3.6 support</li>
<li>Support for Pre-Release distributions of PyPy</li>
<li>Support for PyPy Nighly</li>
</ul>
<h2>v2.1.4</h2>
<ul>
<li>Improvements for more reliable setup on self-hosted runners</li>
</ul>
<h2>v2.1.3</h2>
<ul>
<li>Updates to NPM dependencies</li>
<li>Updates to licenses</li>
</ul>
<h2>v2.1.2</h2>
<ul>
<li>Add Third Party License Information</li>
</ul>
<h2>v2.1.1</h2>
<p>Fix installation logic to prevent leaving files in GITHUB_WORKSPACE
Related issue: <a href="https://github-redirect.dependabot.com/actions/setup-python/issues/101">actions/setup-python#101</a></p>
<h2>v2.1.0</h2>
<ul>
<li>Support for pre-release Python distributions</li>
</ul>
<h2>v2.0.2</h2>
<ul>
<li>Improved logs &amp; output when downloading and setting up Python versions</li>
<li>Improvements and updates to downloading Python versions from actions/python-versions</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/actions/setup-python/compare/v2...v2.2.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/setup-python&package-manager=github_actions&previous-version=2&new-version=2.2.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `819c1bd59454`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.