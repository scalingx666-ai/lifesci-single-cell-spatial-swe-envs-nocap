# Issue

**Title:** build(deps): bump actions/cache from 5.0.5 to 6.1.0

## Description

Bumps [actions/cache](https://github.com/actions/cache) from 5.0.5 to 6.1.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/cache/releases">actions/cache's releases</a>.</em></p>
<blockquote>
<h2>v6.1.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Bump <code>@​actions/cache</code> to v6.1.0 - handle read-only cache access by <a href="https://github.com/jasongin"><code>@​jasongin</code></a> in <a href="">actions/cache#1768</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/cache/compare/v6...v6.1.0">https://github.com/actions/cache/compare/v6...v6.1.0</a></p>
<h2>v6.0.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Update packages, migrate to ESM by <a href="https://github.com/Samirat"><code>@​Samirat</code></a> in <a href="">actions/cache#1760</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/cache/compare/v5...v6.0.0">https://github.com/actions/cache/compare/v5...v6.0.0</a></p>
<h2>v5.1.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Bump <code>@​actions/cache</code> to v5.1.0 - handle read-only cache access by <a href="https://github.com/jasongin"><code>@​jasongin</code></a> in <a href="">actions/cache#1775</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/cache/compare/v5...v5.1.0">https://github.com/actions/cache/compare/v5...v5.1.0</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/actions/cache/blob/main/RELEASES.md">actions/cache's changelog</a>.</em></p>
<blockquote>
<h1>Releases</h1>
<h2>How to prepare a release</h2>
<blockquote>
<p>[!NOTE]
Relevant for maintainers with write access only.</p>
</blockquote>
<ol>
<li>Switch to a new branch from <code>main</code>.</li>
<li>Run <code>npm test</code> to ensure all tests are passing.</li>
<li>Update the version in <a href="https://github.com/actions/cache/blob/main/package.json"><code>https://github.com/actions/cache/blob/main/package.json</code></a>.</li>
<li>Run <code>npm run build</code> to update the compiled files.</li>
<li>Update this <a href="https://github.com/actions/cache/blob/main/RELEASES.md"><code>https://github.com/actions/cache/blob/main/RELEASES.md</code></a> with the new version and changes in the <code>## Changelog</code> section.</li>
<li>Run <code>licensed cache</code> to update the license report.</li>
<li>Run <code>licensed status</code> and resolve any warnings by updating the <a href="https://github.com/actions/cache/blob/main/.licensed.yml"><code>https://github.com/actions/cache/blob/main/.licensed.yml</code></a> file with the exceptions.</li>
<li>Commit your changes and push your branch upstream.</li>
<li>Open a pull request against <code>main</code> and get it reviewed and merged.</li>
<li>Draft a new release <a href="https://github.com/actions/cache/releases">https://github.com/actions/cache/releases</a> use the same version number used in <code>package.json</code>
<ol>
<li>Create a new tag with the version number.</li>
<li>Auto generate release notes and update them to match the changes you made in <code>RELEASES.md</code>.</li>
<li>Toggle the set as the latest release option.</li>
<li>Publish the release.</li>
</ol>
</li>
<li>Navigate to <a href="https://github.com/actions/cache/actions/workflows/release-new-action-version.yml">https://github.com/actions/cache/actions/workflows/release-new-action-version.yml</a>
<ol>
<li>There should be a workflow run queued with the same version number.</li>
<li>Approve the run to publish the new version and update the major tags for this action.</li>
</ol>
</li>
</ol>
<h2>Changelog</h2>
<h3>6.1.0</h3>
<ul>
<li>Bump <code>@actions/cache</code> to v6.1.0 to pick up <a href="">actions/toolkit#2435 Handle cache write error due to read-only token</a></li>
<li>Switch redundant &quot;Cache save failed&quot; warning to debug log in save-only</li>
</ul>
<h3>6.0.0</h3>
<ul>
<li>Updated <code>@actions/cache</code> to ^6.0.1, <code>@actions/core</code> to ^3.0.1, <code>@actions/exec</code> to ^3.0.0, <code>@actions/io</code> to ^3.0.2</li>
<li>Migrated to ESM module system</li>
<li>Upgraded Jest to v30 and test infrastructure to be ESM compatible</li>
</ul>
<h3>5.0.4</h3>
<ul>
<li>Bump <code>minimatch</code> to v3.1.5 (fixes ReDoS via globstar patterns)</li>
<li>Bump <code>undici</code> to v6.24.1 (WebSocket decompression bomb protection, header validation fixes)</li>
<li>Bump <code>fast-xml-parser</code> to v5.5.6</li>
</ul>
<h3>5.0.3</h3>
<ul>
<li>Bump <code>@actions/cache</code> to v5.0.5 (Resolves: <a href="https://github.com/actions/cache/security/dependabot/33">https://github.com/actions/cache/security/dependabot/33</a>)</li>
<li>Bump <code>@actions/core</code> to v2.0.3</li>
</ul>
<h3>5.0.2</h3>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>55cc834</code></a> Merge pull request <a href="">#1768</a> from jasongin/readonly-cache</li>
<li><a href=""><code>d8cd72f</code></a> Bump <code>@​actions/cache</code> to v6.1.0 - handle cache write error due to RO token</li>
<li><a href=""><code>2c8a9bd</code></a> Merge pull request <a href="">#1760</a> from actions/samirat/esm_migration_and_package_update</li>
<li><a href=""><code>e9b91fd</code></a> Prettier fixes</li>
<li><a href=""><code>e4884b8</code></a> Rebuild dist</li>
<li><a href=""><code>10baf01</code></a> Fixed licenses</li>
<li><a href=""><code>e39b386</code></a> Fix test mock return order</li>
<li><a href=""><code>b692820</code></a> PR feedback</li>
<li><a href=""><code>6074912</code></a> Rebuild dist bundles as ESM to match type:module</li>
<li><a href=""><code>5a912e8</code></a> Fix lint and jest issues</li>
<li>Additional commits viewable in <a href="https://github.com/actions/cache/compare/27d5ce7f107fe9357f9df03efb73ab90386fccae...55cc8345863c7cc4c66a329aec7e433d2d1c52a9">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/cache&package-manager=github_actions&previous-version=5.0.5&new-version=6.1.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `550ab7c5bee8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.