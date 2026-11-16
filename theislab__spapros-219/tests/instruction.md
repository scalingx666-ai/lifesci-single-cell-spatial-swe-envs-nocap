# Issue

**Title:** [DEPENDABOT]: Bump pypa/gh-action-pypi-publish from 1.4.2 to 1.5.1

## Description

Bumps [pypa/gh-action-pypi-publish](https://github.com/pypa/gh-action-pypi-publish) from 1.4.2 to 1.5.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pypa/gh-action-pypi-publish/releases">pypa/gh-action-pypi-publish's releases</a>.</em></p>
<blockquote>
<h2>v1.5.1</h2>
<h2>What's Changed</h2>
<ul>
<li>Fixed printing out the dist hashes when <code>packages_dir</code> is a wildcard value. — by <a href="https://github.com/meowmeowmeowcat"><code>@​meowmeowmeowcat</code></a> in <a href="https://github-redirect.dependabot.com/pypa/gh-action-pypi-publish/pull/91">pypa/gh-action-pypi-publish#91</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/pypa/gh-action-pypi-publish/compare/v1.5.0...v1.5.1">https://github.com/pypa/gh-action-pypi-publish/compare/v1.5.0...v1.5.1</a></p>
<h2>v1.5.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Added an action input <code>print_hash</code> for showing the hash values of files to be uploaded — by <a href="https://github.com/meowmeowmeowcat"><code>@​meowmeowmeowcat</code></a> in <a href="https://github-redirect.dependabot.com/pypa/gh-action-pypi-publish/pull/87">pypa/gh-action-pypi-publish#87</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/pllim"><code>@​pllim</code></a> made their first contribution in <a href="https://github-redirect.dependabot.com/pypa/gh-action-pypi-publish/pull/55">pypa/gh-action-pypi-publish#55</a></li>
<li><a href="https://github.com/meowmeowmeowcat"><code>@​meowmeowmeowcat</code></a> made their first contribution in <a href="https://github-redirect.dependabot.com/pypa/gh-action-pypi-publish/pull/87">pypa/gh-action-pypi-publish#87</a></li>
</ul>
<p><strong>Full Diff</strong>: <a href="https://github.com/pypa/gh-action-pypi-publish/compare/v1.4.2...v1.5.0">https://github.com/pypa/gh-action-pypi-publish/compare/v1.4.2...v1.5.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>37f50c2</code></a> Merge PR <a href="https://github-redirect.dependabot.com/pypa/gh-action-pypi-publish/issues/91">#91</a></li>
<li><a href=""><code>9f0421c</code></a> Add #StandWithUkraine banner to README</li>
<li><a href=""><code>c3fbd68</code></a> Remove quotes</li>
<li><a href=""><code>717ba43</code></a> Trim the trailing whitespaces in <code>print-hash.py</code></li>
<li><a href=""><code>4992a00</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/pypa/gh-action-pypi-publish/issues/87">#87</a> from meowmeowmeowcat/show-hash-values</li>
<li><a href=""><code>977d067</code></a> Fix a bug</li>
<li><a href=""><code>5d18baa</code></a> Drop unnecessary <code>file_iterable</code> var</li>
<li><a href=""><code>0575dc8</code></a> Refactor the hash helper script to use pathlib and CLI args</li>
<li><a href=""><code>8682135</code></a> Correct the if-clause for printing the hashes</li>
<li><a href=""><code>c83d37b</code></a> Introduce print_hash in README</li>
<li>Additional commits viewable in <a href="https://github.com/pypa/gh-action-pypi-publish/compare/v1.4.2...v1.5.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=pypa/gh-action-pypi-publish&package-manager=github_actions&previous-version=1.4.2&new-version=1.5.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ca36341addd4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.