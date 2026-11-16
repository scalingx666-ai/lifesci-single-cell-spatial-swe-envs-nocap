# Issue

**Title:** [DEPENDABOT]: Bump rich from 10.4.0 to 10.5.0

## Description

Bumps [rich](https://github.com/willmcgugan/rich) from 10.4.0 to 10.5.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/willmcgugan/rich/releases">rich's releases</a>.</em></p>
<blockquote>
<h2>Mostly repr fixes</h2>
<p>Some fixes, and a few methods to support Textual</p>
<h2>[10.5.0] - 2021-05-07</h2>
<h3>Fixed</h3>
<ul>
<li>Fixed Pandas objects not pretty printing <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1305">willmcgugan/rich#1305</a></li>
<li>Fixed <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1256">willmcgugan/rich#1256</a></li>
<li>Fixed typing with rich.repr.auto decorator</li>
<li>Fixed repr error formatting <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1326">willmcgugan/rich#1326</a></li>
</ul>
<h3>Added</h3>
<ul>
<li>Added new_line_start argument to Console.print</li>
<li>Added Segment.divide method</li>
<li>Added Segment.split_cells method</li>
<li>Added segment.SegmentLines class</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/willmcgugan/rich/blob/master/CHANGELOG.md">rich's changelog</a>.</em></p>
<blockquote>
<h2>[10.5.0] - 2021-05-07</h2>
<h3>Fixed</h3>
<ul>
<li>Fixed Pandas objects not pretty printing <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1305">willmcgugan/rich#1305</a></li>
<li>Fixed <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1256">willmcgugan/rich#1256</a></li>
<li>Fixed typing with rich.repr.auto decorator</li>
<li>Fixed repr error formatting <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1326">willmcgugan/rich#1326</a></li>
</ul>
<h3>Added</h3>
<ul>
<li>Added new_line_start argument to Console.print</li>
<li>Added Segment.divide method</li>
<li>Added Segment.split_cells method</li>
<li>Added segment.SegmentLines class</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>c9afafd</code></a> version bump</li>
<li><a href=""><code>73d4356</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1315">#1315</a> from willmcgugan/auto-repr-fix</li>
<li><a href=""><code>8411f00</code></a> test fix</li>
<li><a href=""><code>8105943</code></a> no need for win test</li>
<li><a href=""><code>125ef57</code></a> provisional type fix</li>
<li><a href=""><code>59f699e</code></a> version bump</li>
<li><a href=""><code>3cf97f1</code></a> divide edge</li>
<li><a href=""><code>e9f96c8</code></a> last yield</li>
<li><a href=""><code>5a71691</code></a> edge case fix</li>
<li><a href=""><code>785fa72</code></a> experiment</li>
<li>Additional commits viewable in <a href="https://github.com/willmcgugan/rich/compare/v10.4.0...v10.5.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=rich&package-manager=pip&previous-version=10.4.0&new-version=10.5.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d52695fbb4f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.