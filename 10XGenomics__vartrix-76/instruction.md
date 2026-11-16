# Issue

**Title:** Bump smallvec from 0.6.10 to 0.6.14

## Description

Bumps [smallvec](https://github.com/servo/rust-smallvec) from 0.6.10 to 0.6.14.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/servo/rust-smallvec/releases">smallvec's releases</a>.</em></p>
<blockquote>
<h2>v0.6.14</h2>
<ul>
<li>Fix a possible buffer overflow in <code>insert_many</code> (<a href="https://github-redirect.dependabot.com/servo/rust-smallvec/issues/252">#252</a>, <a href="https://github-redirect.dependabot.com/servo/rust-smallvec/issues/254">#254</a>).</li>
</ul>
<h2>v0.6.13</h2>
<ul>
<li>Use the <code>maybe-unit</code> crate in place of soon-to-be-deprecated <code>std::mem::uninitialized</code> (<a href="https://github-redirect.dependabot.com/servo/rust-smallvec/issues/180">#180</a>). When built with Rust 1.36 or later, this fixes a source of undefined behavior. It also fixes deprecation warnings in Rust 1.39 and later, and test failures when run in MIRI. In Rust 1.35 and earlier it provides some safety improvements but does not completely eliminate undefined behavior. (However, we are not aware of any cases where the undefined behavior causes bugs in practice in those toolchains.)</li>
</ul>
<h2>v0.6.12</h2>
<ul>
<li>Move code using <code>default fn</code> into its own module (<a href="https://github-redirect.dependabot.com/servo/rust-smallvec/issues/161">#161</a>).</li>
</ul>
<h2>v0.6.11</h2>
<ul>
<li>The unstable <code>alloc</code> feature is no longer needed.  This crate can now build with the <code>std</code> feature disabled on stable Rust 1.36 or later (<a href="https://github-redirect.dependabot.com/servo/rust-smallvec/issues/159">#159</a>).</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>5757ac5</code></a> Fix potential buffer overflow in <code>insert_many</code></li>
<li><a href=""><code>7852204</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/servo/rust-smallvec/issues/180">#180</a> from mbrubeck/maybe_uninit</li>
<li><a href=""><code>58d5416</code></a> Add a test for <a href="https://github-redirect.dependabot.com/servo/rust-smallvec/issues/139">#139</a>.</li>
<li><a href=""><code>26ea2ca</code></a> Run miri in CI</li>
<li><a href=""><code>e64afc8</code></a> Use MaybeUninit for storage of inline items.</li>
<li><a href=""><code>87f156b</code></a> Version 0.6.12</li>
<li><a href=""><code>e60df76</code></a> Version 0.6.11</li>
<li><a href=""><code>3ee6d1e</code></a> Auto merge of <a href="https://github-redirect.dependabot.com/servo/rust-smallvec/issues/161">#161</a> - Centril:master, r=emilio</li>
<li><a href=""><code>92122e2</code></a> Move use of 'default fn' to its own module.</li>
<li><a href=""><code>c83bb71</code></a> Auto merge of <a href="https://github-redirect.dependabot.com/servo/rust-smallvec/issues/159">#159</a> - CryZe:no-std, r=emilio</li>
<li>Additional commits viewable in <a href="https://github.com/servo/rust-smallvec/compare/v0.6.10...v0.6.14">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=smallvec&package-manager=cargo&previous-version=0.6.10&new-version=0.6.14)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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