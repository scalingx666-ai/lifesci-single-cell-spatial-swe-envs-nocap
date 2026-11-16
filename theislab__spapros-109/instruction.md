# Issue

**Title:** [DEPENDABOT]: Bump rich from 10.2.2 to 10.3.0

## Description

Bumps [rich](https://github.com/willmcgugan/rich) from 10.2.2 to 10.3.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/willmcgugan/rich/releases">rich's releases</a>.</em></p>
<blockquote>
<h2>Rich Repr updates</h2>
<p>This release fleshes out the new <a href="https://rich.readthedocs.io/en/latest/pretty.html">Rich Repr</a> protocol</p>
<h2>[10.3.0] - 2021-06-09</h2>
<h3>Added</h3>
<ul>
<li>Added Console.size setter</li>
<li>Added Console.width setter</li>
<li>Added Console.height setter</li>
<li>Added angular style Rich reprs</li>
<li>Added an IPython extension. Load via <code>%load_ext rich</code></li>
</ul>
<h3>Changed</h3>
<ul>
<li>Changed the logic for retrieving the calling frame in console logs to a faster one for the Python implementations that support it.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/willmcgugan/rich/blob/master/CHANGELOG.md">rich's changelog</a>.</em></p>
<blockquote>
<h2>[10.3.0] - 2021-06-09</h2>
<h3>Added</h3>
<ul>
<li>Added Console.size setter</li>
<li>Added Console.width setter</li>
<li>Added Console.height setter</li>
<li>Added angular style Rich reprs</li>
<li>Added an IPython extension. Load via <code>%load_ext rich</code></li>
</ul>
<h3>Changed</h3>
<ul>
<li>Changed the logic for retrieving the calling frame in console logs to a faster one for the Python implementations that support it.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2002463</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1274">#1274</a> from nathanrpage97/feat/add-ipython-extension</li>
<li><a href=""><code>9a65f49</code></a> Merge branch 'master' into feat/add-ipython-extension</li>
<li><a href=""><code>7592f09</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1275">#1275</a> from willmcgugan/tui</li>
<li><a href=""><code>d5d08a2</code></a> lock update</li>
<li><a href=""><code>30efe8d</code></a> Merge branch 'master' into tui</li>
<li><a href=""><code>ed2e4cc</code></a> mypy upgrade</li>
<li><a href=""><code>cc286e9</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1276">#1276</a> from willmcgugan/dependabot/pip/mypy-0.901</li>
<li><a href=""><code>932c451</code></a> repr example</li>
<li><a href=""><code>74ba2e1</code></a> Merge branch 'tui' of github.com:willmcgugan/rich into tui</li>
<li><a href=""><code>74efdcd</code></a> Version bump</li>
<li>Additional commits viewable in <a href="https://github.com/willmcgugan/rich/compare/v10.2.2...v10.3.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=rich&package-manager=pip&previous-version=10.2.2&new-version=10.3.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fbf354463721`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.