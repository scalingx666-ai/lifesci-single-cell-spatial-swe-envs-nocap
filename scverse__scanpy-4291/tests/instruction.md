# Issue

**Title:** ci: bump dorny/paths-filter from 4.0.2 to 4.0.3 in the actions-deps group

## Description

Bumps the actions-deps group with 1 update: [dorny/paths-filter](https://github.com/dorny/paths-filter).

Updates `dorny/paths-filter` from 4.0.2 to 4.0.3
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/dorny/paths-filter/releases">dorny/paths-filter's releases</a>.</em></p>
<blockquote>
<h2>v4.0.3</h2>
<h2>What's Changed</h2>
<ul>
<li>Update Outputs in readme to account for the 'every' predicate-quantifier by <a href="https://github.com/hintron"><code>@​hintron</code></a> in <a href="">dorny/paths-filter#247</a></li>
<li>fix: scope base-ignored warning to API path by <a href="https://github.com/saschabratton"><code>@​saschabratton</code></a> in <a href="">dorny/paths-filter#319</a></li>
<li>docs: add contents permission to PR example by <a href="https://github.com/134130"><code>@​134130</code></a> in <a href="">dorny/paths-filter#248</a></li>
<li>feat: add 'some-with-excludes' predicate quantifier by <a href="https://github.com/arxeiss"><code>@​arxeiss</code></a> in <a href="">dorny/paths-filter#322</a></li>
<li>Document safe handling of file list outputs in workflows by <a href="https://github.com/dorny"><code>@​dorny</code></a> in <a href="">dorny/paths-filter#326</a></li>
</ul>
<h2>Security</h2>
<ul>
<li>Escape multi-line filenames in list-files shell and csv output] by <a href="https://github.com/ken-matsui"><code>@​ken-matsui</code></a> and <a href="https://github.com/tjswlsgg"><code>@​tjswlsgg</code></a> in <a href="https://github.com/advisories/GHSA-7hc6-8hq5-9q2m">https://github.com/advisories/GHSA-7hc6-8hq5-9q2m</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/hintron"><code>@​hintron</code></a> made their first contribution in <a href="">dorny/paths-filter#247</a></li>
<li><a href="https://github.com/134130"><code>@​134130</code></a> made their first contribution in <a href="">dorny/paths-filter#248</a></li>
<li><a href="https://github.com/arxeiss"><code>@​arxeiss</code></a> made their first contribution in <a href="">dorny/paths-filter#322</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/dorny/paths-filter/compare/v4...v4.0.3">https://github.com/dorny/paths-filter/compare/v4...v4.0.3</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/dorny/paths-filter/blob/master/CHANGELOG.md">dorny/paths-filter's changelog</a>.</em></p>
<blockquote>
<h1>Changelog</h1>
<h2>v4.0.3</h2>
<ul>
<li><a href="">Document safe handling of file list outputs in workflows</a></li>
<li><a href="https://github.com/advisories/GHSA-7hc6-8hq5-9q2m">Escape multi-line filenames in list-files shell and csv output</a></li>
<li><a href="">Add 'some-with-excludes' predicate quantifier</a></li>
<li><a href="">Add contents permission to PR example</a></li>
<li><a href="">Scope base-ignored warning to API path</a></li>
<li><a href="">Update outputs in readme to account for the 'every' predicate-quantifier</a></li>
</ul>
<h2>v4.0.2</h2>
<ul>
<li><a href="">Work around git dubious ownership errors in container jobs</a></li>
<li><a href="">Use rev-parse instead of branch --show-current for older git compat</a></li>
<li><a href="">Fix warning message</a></li>
</ul>
<h2>v4.0.1</h2>
<ul>
<li><a href="">Support merge queue</a></li>
</ul>
<h2>v4.0.0</h2>
<ul>
<li><a href="">Update action runtime to node24</a></li>
</ul>
<h2>v3.0.4</h2>
<ul>
<li><a href="https://github.com/advisories/GHSA-7hc6-8hq5-9q2m">Escape multi-line filenames in list-files shell and csv output</a></li>
</ul>
<h2>v3.0.3</h2>
<ul>
<li><a href="">Add missing predicate-quantifier</a></li>
</ul>
<h2>v3.0.2</h2>
<ul>
<li><a href="">Add config parameter for predicate quantifier</a></li>
</ul>
<h2>v3.0.1</h2>
<ul>
<li><a href="">Compare base and ref when token is empty</a></li>
</ul>
<h2>v3.0.0</h2>
<ul>
<li><a href="">Update to Node.js 20</a></li>
<li><a href="">Update all dependencies</a></li>
</ul>
<h2>v2.11.1</h2>
<ul>
<li><a href="">Update @​actions/core to v1.10.0 - Fixes warning about deprecated set-output</a></li>
<li><a href="">Document need for pull-requests: read permission</a></li>
<li><a href="">Updating to actions/checkout@v3</a></li>
</ul>
<h2>v2.11.0</h2>
<ul>
<li><a href="">Set list-files input parameter as not required</a></li>
<li><a href="">Update Node.js</a></li>
<li><a href="">Fix incorrect handling of Unicode characters in exec()</a></li>
<li><a href="">Use Octokit pagination</a></li>
<li><a href="">Updates real world links</a></li>
</ul>
<h2>v2.10.2</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ceb8a2b</code></a> Update CHANGELOG.md for v4.0.3 and v3.0.4 (<a href="">#327</a>)</li>
<li><a href=""><code>ef09b88</code></a> Document safe handling of file list outputs in workflows (<a href="">#326</a>)</li>
<li><a href=""><code>44adc5b</code></a> Merge commit from fork</li>
<li><a href=""><code>4711b7a</code></a> feat: add 'some-with-excludes' predicate quantifier (<a href="">#322</a>)</li>
<li><a href=""><code>93c889f</code></a> fix: escape multi-line filenames in list-files shell and csv output</li>
<li><a href=""><code>b41dfa9</code></a> docs: add contents permission to PR example (<a href="">#248</a>)</li>
<li><a href=""><code>9af6e5a</code></a> fix: scope base-ignored warning to API path (<a href="">#319</a>)</li>
<li><a href=""><code>cae9006</code></a> docs: update outputs in readme to account for the 'every' predicate-quantifie...</li>
<li>See full diff in <a href="https://github.com/dorny/paths-filter/compare/7b450fff21473bca461d4b92ce414b9d0420d706...ceb8a2b8f2d89434be7ff52d3de7ec3738c5cc9d">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=dorny/paths-filter&package-manager=github_actions&previous-version=4.0.2&new-version=4.0.3)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fabadb9412c0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.