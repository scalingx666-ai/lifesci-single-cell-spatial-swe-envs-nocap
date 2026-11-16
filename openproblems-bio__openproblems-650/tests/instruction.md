# Issue

**Title:** Update snakemake requirement from <7.15,>=7.8 to >=7.8,<7.17

## Description

Updates the requirements on [snakemake](https://github.com/snakemake/snakemake) to permit the latest version.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/snakemake/snakemake/releases">snakemake's releases</a>.</em></p>
<blockquote>
<h2>v7.16.1</h2>
<h2><a href="https://github.com/snakemake/snakemake/compare/v7.16.0...v7.16.1">7.16.1</a> (2022-10-18)</h2>
<h3>Bug Fixes</h3>
<ul>
<li>conda create --no-shortcuts absent on Linux/MacOS (regression from <a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1046">#1046</a>) (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1916">#1916</a>) (<a href="">8a86a1e</a>)</li>
<li>fix typo in line display of exceptions (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1912">#1912</a>) (<a href="">55e38a6</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/snakemake/snakemake/blob/main/CHANGELOG.md">snakemake's changelog</a>.</em></p>
<blockquote>
<h2><a href="https://github.com/snakemake/snakemake/compare/v7.16.0...v7.16.1">7.16.1</a> (2022-10-18)</h2>
<h3>Bug Fixes</h3>
<ul>
<li>conda create --no-shortcuts absent on Linux/MacOS (regression from <a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1046">#1046</a>) (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1916">#1916</a>) (<a href="">8a86a1e</a>)</li>
<li>fix typo in line display of exceptions (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1912">#1912</a>) (<a href="">55e38a6</a>)</li>
</ul>
<h2><a href="https://github.com/snakemake/snakemake/compare/v7.15.2...v7.16.0">7.16.0</a> (2022-10-14)</h2>
<h3>Features</h3>
<ul>
<li>k8s: add --k8s-cpu-scalar (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1857">#1857</a>) (<a href="">a067a1b</a>)</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li>allow report generation to handle pathlib objects (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1904">#1904</a>) (<a href="">7c34656</a>)</li>
<li>fix false reruns after checkpoints (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1907">#1907</a>) (<a href="">dc5af12</a>)</li>
</ul>
<h2><a href="https://github.com/snakemake/snakemake/compare/v7.15.1...v7.15.2">7.15.2</a> (2022-10-08)</h2>
<h3>Bug Fixes</h3>
<ul>
<li>Comparison of rules and non-rule instances (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1894">#1894</a>) (<a href="">bf01ece</a>)</li>
<li>delay evaluation of tmpdir to actual job execution, and not submission. This way, tmpdir can be dependent on the node context. (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1860">#1860</a>) (<a href="">4203556</a>)</li>
<li>ensure that rule name string instead of object is passed to tabulate package (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1898">#1898</a>) (<a href="">f9ff157</a>)</li>
<li>issue 1846 (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1888">#1888</a>) (<a href="">da2dfbd</a>)</li>
<li>lexicographically sorted rule display with --list, and trimmed rule docstrings (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1880">#1880</a>) (<a href="">32128ae</a>)</li>
</ul>
<h3>Performance Improvements</h3>
<ul>
<li>Average NamedList <strong>getitem</strong> performance improvement (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1825">#1825</a>) (<a href="">10451b7</a>)</li>
</ul>
<h2><a href="https://github.com/snakemake/snakemake/compare/v7.15.0...v7.15.1">7.15.1</a> (2022-10-04)</h2>
<h3>Bug Fixes</h3>
<ul>
<li>fix <code>--immediate-submit</code> (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1851">#1851</a>) (<a href="">e358372</a>)</li>
<li>Handle temp files for all jobs in a group. (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1779">#1779</a>) (<a href="">d28b893</a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li>small tweaks to flux documentation (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1886">#1886</a>) (<a href="">f29b371</a>)</li>
<li>various little fixes (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1875">#1875</a>) (<a href="">b93f8e3</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>9c0f1d5</code></a> chore(main): release 7.16.1 (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1919">#1919</a>)</li>
<li><a href=""><code>8a86a1e</code></a> fix: conda create --no-shortcuts absent on Linux/MacOS (regression from <a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1046">#1046</a>...</li>
<li><a href=""><code>aa70e2b</code></a> chore(deps): Bump marocchino/sticky-pull-request-comment from 2.2.0 to 2.2.1 ...</li>
<li><a href=""><code>55e38a6</code></a> fix: fix typo in line display of exceptions (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1912">#1912</a>)</li>
<li><a href=""><code>a4dd327</code></a> chore(main): release 7.16.0 (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1900">#1900</a>)</li>
<li><a href=""><code>7c34656</code></a> fix: allow report generation to handle pathlib objects (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1904">#1904</a>)</li>
<li><a href=""><code>dc5af12</code></a> fix: fix false reruns after checkpoints (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1907">#1907</a>)</li>
<li><a href=""><code>a067a1b</code></a> feat: k8s: add --k8s-cpu-scalar (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1857">#1857</a>)</li>
<li><a href=""><code>2a37803</code></a> chore(main): release 7.15.2 (<a href="https://github-redirect.dependabot.com/snakemake/snakemake/issues/1897">#1897</a>)</li>
<li><a href=""><code>4203556</code></a> fix: delay evaluation of tmpdir to actual job execution, and not submission. ...</li>
<li>Additional commits viewable in <a href="https://github.com/snakemake/snakemake/compare/v7.8.0...v7.16.1">compare view</a></li>
</ul>
</details>
<br />

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5e353bd45d13`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.