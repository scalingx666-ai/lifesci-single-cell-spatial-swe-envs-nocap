# Issue

**Title:** [DEPENDABOT]: Bump actions/cache from 3.0.7 to 3.0.8

## Description

Bumps [actions/cache](https://github.com/actions/cache) from 3.0.7 to 3.0.8.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/cache/releases">actions/cache's releases</a>.</em></p>
<blockquote>
<h2>v3.0.8</h2>
<h2>What's Changed</h2>
<ul>
<li>Fix <code>zstd</code> not working for windows on gnu tar in issues.</li>
<li>Allow users to provide a custom timeout as input for aborting cache segment download using the environment variable <code>SEGMENT_DOWNLOAD_TIMEOUT_MIN</code>. Default is 60 minutes.</li>
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
<h3>3.0.8</h3>
<ul>
<li>Fix zstd not working for windows on gnu tar in issues <a href="https://github-redirect.dependabot.com/actions/cache/issues/888">#888</a> and <a href="https://github-redirect.dependabot.com/actions/cache/issues/891">#891</a>.</li>
<li>Allowing users to provide a custom timeout as input for aborting download of a cache segment using an environment variable <code>SEGMENT_DOWNLOAD_TIMEOUT_MIN</code>. Default is 60 minutes.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>fd5de65</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/actions/cache/issues/899">#899</a> from actions/kotewar/download-and-compression-fix</li>
<li><a href=""><code>d49b6bb</code></a> Updated actions/cache toolkit dep to v3.0.4</li>
<li>See full diff in <a href="https://github.com/actions/cache/compare/v3.0.7...v3.0.8">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/cache&package-manager=github_actions&previous-version=3.0.7&new-version=3.0.8)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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