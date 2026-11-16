# Issue

**Title:** [DEPENDABOT]: Bump codecov/codecov-action from 1.5.2 to 2.0.1

## Description

Bumps [codecov/codecov-action](https://github.com/codecov/codecov-action) from 1.5.2 to 2.0.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/codecov/codecov-action/releases">codecov/codecov-action's releases</a>.</em></p>
<blockquote>
<h2>v2.0.1</h2>
<h3>Fixes</h3>
<ul>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/424">#424</a> fix: Issue in building all deep dependencies</li>
</ul>
<h2>v2.0.0</h2>
<p>On February 1, 2022, the <code>v1</code> uploader will be full sunset and no longer function. This is due
to the deprecation of the underlying bash uploader. This version uses the new <a href="https://github.com/codecov/uploader">uploader</a>.</p>
<p>The <code>v2</code> Action downloads, verifies, and runs the Codecov binary.</p>
<h3>Breaking Changes</h3>
<ul>
<li>Multiple fields have not been transferred from the bash uploader or have been deprecated. Notably
many of the <code>functionalities</code> and <code>gcov_</code> arguments have been removed. Please check the documentation
for the full list.</li>
</ul>
<h3>Features</h3>
<ul>
<li><code>dry-run</code> argument allows Codecov flow without uploading reports to Codecov</li>
<li>(Enterprise only) <code>slug</code> allows specifying the repository slug manually</li>
<li>(Enterprise only) <code>url</code> allows changing the upload host</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/codecov/codecov-action/blob/master/CHANGELOG.md">codecov/codecov-action's changelog</a>.</em></p>
<blockquote>
<h2>2.0.1</h2>
<h3>Fixes</h3>
<ul>
<li><a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/424">#424</a> fix: Issue in building all deep dependencies</li>
</ul>
<h2>2.0.0</h2>
<p>On February 1, 2022, the <code>v1</code> uploader will be full sunset and no longer function. This is due
to the deprecation of the underlying bash uploader. This version uses the new <a href="https://github.com/codecov/uploader">uploader</a>.</p>
<p>The <code>v2</code> Action downloads, verifies, and runs the Codecov binary.</p>
<h3>Breaking Changes</h3>
<ul>
<li>Multiple fields have not been transferred from the bash uploader or have been deprecated. Notably
many of the <code>functionalities</code> and <code>gcov_</code> arguments have been removed. Please check the documentation
for the full list.</li>
</ul>
<h3>Features</h3>
<ul>
<li><code>dry-run</code> argument allows Codecov flow without uploading reports to Codecov</li>
<li>(Enterprise only) <code>slug</code> allows specifying the repository slug manually</li>
<li>(Enterprise only) <code>url</code> allows changing the upload host</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>c585afe</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/424">#424</a> from codecov/2.0.1-fix-deps</li>
<li><a href=""><code>852cffb</code></a> Remove dist/coverage</li>
<li><a href=""><code>d910efb</code></a> Update CHANGELOG</li>
<li><a href=""><code>439c1e5</code></a> Remove coverage folder</li>
<li><a href=""><code>fc5d663</code></a> fix: Hack to force asn1.js</li>
<li><a href=""><code>5c832ae</code></a> Force the dep</li>
<li><a href=""><code>71fa76a</code></a> fix: Add job to test no deps</li>
<li><a href=""><code>672fbdc</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/421">#421</a> from codecov/dependabot/npm_and_yarn/types/node-16.3.3</li>
<li><a href=""><code>1691a31</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/codecov/codecov-action/issues/422">#422</a> from codecov/dependabot/npm_and_yarn/vercel/ncc-0.29.0</li>
<li><a href=""><code>ad2b003</code></a> fix: Add deep deps</li>
<li>Additional commits viewable in <a href="https://github.com/codecov/codecov-action/compare/v1.5.2...v2.0.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=codecov/codecov-action&package-manager=github_actions&previous-version=1.5.2&new-version=2.0.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0aabb85e016f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.