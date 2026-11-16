# Issue

**Title:** Bump actions/download-artifact from 1 to 3

## Description

Bumps [actions/download-artifact](https://github.com/actions/download-artifact) from 1 to 3.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/download-artifact/releases">actions/download-artifact's releases</a>.</em></p>
<blockquote>
<h2>v3.0.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Update default runtime to node16 (<a href="">actions/download-artifact#134</a>)</li>
<li>Update package-lock.json file version to 2 (<a href="">actions/download-artifact#136</a>)</li>
</ul>
<h3>Breaking Changes</h3>
<p>With the update to Node 16, all scripts will now be run with Node 16 rather than Node 12.</p>
<h2>v2.1.1</h2>
<ul>
<li>Bump <code>@actions/core</code> to the latest version to prevent breaking changes once <code>set-output</code> and <code>save-state</code> commands are deprecated <a href="">#21</a></li>
</ul>
<h2>v2.1.0 Download Artifact</h2>
<ul>
<li>Improved output &amp; logging</li>
<li>Fixed issue where downloading all artifacts could cause display percentages to be over 100%</li>
<li>Various small bug fixes &amp; improvements</li>
</ul>
<h2>v2.0.10</h2>
<ul>
<li>Retry on HTTP 500 responses from the service</li>
</ul>
<h2>v2.0.9</h2>
<ul>
<li>Fixes to proxy related issues</li>
</ul>
<h2>v2.0.8</h2>
<ul>
<li>Improvements to retryability if an error is encountered during artifact download</li>
</ul>
<h2>v2.0.7 download-artifact</h2>
<ul>
<li>Improved download retry-ability if a partial download is encountered</li>
</ul>
<h2>v2.0.6</h2>
<p>Update actions/core NPM package that is used internally</p>
<h2>v2.0.5</h2>
<ul>
<li>Add Third Party License Information</li>
</ul>
<h2>v2.0.4</h2>
<ul>
<li>Use the latest version of the <code>@actions/artifact</code> NPM package</li>
</ul>
<h2>v2.0.3</h2>
<ul>
<li>Misc improvements</li>
</ul>
<h2>v2.0.2</h2>
<ul>
<li>Support for tilde expansion</li>
</ul>
<h2>v2.0.1</h2>
<ul>
<li>Download path output</li>
<li>Improved logging</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>9bc31d5</code></a> Update to latest actions/artifact NPM package (<a href="">#195</a>)</li>
<li><a href=""><code>d2278a1</code></a> Update release-new-action-version.yml (<a href="">#196</a>)</li>
<li><a href=""><code>c1a6d8f</code></a> Update codeql-analysis.yml (<a href="">#197</a>)</li>
<li><a href=""><code>9782bd6</code></a> Update <code>@​actions/core</code> to 1.10.0 (<a href="">#178</a>)</li>
<li><a href=""><code>076f0f7</code></a> Merge pull request <a href="">#156</a> from actions/dependabot/npm_and_yarn/ansi-regex-4.1.1</li>
<li><a href=""><code>7151be3</code></a> Bump ansi-regex from 4.1.0 to 4.1.1</li>
<li><a href=""><code>51cbdc4</code></a> Merge pull request <a href="">#152</a> from actions/dependabot/npm_and_yarn/minimist-1.2.6</li>
<li><a href=""><code>e89a529</code></a> Bump minimist from 1.2.5 to 1.2.6</li>
<li><a href=""><code>fb598a6</code></a> Merge pull request <a href="">#136</a> from actions/jtamsut/update-lockfile-version</li>
<li><a href=""><code>a4a09c5</code></a> regenerate index.js</li>
<li>Additional commits viewable in <a href="https://github.com/actions/download-artifact/compare/v1...v3">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/download-artifact&package-manager=github_actions&previous-version=1&new-version=3)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ea6a3eb721f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.