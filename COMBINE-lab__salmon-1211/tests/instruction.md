# Issue

**Title:** chore(deps): bump sharp from 0.35.3 to 0.35.4 in /website

## Description

Bumps [sharp](https://github.com/lovell/sharp) from 0.35.3 to 0.35.4.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/lovell/sharp/releases">sharp's releases</a>.</em></p>
<blockquote>
<h2>v0.35.4</h2>
<p><a href="https://github.com/lovell/sharp-libvips/releases/tag/v1.3.3">https://github.com/lovell/sharp-libvips/releases/tag/v1.3.3</a></p>
<ul>
<li>
<p>Bound resize dimensions to coordinate limit.</p>
</li>
<li>
<p>Bound composite left and top to coordinate limit.
<a href="">#4564</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Round palette bit depth up for png and gif colours.
<a href="">#4569</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Ensure tiff.subifd input option is used.
<a href="">#4572</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Ensure <code>info.pages</code> is correct when limiting input page range.
<a href="">#4578</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Improve support for input Streams finishing before output is requested.
<a href="">#4584</a>
<a href="https://github.com/Jaybhade"><code>@​Jaybhade</code></a></p>
</li>
</ul>
<h2>v0.35.4-rc.0</h2>
<ul>
<li>
<p>Upgrade to libvips v8.18.6 for upstream bug fixes.</p>
</li>
<li>
<p>Bound resize dimensions to coordinate limit.</p>
</li>
<li>
<p>Bound composite left and top to coordinate limit.
<a href="">#4564</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Round palette bit depth up for png and gif colours.
<a href="">#4569</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Ensure tiff.subifd input option is used.
<a href="">#4572</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Ensure <code>info.pages</code> is correct when limiting input page range.
<a href="">#4578</a>
<a href="https://github.com/metsw24-max"><code>@​metsw24-max</code></a></p>
</li>
<li>
<p>Improve support for input Streams finishing before output is requested.
<a href="">#4584</a>
<a href="https://github.com/Jaybhade"><code>@​Jaybhade</code></a></p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7f1a0a2</code></a> Release v0.35.4</li>
<li><a href=""><code>f927818</code></a> Upgrade to sharp-libvips v1.3.3</li>
<li><a href=""><code>e802092</code></a> Prerelease v0.35.4-rc.0</li>
<li><a href=""><code>e13eb2f</code></a> CI: Fix wasm32 build (<a href="">#4589</a>)</li>
<li><a href=""><code>a82a0b3</code></a> Upgrade to libvips v8.18.6</li>
<li><a href=""><code>8044fe4</code></a> Bound resize dimensions to coordinate limit</li>
<li><a href=""><code>147f859</code></a> Docs: changelog entries for <a href="">#4578</a> <a href="">#4584</a></li>
<li><a href=""><code>ee5bfb8</code></a> Tests: use yauzl directly rather than via extract-zip wrapper</li>
<li><a href=""><code>7a77889</code></a> Bump uraimo/run-on-arch-action from 3.1.0 to 3.2.0 (<a href="">#4588</a>)</li>
<li><a href=""><code>ea5bef2</code></a> Improve support for input Streams finishing before output is requested (<a href="">#4584</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/lovell/sharp/compare/v0.35.3...v0.35.4">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=sharp&package-manager=npm_and_yarn&previous-version=0.35.3&new-version=0.35.4)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/COMBINE-lab/salmon/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3be8b31d312`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.