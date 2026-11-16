# Issue

**Title:** [DEPENDABOT]: Bump actions/download-artifact from 2.1.0 to 3.0.2

## Description

Bumps [actions/download-artifact](https://github.com/actions/download-artifact) from 2.1.0 to 3.0.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/download-artifact/releases">actions/download-artifact's releases</a>.</em></p>
<blockquote>
<h2>v3.0.2</h2>
<ul>
<li>Bump <code>@actions/artifact</code> to v1.1.1 - <a href="https://github-redirect.dependabot.com/actions/download-artifact/pull/195">actions/download-artifact#195</a></li>
<li>Fixed a bug in Node16 where if an HTTP download finished too quickly (&lt;1ms, e.g. when it's mocked) we attempt to delete a temp file that has not been created yet <a href="hhttps://github-redirect.dependabot.com/actions/toolkit/pull/1278">actions/toolkit#1278</a></li>
</ul>
<h2>v3.0.1</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/actions/download-artifact/pull/178">Bump <code>@​actions/core</code> to 1.10.0</a></li>
</ul>
<h2>v3.0.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Update default runtime to node16 (<a href="https://github-redirect.dependabot.com/actions/download-artifact/pull/134">actions/download-artifact#134</a>)</li>
<li>Update package-lock.json file version to 2 (<a href="https://github-redirect.dependabot.com/actions/download-artifact/pull/136">actions/download-artifact#136</a>)</li>
</ul>
<h3>Breaking Changes</h3>
<p>With the update to Node 16, all scripts will now be run with Node 16 rather than Node 12.</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>9bc31d5</code></a> Update to latest actions/artifact NPM package (<a href="https://github-redirect.dependabot.com/actions/download-artifact/issues/195">#195</a>)</li>
<li><a href=""><code>d2278a1</code></a> Update release-new-action-version.yml (<a href="https://github-redirect.dependabot.com/actions/download-artifact/issues/196">#196</a>)</li>
<li><a href=""><code>c1a6d8f</code></a> Update codeql-analysis.yml (<a href="https://github-redirect.dependabot.com/actions/download-artifact/issues/197">#197</a>)</li>
<li><a href=""><code>9782bd6</code></a> Update <code>@​actions/core</code> to 1.10.0 (<a href="https://github-redirect.dependabot.com/actions/download-artifact/issues/178">#178</a>)</li>
<li><a href=""><code>076f0f7</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/download-artifact/issues/156">#156</a> from actions/dependabot/npm_and_yarn/ansi-regex-4.1.1</li>
<li><a href=""><code>7151be3</code></a> Bump ansi-regex from 4.1.0 to 4.1.1</li>
<li><a href=""><code>51cbdc4</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/download-artifact/issues/152">#152</a> from actions/dependabot/npm_and_yarn/minimist-1.2.6</li>
<li><a href=""><code>e89a529</code></a> Bump minimist from 1.2.5 to 1.2.6</li>
<li><a href=""><code>fb598a6</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/download-artifact/issues/136">#136</a> from actions/jtamsut/update-lockfile-version</li>
<li><a href=""><code>a4a09c5</code></a> regenerate index.js</li>
<li>Additional commits viewable in <a href="https://github.com/actions/download-artifact/compare/v2.1.0...v3.0.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/download-artifact&package-manager=github_actions&previous-version=2.1.0&new-version=3.0.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b61721007d9f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.