# Issue

**Title:** [DEPENDABOT]: Bump rich from 10.14.0 to 10.16.2

## Description

Bumps [rich](https://github.com/willmcgugan/rich) from 10.14.0 to 10.16.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/willmcgugan/rich/releases">rich's releases</a>.</em></p>
<blockquote>
<h2>v10.16.2</h2>
<h2>[10.16.2] - 2021-01-02</h2>
<h3>Fixed</h3>
<ul>
<li>Fixed @ not being escaped in markup</li>
</ul>
<h2>v10.16.1</h2>
<h2>[10.16.1] - 2021-12-15</h2>
<h3>Fixed</h3>
<ul>
<li>Fixed issues with overlapping tags <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1755">willmcgugan/rich#1755</a></li>
</ul>
<h2>v10.16.0</h2>
<p>A bugfix for progress bars in Jupyter in this release. And a new property on Text class which exports the equivalent console markup.</p>
<h2>[10.16.0] - 2021-12-12</h2>
<h3>Fixed</h3>
<ul>
<li>Double print of progress bar in Jupyter <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1737">willmcgugan/rich#1737</a></li>
</ul>
<h3>Added</h3>
<ul>
<li>Added Text.markup property <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1751">willmcgugan/rich#1751</a></li>
</ul>
<h2>Hotfix to fix deadlock issue with Live (including status and progress)</h2>
<p>AFAIK this issue only occurred in test suites, but it is a recommended that if you have 10.15.X installed you should upgrade.</p>
<h2>[10.15.2] - 2021-12-02</h2>
<h3>Fixed</h3>
<ul>
<li>Deadlock issue <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1734">willmcgugan/rich#1734</a></li>
</ul>
<h2>v10.15.1</h2>
<p>Reverted a fix for <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1530">willmcgugan/rich#1530</a></p>
<p>On reflection, I think the fix might introduce the possibility for a deadlock -- although none was reported.</p>
<h2>[10.15.1] - 2021-11-29</h2>
<h3>Changed</h3>
<ul>
<li>Reverted thread-safety fix for Live that introduced deadlock potential</li>
</ul>
<h2>v10.15.0</h2>
<h2>[10.15.0] - 2021-11-28</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/Textualize/rich/blob/master/CHANGELOG.md">rich's changelog</a>.</em></p>
<blockquote>
<h2>[10.16.2] - 2021-01-02</h2>
<h3>Fixed</h3>
<ul>
<li>Fixed @ not being escaped in markup</li>
</ul>
<h2>[10.16.1] - 2021-12-15</h2>
<h3>Fixed</h3>
<ul>
<li>Fixed issues with overlapping tags <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1755">willmcgugan/rich#1755</a></li>
</ul>
<h2>[10.16.0] - 2021-12-12</h2>
<h3>Fixed</h3>
<ul>
<li>Double print of progress bar in Jupyter <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1737">willmcgugan/rich#1737</a></li>
</ul>
<h3>Added</h3>
<ul>
<li>Added Text.markup property <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1751">willmcgugan/rich#1751</a></li>
</ul>
<h2>[10.15.2] - 2021-12-02</h2>
<h3>Fixed</h3>
<ul>
<li>Deadlock issue <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1734">willmcgugan/rich#1734</a></li>
</ul>
<h2>[10.15.1] - 2021-11-29</h2>
<h3>Fixed</h3>
<ul>
<li>Reverted thread-safety fix for Live that introduced deadlock potential</li>
</ul>
<h2>[10.15.0] - 2021-11-28</h2>
<h3>Added</h3>
<ul>
<li>Added dynamic_progress.py to examples</li>
<li>Added ConsoleOptions.update_height</li>
<li>Fixed Padding not respecting height</li>
</ul>
<h3>Changed</h3>
<ul>
<li>Some optimizations for simple strings (with only single cell widths)</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Fixed issue with progress bar not rendering markup <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1721">willmcgugan/rich#1721</a></li>
<li>Fixed race condition when exiting Live <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1530">willmcgugan/rich#1530</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2ba277a</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1793">#1793</a> from willmcgugan/escape_at</li>
<li><a href=""><code>e839bfb</code></a> additional test</li>
<li><a href=""><code>4b1293e</code></a> fix at escape</li>
<li><a href=""><code>1d5152e</code></a> fix code block</li>
<li><a href=""><code>7331ca6</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1789">#1789</a> from willmcgugan/dependabot/pip/attrs-21.4.0</li>
<li><a href=""><code>a1c76b2</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1781">#1781</a> from MaxG87/master</li>
<li><a href=""><code>c00a665</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1753">#1753</a> from joehalliwell/per_message_log_highlighting</li>
<li><a href=""><code>8a3dc75</code></a> Remove unused import</li>
<li><a href=""><code>300cff6</code></a> Use getattr's built-in default</li>
<li><a href=""><code>23daac5</code></a> Add documentation</li>
<li>Additional commits viewable in <a href="https://github.com/willmcgugan/rich/compare/v10.14.0...v10.16.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=rich&package-manager=pip&previous-version=10.14.0&new-version=10.16.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b9c46f0a14ef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.