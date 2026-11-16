# Issue

**Title:** [DEPENDABOT]: Bump rich from 10.5.0 to 10.6.0

## Description

Bumps [rich](https://github.com/willmcgugan/rich) from 10.5.0 to 10.6.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/willmcgugan/rich/releases">rich's releases</a>.</em></p>
<blockquote>
<h2>Emoji variants</h2>
<h2>[10.6.0] - 2021-07-12</h2>
<h3>Deprecated</h3>
<ul>
<li>Added deprecation warning for tabulate_mapping which will be removed in v11.0.0</li>
</ul>
<h3>Added</h3>
<ul>
<li>Added precision argument to filesize.decimal</li>
<li>Added separator argument to filesize.decimal</li>
<li>Added _rich_traceback_guard to Traceback</li>
<li>Added emoji_variant to Console</li>
<li>Added -emoji and -text variant selectors to emoji code</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Fixed issue with adjoining color tags <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1334">willmcgugan/rich#1334</a></li>
</ul>
<h3>Changed</h3>
<ul>
<li>Changed Console.size to use unproxied stdin and stdout</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/willmcgugan/rich/blob/master/CHANGELOG.md">rich's changelog</a>.</em></p>
<blockquote>
<h2>[10.6.0] - 2021-07-12</h2>
<h3>Deprecated</h3>
<ul>
<li>Added deprecation warning for tabulate_mapping which will be removed in v11.0.0</li>
</ul>
<h3>Added</h3>
<ul>
<li>Added precision argument to filesize.decimal</li>
<li>Added separator argument to filesize.decimal</li>
<li>Added _rich_traceback_guard to Traceback</li>
<li>Added emoji_variant to Console</li>
<li>Added -emoji and -text variant selectors to emoji code</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Fixed issue with adjoining color tags <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1334">willmcgugan/rich#1334</a></li>
</ul>
<h3>Changed</h3>
<ul>
<li>Changed Console.size to use unproxied stdin and stdout</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2ea7e58</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1346">#1346</a> from willmcgugan/height-fixes</li>
<li><a href=""><code>836a474</code></a> update</li>
<li><a href=""><code>78b8c44</code></a> emoji variant</li>
<li><a href=""><code>62b00db</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1344">#1344</a> from lodagro/patch-1</li>
<li><a href=""><code>32deeba</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1345">#1345</a> from willmcgugan/dependabot/pip/sphinx-4.1.0</li>
<li><a href=""><code>e84aa0a</code></a> Bump sphinx from 4.0.3 to 4.1.0</li>
<li><a href=""><code>b5654c9</code></a> Fix docstring typo</li>
<li><a href=""><code>bf72103</code></a> Added _rich_traceback_guard</li>
<li><a href=""><code>aba4c7b</code></a> Added max height</li>
<li><a href=""><code>1e73828</code></a> options only</li>
<li>Additional commits viewable in <a href="https://github.com/willmcgugan/rich/compare/v10.5.0...v10.6.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=rich&package-manager=pip&previous-version=10.5.0&new-version=10.6.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0aabb85e016f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.