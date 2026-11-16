# Issue

**Title:** build(deps): bump zip from 9.3.0 to 9.4.1 in the cargo-patch-minor group

## Description

Bumps the cargo-patch-minor group with 1 update: [zip](https://github.com/zip-rs/zip2).

Updates `zip` from 9.3.0 to 9.4.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/zip-rs/zip2/releases">zip's releases</a>.</em></p>
<blockquote>
<h2>v9.4.1</h2>
<h3><!-- raw HTML omitted -->🐛 Bug Fixes</h3>
<ul>
<li>Add a OwnedZipFileEntry for <a href="">#177</a> (<a href="">#1270</a>)</li>
</ul>
<h3><!-- raw HTML omitted -->🚜 Refactor</h3>
<ul>
<li>Use boxed slices instead of Vec when growability isn't needed (<a href="">#1271</a>)</li>
</ul>
<h2>v9.4.0</h2>
<h3><!-- raw HTML omitted -->🚀 Features</h3>
<ul>
<li>Implement ZipIterable::files_with_reader (<a href="">#1267</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/zip-rs/zip2/blob/master/CHANGELOG.md">zip's changelog</a>.</em></p>
<blockquote>
<h2><a href="https://github.com/zip-rs/zip2/compare/v9.4.0...v9.4.1">9.4.1</a> - 2026-11-06</h2>
<h3><!-- raw HTML omitted -->🐛 Bug Fixes</h3>
<ul>
<li>Add a OwnedZipFileEntry for <a href="">#177</a> (<a href="">#1270</a>)</li>
</ul>
<h3><!-- raw HTML omitted -->🚜 Refactor</h3>
<ul>
<li>Use boxed slices instead of Vec when growability isn't needed (<a href="">#1271</a>)</li>
</ul>
<h2><a href="https://github.com/zip-rs/zip2/compare/v9.3.0...v9.4.0">9.4.0</a> - 2026-11-05</h2>
<h3><!-- raw HTML omitted -->🚀 Features</h3>
<ul>
<li>Implement ZipIterable::files_with_reader (<a href="">#1267</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>96e8cce</code></a> chore: release v9.4.1 (<a href="">#1272</a>)</li>
<li><a href=""><code>f1b82f2</code></a> docs(example): Fix bug in memory-tracking example where reallocations were co...</li>
<li><a href=""><code>2308d6d</code></a> refactor: Use boxed slices instead of Vec when growability isn't needed (<a href="">#1271</a>)</li>
<li><a href=""><code>b3ad5df</code></a> fix: Add a OwnedZipFileEntry for <a href="">#177</a> (<a href="">#1270</a>)</li>
<li><a href=""><code>196b805</code></a> chore(deps): update lzma-rust2 from 0.24 to 0.25 (<a href="">#1268</a>)</li>
<li><a href=""><code>f347dd4</code></a> chore: release v9.4.0 (<a href="">#1269</a>)</li>
<li><a href=""><code>e9b7dcd</code></a> feat: Implement ZipIterable::files_with_reader (<a href="">#1267</a>)</li>
<li><a href=""><code>47765a9</code></a> docs(security): Clarify that some &quot;vulnerabilities&quot; are necessary for legitim...</li>
<li><a href=""><code>53cfe46</code></a> ci(deps): bump useblacksmith/checkout from 1.8.1 to 1.8.2 (<a href="">#1260</a>)</li>
<li><a href=""><code>b66f6b1</code></a> ci(deps): bump step-security/harden-runner from 2.22.2 to 2.22.3 (<a href="">#1262</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/zip-rs/zip2/compare/v9.3.0...v9.4.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=zip&package-manager=cargo&previous-version=9.3.0&new-version=9.4.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot ignore <dependency name> major version` will close this group update PR and stop Dependabot creating any more for the specific dependency's major version (unless you unignore this specific dependency's major version or upgrade to it yourself)
- `@dependabot ignore <dependency name> minor version` will close this group update PR and stop Dependabot creating any more for the specific dependency's minor version (unless you unignore this specific dependency's minor version or upgrade to it yourself)
- `@dependabot ignore <dependency name>` will close this group update PR and stop Dependabot creating any more for the specific dependency (unless you unignore this specific dependency or upgrade to it yourself)
- `@dependabot unignore <dependency name>` will remove all of the ignore conditions of the specified dependency
- `@dependabot unignore <dependency name> <ignore condition>` will remove the ignore condition of the specified dependency and ignore conditions

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1baee6b19a8d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.