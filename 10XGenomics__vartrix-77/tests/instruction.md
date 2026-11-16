# Issue

**Title:** Bump ordered-float from 1.0.2 to 1.1.1

## Description

Bumps [ordered-float](https://github.com/reem/rust-ordered-float) from 1.0.2 to 1.1.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/reem/rust-ordered-float/releases">ordered-float's releases</a>.</em></p>
<blockquote>
<h2>v1.1.1</h2>
<ul>
<li>Make assignment operators panic safe (<a href="https://github-redirect.dependabot.com/reem/rust-ordered-float/issues/71">#71</a>). This fixes a bug that could cause undefined behavior in safe code.</li>
</ul>
<h2>v1.1.0</h2>
<ul>
<li>Implement Sum and Product traits for NotNan (<a href="https://github-redirect.dependabot.com/reem/rust-ordered-float/issues/65">#65</a>).</li>
<li>Implement Neg and Zero traits for OrderedFloat (<a href="https://github-redirect.dependabot.com/reem/rust-ordered-float/issues/60">#60</a>, <a href="https://github-redirect.dependabot.com/reem/rust-ordered-float/issues/66">#66</a>).</li>
<li>Implement Add, Sub, Mul, and Div traits for OrderedFloat.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ebbbb47</code></a> Version 1.1.1</li>
<li><a href=""><code>da4a8dd</code></a> Make assignment operators panic safe</li>
<li><a href=""><code>96672a8</code></a> Version 1.1.0</li>
<li><a href=""><code>7084878</code></a> impl Add/Sub/Mul/Div for OrderedFloat</li>
<li><a href=""><code>57e16fd</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/reem/rust-ordered-float/issues/66">#66</a> from Uriopass/patch-1</li>
<li><a href=""><code>9a241dc</code></a> Add Zero impl for OrderedFloat</li>
<li><a href=""><code>90f4ca8</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/reem/rust-ordered-float/issues/65">#65</a> from bennofs/master</li>
<li><a href=""><code>eae4033</code></a> Add Sum/Product impls for NotNan</li>
<li><a href=""><code>06afbc9</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/reem/rust-ordered-float/issues/60">#60</a> from wookietreiber/topic/neg</li>
<li><a href=""><code>9013e4c</code></a> adds neg for ordered float</li>
<li>See full diff in <a href="https://github.com/reem/rust-ordered-float/compare/v1.0.2...v1.1.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=ordered-float&package-manager=cargo&previous-version=1.0.2&new-version=1.1.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `586b2ad1241e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.