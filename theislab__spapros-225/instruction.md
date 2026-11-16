# Issue

**Title:** [DEPENDABOT]: Bump actions/checkout from 2.4.0 to 3.0.2

## Description

Bumps [actions/checkout](https://github.com/actions/checkout) from 2.4.0 to 3.0.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/releases">actions/checkout's releases</a>.</em></p>
<blockquote>
<h2>v3.0.2</h2>
<h2>What's Changed</h2>
<ul>
<li>Add set-safe-directory input to allow customers to take control. by <a href="https://github.com/TingluoHuang"><code>@​TingluoHuang</code></a> in <a href="https://github-redirect.dependabot.com/actions/checkout/pull/770">actions/checkout#770</a></li>
<li>Prepare changelog for v3.0.2. by <a href="https://github.com/TingluoHuang"><code>@​TingluoHuang</code></a> in <a href="https://github-redirect.dependabot.com/actions/checkout/pull/777">actions/checkout#777</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v3...v3.0.2">https://github.com/actions/checkout/compare/v3...v3.0.2</a></p>
<h2>v3.0.1</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/762">Fixed an issue where checkout failed to run in container jobs due to the new git setting <code>safe.directory</code></a></li>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/744">Bumped various npm package versions</a></li>
</ul>
<h2>v3.0.0</h2>
<ul>
<li>Updated to the node16 runtime by default
<ul>
<li>This requires a minimum <a href="https://github.com/actions/runner/releases/tag/v2.285.0">Actions Runner</a> version of v2.285.0 to run, which is by default available in GHES 3.4 or later.</li>
</ul>
</li>
</ul>
<h2>v2.4.2</h2>
<h2>What's Changed</h2>
<ul>
<li>Add set-safe-directory input to allow customers to take control. (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/770">#770</a>) by <a href="https://github.com/TingluoHuang"><code>@​TingluoHuang</code></a> in <a href="https://github-redirect.dependabot.com/actions/checkout/pull/776">actions/checkout#776</a></li>
<li>Prepare changelog for v2.4.2. by <a href="https://github.com/TingluoHuang"><code>@​TingluoHuang</code></a> in <a href="https://github-redirect.dependabot.com/actions/checkout/pull/778">actions/checkout#778</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v2...v2.4.2">https://github.com/actions/checkout/compare/v2...v2.4.2</a></p>
<h2>v2.4.1</h2>
<ul>
<li>Fixed an issue where checkout failed to run in container jobs due to the new git setting <code>safe.directory</code></li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/blob/main/CHANGELOG.md">actions/checkout's changelog</a>.</em></p>
<blockquote>
<h2>v3.0.2</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/770">Add input <code>set-safe-directory</code></a></li>
</ul>
<h2>v3.0.1</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/762">Fixed an issue where checkout failed to run in container jobs due to the new git setting <code>safe.directory</code></a></li>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/744">Bumped various npm package versions</a></li>
</ul>
<h2>v3.0.0</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/689">Update to node 16</a></li>
</ul>
<h2>v2.3.1</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/284">Fix default branch resolution for .wiki and when using SSH</a></li>
</ul>
<h2>v2.3.0</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/278">Fallback to the default branch</a></li>
</ul>
<h2>v2.2.0</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/258">Fetch all history for all tags and branches when fetch-depth=0</a></li>
</ul>
<h2>v2.1.1</h2>
<ul>
<li>Changes to support GHES (<a href="https://github-redirect.dependabot.com/actions/checkout/pull/236">here</a> and <a href="https://github-redirect.dependabot.com/actions/checkout/pull/248">here</a>)</li>
</ul>
<h2>v2.1.0</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/191">Group output</a></li>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/199">Changes to support GHES alpha release</a></li>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/184">Persist core.sshCommand for submodules</a></li>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/163">Add support ssh</a></li>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/179">Convert submodule SSH URL to HTTPS, when not using SSH</a></li>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/157">Add submodule support</a></li>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/144">Follow proxy settings</a></li>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/141">Fix ref for pr closed event when a pr is merged</a></li>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/128">Fix issue checking detached when git less than 2.22</a></li>
</ul>
<h2>v2.0.0</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/108">Do not pass cred on command line</a></li>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/107">Add input persist-credentials</a></li>
<li><a href="https://github-redirect.dependabot.com/actions/checkout/pull/104">Fallback to REST API to download repo</a></li>
</ul>
<h2>v2 (beta)</h2>
<ul>
<li>Improved fetch performance
<ul>
<li>The default behavior now fetches only the SHA being checked-out</li>
</ul>
</li>
<li>Script authenticated git commands</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2541b12</code></a> Prepare changelog for v3.0.2. (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/777">#777</a>)</li>
<li><a href=""><code>0ffe6f9</code></a> Add set-safe-directory input to allow customers to take control. (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/770">#770</a>)</li>
<li><a href=""><code>dcd71f6</code></a> Enforce safe directory (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/762">#762</a>)</li>
<li><a href=""><code>add3486</code></a> Patch to fix the dependbot alert. (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/744">#744</a>)</li>
<li><a href=""><code>5126516</code></a> Bump minimist from 1.2.5 to 1.2.6 (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/741">#741</a>)</li>
<li><a href=""><code>d50f8ea</code></a> Add v3.0 release information to changelog (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/740">#740</a>)</li>
<li><a href=""><code>2d1c119</code></a> update test workflows to checkout v3 (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/709">#709</a>)</li>
<li><a href=""><code>a12a394</code></a> update readme for v3 (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/708">#708</a>)</li>
<li><a href=""><code>8f9e05e</code></a> Update to node 16 (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/689">#689</a>)</li>
<li><a href=""><code>230611d</code></a> Change secret name for PAT to not start with GITHUB_ (<a href="https://github-redirect.dependabot.com/actions/checkout/issues/623">#623</a>)</li>
<li>See full diff in <a href="https://github.com/actions/checkout/compare/v2.4.0...v3.0.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/checkout&package-manager=github_actions&previous-version=2.4.0&new-version=3.0.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6e9bda842372`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.