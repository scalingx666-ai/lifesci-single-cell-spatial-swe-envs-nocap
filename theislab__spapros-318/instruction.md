# Issue

**Title:** [DEPENDABOT]: Bump pypa/gh-action-pypi-publish from 1.5.1 to 1.8.14

## Description

Bumps [pypa/gh-action-pypi-publish](https://github.com/pypa/gh-action-pypi-publish) from 1.5.1 to 1.8.14.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pypa/gh-action-pypi-publish/releases">pypa/gh-action-pypi-publish's releases</a>.</em></p>
<blockquote>
<h2>v1.8.14</h2>
<h2>🛠️ Internal Dependencies</h2>
<p>Nothing changed feature-wise. The only notable update is that the underlying container runtime now uses Python 3.12 and pip has been updated to v24.0 there.
This is should go unnoticed in terms of behavior. It's just a bit of maintenance burden to be done occasionally by <a href="https://github.com/webknjaz"><code>@​webknjaz</code></a><a href="https://github.com/sponsors/webknjaz">💰</a>.
<em>Enjoy!</em></p>
<p><strong>🪞 Full Diff</strong>: <a href="https://github.com/pypa/gh-action-pypi-publish/compare/v1.8.13...v1.8.14">https://github.com/pypa/gh-action-pypi-publish/compare/v1.8.13...v1.8.14</a></p>
<p><strong>🧔‍♂️ Release Manager:</strong> <a href="https://github.com/sponsors/webknjaz"><code>@​webknjaz 🇺🇦</code></a></p>
<h2>v1.8.13</h2>
<h2>🐛 What's Fixed</h2>
<p>This action is now able to consume and publish distribution packages with <code>Metadata-Version: 2.3</code> embedded.</p>
<h2>🛠️ Internal Dependencies</h2>
<p><a href="https://github.com/SigureMo"><code>@​SigureMo</code></a><a href="https://github.com/sponsors/SigureMo">💰</a> sent us a bump of <code>pkginfo</code> version to version 1.10.0 in <a href="">#219</a>. It's a transitive dependency for us and is not an API-level change but upgrading it has a side effect of letting Twine recognize distribution packages <a href="https://packaging.python.org/en/latest/specifications/core-metadata/">declaring <code>Metadata-Version: 2.3</code></a>. In particular, it is known to affect distributions built with <code>Maturin &gt;= 1.5.0</code>.</p>
<p>Following that, <a href="https://github.com/webknjaz"><code>@​webknjaz</code></a><a href="https://github.com/sponsors/webknjaz">💰</a> upgraded other transitive and direct dependency pins, including, among others, the following notable bumps:</p>
<ul>
<li><code>cryptography == 42.0.5</code></li>
<li><code>id == 1.3.0</code></li>
<li><code>readme-renderer == 43.0</code></li>
<li><code>Twine == 5.0.0</code></li>
</ul>
<h2>💪 New Contributors</h2>
<p><a href="https://github.com/SigureMo"><code>@​SigureMo</code></a> made their first contribution in <a href="">pypa/gh-action-pypi-publish#219</a></p>
<p><strong>🪞 Full Diff</strong>: <a href="https://github.com/pypa/gh-action-pypi-publish/compare/v1.8.12...v1.8.13">https://github.com/pypa/gh-action-pypi-publish/compare/v1.8.12...v1.8.13</a></p>
<p><strong>🧔‍♂️ Release Manager:</strong> <a href="https://github.com/sponsors/webknjaz"><code>@​webknjaz 🇺🇦</code></a></p>
<h2>v1.8.12</h2>
<h2>💅 Cosmetic Output Improvements</h2>
<p><a href="https://github.com/woodruffw"><code>@​woodruffw</code></a><a href="https://github.com/sponsors/woodruffw">💰</a> replaced the notice annotations with simplified debug messages related to authentication methanism selection via <a href="">#196</a>. The also improved the error clarity during OIDC exchange on PRs from forks via  <a href="">#203</a>.</p>
<h2>📝 What's Documented</h2>
<p><a href="https://github.com/virtuald"><code>@​virtuald</code></a><a href="https://github.com/sponsors/virtuald">💰</a> updated the docs and pointer messages were updated to mention that reusable workflows aren't supported right now in <a href="">#186</a> and <a href="https://github.com/xuanzhi33"><code>@​xuanzhi33</code></a><a href="https://github.com/sponsors/xuanzhi33">💰</a> later corrected the markdown syntax there via <a href="">#216</a>.</p>
<h2>🛠️ Internal Dependencies</h2>
<ul>
<li>pre-commit linters got autoupdated @ <a href="">#204</a></li>
<li>Cryptography was bumped from 41.0.6 to 42.0.4 @ <a href="">#210</a>, <a href="">#213</a> and <a href="">#214</a></li>
</ul>
<h2>⚙️  Secret Stuff</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>81e9d93</code></a> Bump <code>pip</code> to v24.0 in runtime prerequisites lock</li>
<li><a href=""><code>91527c4</code></a> Regenerate lockfiles with pip-tools v7.4.1</li>
<li><a href=""><code>3a817c6</code></a> Bump action runtime to CPython 3.12</li>
<li><a href=""><code>741947b</code></a> Add a config file for <code>pip-tools</code></li>
<li><a href=""><code>d7af439</code></a> Mass-bump transitive dependencies of runtime</li>
<li><a href=""><code>e90ddca</code></a> Bump <code>readme-renderer</code> to v43.0</li>
<li><a href=""><code>dae7fa3</code></a> Bump Twine to v5.0.0</li>
<li><a href=""><code>0fe04ae</code></a> Bump <code>id</code> to v1.3.0</li>
<li><a href=""><code>444e179</code></a> Bump cryptography to v42.0.5</li>
<li><a href=""><code>820be4e</code></a> Normalize pip-tools' header comment @ <code>runtime.txt</code></li>
<li>Additional commits viewable in <a href="https://github.com/pypa/gh-action-pypi-publish/compare/v1.5.1...v1.8.14">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=pypa/gh-action-pypi-publish&package-manager=github_actions&previous-version=1.5.1&new-version=1.8.14)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dbf4b7cec1ca`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.