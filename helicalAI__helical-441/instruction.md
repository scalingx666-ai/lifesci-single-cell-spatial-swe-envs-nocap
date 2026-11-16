# Issue

**Title:** build(deps): bump hydra-core from 1.3.2 to 1.3.7

## Description

Bumps [hydra-core](https://github.com/facebookresearch/hydra) from 1.3.2 to 1.3.7.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/facebookresearch/hydra/releases">hydra-core's releases</a>.</em></p>
<blockquote>
<h2>Hydra 1.3.7</h2>
<h2>What's Changed</h2>
<ul>
<li>Strengthen defense-in-depth checks for configured targets, Python runtime state, process-environment mutation, and logging formatters. These checks are not a complete security boundary. (<a href="">#3442</a>)</li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/hydra-ecosystem/hydra/compare/v1.3.6...v1.3.7">https://github.com/hydra-ecosystem/hydra/compare/v1.3.6...v1.3.7</a></p>
<h2>Hydra 1.3.6</h2>
<h2>What's Changed</h2>
<ul>
<li>Harden instantiate authorization against unsafe aliases and callable results. (<a href="">#3410</a>)</li>
<li>Apply Hydra's target blacklist to Python logging configuration. (<a href="">#3418</a>)</li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/hydra-ecosystem/hydra/compare/v1.3.5...v1.3.6">https://github.com/hydra-ecosystem/hydra/compare/v1.3.5...v1.3.6</a></p>
<h2>Hydra 1.3.5</h2>
<h2>What's Changed</h2>
<ul>
<li>Warn Hydra 1.3 users relying on Hydra 1.1 behavior  (<a href="">#3347</a>)</li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/facebookresearch/hydra/compare/v1.3.4...v1.3.5">https://github.com/facebookresearch/hydra/compare/v1.3.4...v1.3.5</a></p>
<h2>Hydra 1.3.4</h2>
<p>Security patch release for the 1.3 line.</p>
<ul>
<li>Add a blocklist to <code>hydra.utils.instantiate()</code> for security-sensitive <code>_target_</code> callables.</li>
</ul>
<p>Users on Hydra 1.3 should upgrade from <code>hydra-core&lt;=1.3.3</code> to <code>hydra-core==1.3.4</code>.</p>
<p>Hydra 1.3.3 fixes source builds with modern setuptools by removing the setup.py dependency on pkg_resources. Fixes <a href="">#3207</a>.</p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/hydra-ecosystem/hydra/blob/v1.3.7/NEWS.md">hydra-core's changelog</a>.</em></p>
<blockquote>
<h1>1.3.7 (2026-09-14)</h1>
<h3>Bug Fixes</h3>
<ul>
<li>Strengthen defense-in-depth checks for configured targets, Python runtime state,
process-environment mutation, and logging formatters. These checks are not a
complete security boundary. (<a href="">#3442</a>)
1.3.6 (2026-08-29)
==================</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li>Harden instantiate authorization against unsafe aliases and callable results.
(<a href="">#3410</a>)</li>
<li>Apply Hydra's target blocklist to Python logging configuration.
(<a href="">#3418</a>)</li>
</ul>
<h1>1.3.5 (2026-08-06)</h1>
<h3>API Change (Renames, deprecations and removals)</h3>
<ul>
<li>Warn Hydra 1.3 applications that rely on Hydra 1.1 compatibility before
upgrading to Hydra 1.4. (<a href="">#3334</a>)
1.3.4 (2026-07-05)
==================</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li>Add an instantiate target blocklist for security-sensitive callables. (<a href="">#3259</a>)
1.3.3 (2026-06-11)
==================</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li>Remove the setup.py dependency on pkg_resources for source builds. (<a href="">#3207</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>81715a5</code></a> Prepare hydra-core 1.3.7 release</li>
<li><a href=""><code>4720dfc</code></a> Merge commit from fork</li>
<li><a href=""><code>27df755</code></a> Prepare Hydra 1.3.6 release</li>
<li><a href=""><code>ff3e4db</code></a> Harden logging target resolution on 1.3 (<a href="">#3420</a>)</li>
<li><a href=""><code>aa102ea</code></a> Harden deferred instantiate dispatch on 1.3</li>
<li><a href=""><code>2c82bbb</code></a> Backport instantiate target authorization hardening to 1.3 (<a href="">#3413</a>)</li>
<li><a href=""><code>06613ce</code></a> Bump Hydra to 1.3.6.dev0</li>
<li><a href=""><code>51647a2</code></a> Release Hydra 1.3.5</li>
<li><a href=""><code>445b0a7</code></a> Warn Hydra 1.3 users relying on 1.1 compatibility (<a href="">#3347</a>)</li>
<li><a href=""><code>81070c4</code></a> Release Hydra 1.3.4</li>
<li>Additional commits viewable in <a href="https://github.com/facebookresearch/hydra/compare/v1.3.2...v1.3.7">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=hydra-core&package-manager=pip&previous-version=1.3.2&new-version=1.3.7)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/helicalAI/helical/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eefd9c20ed49`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.