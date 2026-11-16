# Issue

**Title:** [DEPENDABOT]: Bump actions/upload-artifact from 2.2.4 to 2.3.1

## Description

Bumps [actions/upload-artifact](https://github.com/actions/upload-artifact) from 2.2.4 to 2.3.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/upload-artifact/releases">actions/upload-artifact's releases</a>.</em></p>
<blockquote>
<h2>v2.3.1</h2>
<p>Fix for empty fails on Windows failing on upload <a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/281">#281</a></p>
<h2>v2.3.0 Upload Artifact</h2>
<ul>
<li>Optimizations for faster uploads of larger files that are already compressed</li>
<li>Significantly improved logging when there are chunked uploads</li>
<li>Clarifications in logs around the upload size and prohibited characters that aren't allowed in the artifact name or any uploaded files</li>
<li>Various other small bugfixes &amp; optimizations</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>82c141c</code></a> Bump <code>@​actions/artifact</code> to version 0.6.1 (<a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/286">#286</a>)</li>
<li><a href=""><code>da838ae</code></a> Bump <code>@​actions/artifact</code> to version 0.6.0 (<a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/280">#280</a>)</li>
<li><a href=""><code>f4ac36d</code></a> Improve readme (<a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/278">#278</a>)</li>
<li><a href=""><code>5f375cc</code></a> Document how to correctly use environment variables for path input (<a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/274">#274</a>)</li>
<li><a href=""><code>a009a66</code></a> Create release-new-action-version.yml (<a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/277">#277</a>)</li>
<li><a href=""><code>b9bb657</code></a> Bump tmpl from 1.0.4 to 1.0.5 (<a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/250">#250</a>)</li>
<li><a href=""><code>0b3de3e</code></a> Fix <code>README.md</code> links and some formatting updates (<a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/273">#273</a>)</li>
<li><a href=""><code>54f3f7f</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/271">#271</a> from actions/robherley/dupe-issue-template</li>
<li><a href=""><code>f061e61</code></a> rm dupe security vulnerability from issue template</li>
<li><a href=""><code>ee82d6a</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/upload-artifact/issues/269">#269</a> from actions/robherley/update-issue-templates</li>
<li>Additional commits viewable in <a href="https://github.com/actions/upload-artifact/compare/v2.2.4...v2.3.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/upload-artifact&package-manager=github_actions&previous-version=2.2.4&new-version=2.3.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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