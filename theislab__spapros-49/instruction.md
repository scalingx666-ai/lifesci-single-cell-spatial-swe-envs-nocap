# Issue

**Title:** [DEPENDABOT]: Bump flake8-bugbear from 21.3.2 to 21.4.3

## Description

Bumps [flake8-bugbear](https://github.com/PyCQA/flake8-bugbear) from 21.3.2 to 21.4.3.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/PyCQA/flake8-bugbear/releases">flake8-bugbear's releases</a>.</em></p>
<blockquote>
<h2>21.4.3</h2>
<p>Verify the element in item_context.args is of type ast.Name for b017</p>
<h2>21.4.2</h2>
<ul>
<li>Add another hasattr() check to b017 visit for .func</li>
</ul>
<h2>21.4.1</h2>
<p>Happy April Fools! This is no joke, it's a real release.</p>
<ul>
<li>Add B017: check for gotta-catch-em-all assertRaises(Exception)</li>
</ul>
<p>Catching them all is bad!</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>63239e0</code></a> Update Change Log for 21.4.3 release</li>
<li><a href=""><code>3cab68c</code></a> Bugfix: Verify the element in item_context.args is of type ast.Name (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/166">#166</a>)</li>
<li><a href=""><code>d3bf9ab</code></a> Increment version to 21.4.2 for release + Update Changelog</li>
<li><a href=""><code>a97d3db</code></a> Add another hasattr() check to b017 visit (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/165">#165</a>)</li>
<li><a href=""><code>bfd3b7e</code></a> Increment version to 21.4.1 for release</li>
<li><a href=""><code>9d18e5f</code></a> Add B017 - detection for an evil form of assertRaises (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/163">#163</a>)</li>
<li>See full diff in <a href="https://github.com/PyCQA/flake8-bugbear/compare/21.3.2...21.4.3">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=flake8-bugbear&package-manager=pip&previous-version=21.3.2&new-version=21.4.3)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1cbb25e0d4cb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.