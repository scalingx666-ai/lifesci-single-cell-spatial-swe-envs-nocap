# Issue

**Title:** [DEPENDABOT]: Bump actions/cache from 2.1.7 to 3.0.7

## Description

Bumps [actions/cache](https://github.com/actions/cache) from 2.1.7 to 3.0.7.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/cache/releases">actions/cache's releases</a>.</em></p>
<blockquote>
<h2>v3.0.7</h2>
<h2>What's Changed</h2>
<ul>
<li>Fix for the download stuck problem has been added in actions/cache for users who were intermittently facing the issue. As part of this fix, new timeout has been introduced in the download step to stop the download if it doesn't complete within an hour and run the rest of the workflow without erroring out.</li>
</ul>
<h2>v3.0.6</h2>
<h3>What's Changed</h3>
<ul>
<li>Add example for clojure lein project dependencies by <a href="https://github.com/shivamarora1"><code>@​shivamarora1</code></a> in PR <a href="https://github-redirect.dependabot.com/actions/cache/pull/835">actions/cache#835</a></li>
<li>Update toolkit's cache npm module to latest. Bump cache version to v3.0.6 by <a href="https://github.com/pdotl"><code>@​pdotl</code></a> in PR <a href="https://github-redirect.dependabot.com/actions/cache/pull/887">actions/cache#887</a></li>
<li>Fix issue <a href="https://github-redirect.dependabot.com/actions/cache/issues/809">#809</a> where cache save/restore was failing for Amazon Linux 2 runners due to older tar version</li>
<li>Fix issue <a href="https://github-redirect.dependabot.com/actions/cache/issues/833">#833</a> where cache save was not working for caching github workspace directory</li>
</ul>
<h3>New Contributors</h3>
<ul>
<li><a href="https://github.com/shivamarora1"><code>@​shivamarora1</code></a> made their first contribution in <a href="https://github-redirect.dependabot.com/actions/cache/pull/835">actions/cache#835</a></li>
<li><a href="https://github.com/pdotl"><code>@​pdotl</code></a> made their first contribution in <a href="https://github-redirect.dependabot.com/actions/cache/pull/887">actions/cache#887</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/cache/compare/v3...v3.0.6">https://github.com/actions/cache/compare/v3...v3.0.6</a></p>
<h2>v3.0.5</h2>
<p>Removed error handling by consuming actions/cache 3.0 toolkit, Now cache server error handling will be done by toolkit.</p>
<h2>v3.0.4</h2>
<p>In this release, we have fixed the tar creation error while trying to create it with path as <code>~/</code> home folder on <code>ubuntu-latest</code>.</p>
<h2>v3.0.3</h2>
<p>Fixed avoiding empty cache save when no files are available for caching. (<a href="https://github-redirect.dependabot.com/actions/cache/issues/624">actions/cache#624</a>)</p>
<h2>v3.0.2</h2>
<p>This release adds the support for dynamic cache size cap on GHES.</p>
<h2>v3.0.1</h2>
<ul>
<li>Added support for caching from GHES 3.5.</li>
<li>Fixed download issue for files &gt; 2GB during restore.</li>
</ul>
<h2>v3.0.0</h2>
<ul>
<li>
<p>This change adds a minimum runner version(node12 -&gt; node16), which can break users using an out-of-date/fork of the runner. This would be most commonly affecting users on GHES 3.3 or before, as those runners do not support node16 actions and they can use actions from github.com via <a href="https://docs.github.com/en/enterprise-server@3.0/admin/github-actions/managing-access-to-actions-from-githubcom/enabling-automatic-access-to-githubcom-actions-using-github-connect">github connect</a> or manually copying the repo to their GHES instance.</p>
</li>
<li>
<p>Few dependencies and cache action usage examples have also been updated.</p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/actions/cache/blob/main/RELEASES.md">actions/cache's changelog</a>.</em></p>
<blockquote>
<h3>3.0.7</h3>
<ul>
<li>Fixed <a href="https://github-redirect.dependabot.com/actions/cache/issues/810">#810</a> - download stuck issue. A new timeout is introduced in the download process to abort the download if it gets stuck and doesn't finish within an hour.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a7c34ad</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/cache/issues/894">#894</a> from actions/kotewar/update-toolkit-version</li>
<li><a href=""><code>83394c9</code></a> Updated cache version in license file</li>
<li><a href=""><code>e839c25</code></a> Updated actions/cache version to 3.0.3</li>
<li><a href=""><code>33a923d</code></a> Added release information</li>
<li><a href=""><code>a404368</code></a> Updated actions/cache version to 3.0.2</li>
<li><a href=""><code>f427802</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/cache/issues/887">#887</a> from actions/pdotl-version-patch</li>
<li><a href=""><code>9916fe1</code></a> Update cache version in licences</li>
<li><a href=""><code>318935e</code></a> Update README and RELEASES</li>
<li><a href=""><code>85efbb5</code></a> Update cache npm module to latest</li>
<li><a href=""><code>4387dbc</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/cache/issues/835">#835</a> from shivamarora1/clojure-lein-example</li>
<li>Additional commits viewable in <a href="https://github.com/actions/cache/compare/v2.1.7...v3.0.7">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/cache&package-manager=github_actions&previous-version=2.1.7&new-version=3.0.7)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `abf158e195b0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.