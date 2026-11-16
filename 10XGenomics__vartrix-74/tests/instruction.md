# Issue

**Title:** Bump crossbeam-deque from 0.7.1 to 0.7.4

## Description

Bumps [crossbeam-deque](https://github.com/crossbeam-rs/crossbeam) from 0.7.1 to 0.7.4.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/crossbeam-rs/crossbeam/blob/master/CHANGELOG.md">crossbeam-deque's changelog</a>.</em></p>
<blockquote>
<h1>Version 0.8.1</h1>
<ul>
<li>Support targets that do not have atomic CAS on stable Rust (<a href="https://github-redirect.dependabot.com/crossbeam-rs/crossbeam/issues/698">#698</a>)</li>
</ul>
<h1>Version 0.8.0</h1>
<ul>
<li>Bump the minimum supported Rust version to 1.36.</li>
<li>Bump <code>crossbeam-channel</code> to <code>0.5</code>.</li>
<li>Bump <code>crossbeam-deque</code> to <code>0.8</code>.</li>
<li>Bump <code>crossbeam-epoch</code> to <code>0.9</code>.</li>
<li>Bump <code>crossbeam-queue</code> to <code>0.3</code>.</li>
<li>Bump <code>crossbeam-utils</code> to <code>0.8</code>.</li>
</ul>
<h1>Version 0.7.3</h1>
<ul>
<li>Fix breakage with nightly feature due to <a href="https://github-redirect.dependabot.com/rust-lang/rust/issues/65214">rust-lang/rust#65214</a>.</li>
<li>Bump <code>crossbeam-channel</code> to <code>0.4</code>.</li>
<li>Bump <code>crossbeam-epoch</code> to <code>0.8</code>.</li>
<li>Bump <code>crossbeam-queue</code> to <code>0.2</code>.</li>
<li>Bump <code>crossbeam-utils</code> to <code>0.7</code>.</li>
</ul>
<h1>Version 0.7.2</h1>
<ul>
<li>Bump <code>crossbeam-channel</code> to <code>0.3.9</code>.</li>
<li>Bump <code>crossbeam-epoch</code> to <code>0.7.2</code>.</li>
<li>Bump <code>crossbeam-utils</code> to <code>0.6.6</code>.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>0485137</code></a> Prepare for the next release</li>
<li><a href=""><code>180b462</code></a> Fix deque steal race condition</li>
<li><a href=""><code>48b13dc</code></a> Bump crossbeam-channel to v0.4.4</li>
<li><a href=""><code>679dac8</code></a> Bump crossbeam-channel to v0.4.3</li>
<li><a href=""><code>f652c6a</code></a> Change crossbeam-channel's license to MIT OR Apache-2.0.</li>
<li><a href=""><code>149a3c9</code></a> Release crossbeam-queue 0.2.3</li>
<li><a href=""><code>18363b5</code></a> Merge <a href="https://github-redirect.dependabot.com/crossbeam-rs/crossbeam/issues/476">#476</a></li>
<li><a href=""><code>e32c891</code></a> Release new versions</li>
<li><a href=""><code>6d6591a</code></a> Merge <a href="https://github-redirect.dependabot.com/crossbeam-rs/crossbeam/issues/474">#474</a></li>
<li><a href=""><code>528c3ca</code></a> Undo bump of rand as it bumps MSRV</li>
<li>Additional commits viewable in <a href="https://github.com/crossbeam-rs/crossbeam/compare/crossbeam-deque-0.7.1...crossbeam-deque-0.7.4">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=crossbeam-deque&package-manager=cargo&previous-version=0.7.1&new-version=0.7.4)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot use these labels` will set the current labels as the default for future PRs for this repo and language
- `@dependabot use these reviewers` will set the current reviewers as the default for future PRs for this repo and language
- `@dependabot use these assignees` will set the current assignees as the default for future PRs for this repo and language
- `@dependabot use this milestone` will set the current milestone as the default for future PRs for this repo and language

You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/10XGenomics/vartrix/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bf8e95056b48`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.