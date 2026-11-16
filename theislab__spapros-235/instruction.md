# Issue

**Title:** [DEPENDABOT]: Bump actions/upload-artifact from 2.3.1 to 3.1.0

## Description

Bumps [actions/upload-artifact](https://github.com/actions/upload-artifact) from 2.3.1 to 3.1.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/upload-artifact/releases">actions/upload-artifact's releases</a>.</em></p>
<blockquote>
<h2>v3.1.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Bump <code>@​actions/artifact</code> to v1.1.0 (<a href="https://github-redirect.dependabot.com/actions/upload-artifact/pull/327">actions/upload-artifact#327</a>)
<ul>
<li>Adds checksum headers on artifact upload (<a href="https://github-redirect.dependabot.com/actions/toolkit/pull/1095">actions/toolkit#1095</a>) (<a href="https://github-redirect.dependabot.com/actions/toolkit/pull/1063">actions/toolkit#1063</a>)</li>
</ul>
</li>
</ul>
<h2>v3.0.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Update default runtime to node16 (<a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/293">#293</a>)</li>
<li>Update package-lock.json file version to 2 (<a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/302">#302</a>)</li>
</ul>
<h3>Breaking Changes</h3>
<p>With the update to Node 16, all scripts will now be run with Node 16 rather than Node 12.</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>3cea537</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/327">#327</a> from actions/robherley/artifact-1.1.0</li>
<li><a href=""><code>849aa77</code></a> nvm use 12 &amp; npm run release</li>
<li><a href=""><code>4d39869</code></a> recompile with correct ncc version</li>
<li><a href=""><code>2e0d362</code></a> bump <code>@​actions/artifact</code> to 1.1.0</li>
<li><a href=""><code>09a5d6a</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/320">#320</a> from actions/dependabot/npm_and_yarn/ansi-regex-4.1.1</li>
<li><a href=""><code>189315d</code></a> Bump ansi-regex from 4.1.0 to 4.1.1</li>
<li><a href=""><code>d159c2d</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/297">#297</a> from actions/dependabot/npm_and_yarn/ajv-6.12.6</li>
<li><a href=""><code>c26a7ba</code></a> Bump ajv from 6.11.0 to 6.12.6</li>
<li><a href=""><code>6ed6c72</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/303">#303</a> from actions/dependabot/npm_and_yarn/yargs-parser-13.1.2</li>
<li><a href=""><code>2aeee26</code></a> Bump yargs-parser from 13.1.1 to 13.1.2</li>
<li>Additional commits viewable in <a href="https://github.com/actions/upload-artifact/compare/v2.3.1...v3.1.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/upload-artifact&package-manager=github_actions&previous-version=2.3.1&new-version=3.1.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `626e6b0aba9a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.