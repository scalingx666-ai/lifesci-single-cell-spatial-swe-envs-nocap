# Issue

**Title:** Bump actions/download-artifact from 3 to 8

## Description

Bumps [actions/download-artifact](https://github.com/actions/download-artifact) from 3 to 8.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/download-artifact/releases">actions/download-artifact's releases</a>.</em></p>
<blockquote>
<h2>v8.0.0</h2>
<h2>v8 - What's new</h2>
<blockquote>
<p>[!IMPORTANT]
actions/download-artifact@v8 has been migrated to an ESM module. This should be transparent to the caller but forks might need to make significant changes.</p>
</blockquote>
<blockquote>
<p>[!IMPORTANT]
Hash mismatches will now error by default. Users can override this behavior with a setting change (see below).</p>
</blockquote>
<h3>Direct downloads</h3>
<p>To support direct uploads in <code>actions/upload-artifact</code>, the action will no longer attempt to unzip all downloaded files. Instead, the action checks the <code>Content-Type</code> header ahead of unzipping and skips non-zipped files. Callers wishing to download a zipped file as-is can also set the new <code>skip-decompress</code> parameter to <code>true</code>.</p>
<h3>Enforced checks (breaking)</h3>
<p>A previous release introduced digest checks on the download. If a download hash didn't match the expected hash from the server, the action would log a warning. Callers can now configure the behavior on mismatch with the <code>digest-mismatch</code> parameter. To be secure by default, we are now defaulting the behavior to <code>error</code> which will fail the workflow run.</p>
<h3>ESM</h3>
<p>To support new versions of the @actions/* packages, we've upgraded the package to ESM.</p>
<h2>What's Changed</h2>
<ul>
<li>Don't attempt to un-zip non-zipped downloads by <a href="https://github.com/danwkennedy"><code>@​danwkennedy</code></a> in <a href="">actions/download-artifact#460</a></li>
<li>Add a setting to specify what to do on hash mismatch and default it to <code>error</code> by <a href="https://github.com/danwkennedy"><code>@​danwkennedy</code></a> in <a href="">actions/download-artifact#461</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/download-artifact/compare/v7...v8.0.0">https://github.com/actions/download-artifact/compare/v7...v8.0.0</a></p>
<h2>v7.0.0</h2>
<h2>v7 - What's new</h2>
<blockquote>
<p>[!IMPORTANT]
actions/download-artifact@v7 now runs on Node.js 24 (<code>runs.using: node24</code>) and requires a minimum Actions Runner version of 2.327.1. If you are using self-hosted runners, ensure they are updated before upgrading.</p>
</blockquote>
<h3>Node.js 24</h3>
<p>This release updates the runtime to Node.js 24. v6 had preliminary support for Node 24, however this action was by default still running on Node.js 20. Now this action by default will run on Node.js 24.</p>
<h2>What's Changed</h2>
<ul>
<li>Update GHES guidance to include reference to Node 20 version by <a href="https://github.com/patrikpolyak"><code>@​patrikpolyak</code></a> in <a href="">actions/download-artifact#440</a></li>
<li>Download Artifact Node24 support by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/download-artifact#415</a></li>
<li>fix: update <code>@​actions/artifact</code> to fix Node.js 24 punycode deprecation by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/download-artifact#451</a></li>
<li>prepare release v7.0.0 for Node.js 24 support by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/download-artifact#452</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/patrikpolyak"><code>@​patrikpolyak</code></a> made their first contribution in <a href="">actions/download-artifact#440</a></li>
<li><a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> made their first contribution in <a href="">actions/download-artifact#415</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/download-artifact/compare/v6.0.0...v7.0.0">https://github.com/actions/download-artifact/compare/v6.0.0...v7.0.0</a></p>
<h2>v6.0.0</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>9000827</code></a> Merge pull request <a href="">#493</a> from actions/tunc-d-prepare-download-v8-0-2</li>
<li><a href=""><code>e455989</code></a> Prepare download-artifact v8.0.2</li>
<li><a href=""><code>a00b90c</code></a> Merge pull request <a href="">#492</a> from actions/tunc-d-download-artifact-package-bump</li>
<li><a href=""><code>29bb7ce</code></a> Update <code>@​actions/artifact</code> to 6.3.1</li>
<li><a href=""><code>484a0b5</code></a> Update the readme (<a href="">#473</a>)</li>
<li><a href=""><code>3e5f45b</code></a> Add regression tests for CJK characters (<a href="">#471</a>)</li>
<li><a href=""><code>e6d03f6</code></a> Add a regression test for artifact name + content-type mismatches (<a href="">#472</a>)</li>
<li><a href=""><code>70fc10c</code></a> Merge pull request <a href="">#461</a> from actions/danwkennedy/digest-mismatch-behavior</li>
<li><a href=""><code>f258da9</code></a> Add change docs</li>
<li><a href=""><code>ccc058e</code></a> Fix linting issues</li>
<li>Additional commits viewable in <a href="https://github.com/actions/download-artifact/compare/v3...v8">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=actions/download-artifact&package-manager=github_actions&previous-version=3&new-version=8)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3ea839e879f2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.