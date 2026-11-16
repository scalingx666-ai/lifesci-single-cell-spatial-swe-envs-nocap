# Issue

**Title:** [DEPENDABOT]: Bump flake8-bugbear from 21.9.2 to 21.11.29

## Description

Bumps [flake8-bugbear](https://github.com/PyCQA/flake8-bugbear) from 21.9.2 to 21.11.29.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/PyCQA/flake8-bugbear/releases">flake8-bugbear's releases</a>.</em></p>
<blockquote>
<h2>21.11.29</h2>
<ul>
<li>B018: Disable strings from check for now (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/209">#209</a>)</li>
</ul>
<h2>21.11.28</h2>
<ul>
<li>B904: ensure the raise is in the same context with the except (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/191">#191</a>)</li>
<li>Add Option to extend the list of immutable calls (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/204">#204</a>)</li>
<li>Update B014: <code>binascii.Error</code> is now treated as a subclass of <code>ValueError</code> (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/206">#206</a>)</li>
<li>add simple pre-commit config (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/205">#205</a>)</li>
<li>Test with 3.10 official</li>
<li>Add B018 check to find useless declarations (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/196">#196</a>, <a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/202">#202</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>49aec18</code></a> Update version + Change Log for 21.11.29 release (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/210">#210</a>)</li>
<li><a href=""><code>225f4e6</code></a> Remove detection of strings in B018 (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/209">#209</a>)</li>
<li><a href=""><code>9e311d5</code></a> Fix 904 tests to expect on correct raise line</li>
<li><a href=""><code>987e539</code></a> Update CHANGES.md, black format, update to version 21.11.28 for release</li>
<li><a href=""><code>9e14a8c</code></a> B904: ensure the raise is in the same context with the except (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/191">#191</a>)</li>
<li><a href=""><code>c452048</code></a> Add Option to extend the list of immutable calls (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/204">#204</a>)</li>
<li><a href=""><code>c90fa65</code></a> B014: catch binascii.Error and ValueError redundancy + cleanup (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/206">#206</a>)</li>
<li><a href=""><code>71091f9</code></a> add simple pre-commit config (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/205">#205</a>)</li>
<li><a href=""><code>98829c3</code></a> Improve B018 further (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/202">#202</a>)</li>
<li><a href=""><code>2ca8d79</code></a> B018: Find more constants w/o assign (<a href="https://github-redirect.dependabot.com/PyCQA/flake8-bugbear/issues/201">#201</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/PyCQA/flake8-bugbear/compare/21.9.2...21.11.29">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=flake8-bugbear&package-manager=pip&previous-version=21.9.2&new-version=21.11.29)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `69c70b1410ab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.