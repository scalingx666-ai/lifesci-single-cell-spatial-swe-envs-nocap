# Issue

**Title:** [DEPENDABOT]: Bump rich from 9.12.4 to 9.13.0

## Description

Bumps [rich](https://github.com/willmcgugan/rich) from 9.12.4 to 9.13.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/willmcgugan/rich/releases">rich's releases</a>.</em></p>
<blockquote>
<h2>Pretty dataclass support</h2>
<p>The highlight of this release is that pretty printing now supports dataclasses, which can now collapse just like other data structures. Here's an example:</p>
<!-- raw HTML omitted -->
<h2>[9.13.0] - 2021-03-06</h2>
<h3>Added</h3>
<ul>
<li>Pretty printer now supports dataclasses</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Fixed Syntax background <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1088">willmcgugan/rich#1088</a></li>
<li>Fix for double tracebacks when no formatter <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1079">willmcgugan/rich#1079</a></li>
</ul>
<h3>Changed</h3>
<ul>
<li>Added ws and wss to url highlighter</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/willmcgugan/rich/blob/master/CHANGELOG.md">rich's changelog</a>.</em></p>
<blockquote>
<h2>[9.13.0] - 2021-03-06</h2>
<h3>Added</h3>
<ul>
<li>Pretty printer now supports dataclasses</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Fixed Syntax background <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1088">willmcgugan/rich#1088</a></li>
<li>Fix for double tracebacks when no formatter <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1079">willmcgugan/rich#1079</a></li>
</ul>
<h3>Changed</h3>
<ul>
<li>Added ws and wss to url highlighter</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>c3d0e35</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1095">#1095</a> from willmcgugan/formatter-fix</li>
<li><a href=""><code>8b4e474</code></a> no double tracebacks</li>
<li><a href=""><code>6978f29</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1094">#1094</a> from willmcgugan/pretty-dataclass</li>
<li><a href=""><code>bcd61cc</code></a> type fix</li>
<li><a href=""><code>01d1563</code></a> add test for google colab</li>
<li><a href=""><code>7536d54</code></a> py36 exception</li>
<li><a href=""><code>cbbc490</code></a> rename dataclass in test</li>
<li><a href=""><code>681c14a</code></a> type fixes</li>
<li><a href=""><code>a05ff5f</code></a> pretty printable dataclasses</li>
<li><a href=""><code>7dd6eb1</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1091">#1091</a> from Adilius/master</li>
<li>Additional commits viewable in <a href="https://github.com/willmcgugan/rich/compare/v9.12.4...v9.13.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=rich&package-manager=pip&previous-version=9.12.4&new-version=9.13.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b6c9703f95d5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.