# Issue

**Title:** [DEPENDABOT]: Bump rich from 10.1.0 to 10.2.1

## Description

Bumps [rich](https://github.com/willmcgugan/rich) from 10.1.0 to 10.2.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/willmcgugan/rich/releases">rich's releases</a>.</em></p>
<blockquote>
<h2>Fix markdown in layout</h2>
<h2>[10.2.1] - 2021-05-17</h2>
<h3>Fixed</h3>
<ul>
<li>Fixed panel in Markdown exploding <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1234">willmcgugan/rich#1234</a></li>
</ul>
<h2>Expanded pretty printing</h2>
<p>This version has some enhancements to pretty printing. Rich will now pretty print objects created with attrs (<a href="https://www.attrs.org/en/stable/">https://www.attrs.org/en/stable/</a>). Additionally, there is expanded support for UserList, UserDict, and mappingproxy -- less common containers in Python.</p>
<!-- raw HTML omitted -->
<h2>[10.2.0] - 2021-05-12</h2>
<h3>Added</h3>
<ul>
<li>Added syntax for call, i.e. &quot;Foo(bar)&quot;</li>
<li>Added Console.measure as a convenient alias for Measurement.get</li>
<li>Added support for pretty printing attrs objects</li>
<li>Added mappingproxy to pretty print</li>
<li>Added UserDict and UserList support to pretty printer</li>
</ul>
<h3>Changed</h3>
<ul>
<li>Changed colorama init to set strip=False</li>
<li>Changed highlighter for False, True, None to not match in the middle of a word. i.e. NoneType is no longer highlighted as None</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Fixed initial</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/willmcgugan/rich/blob/master/CHANGELOG.md">rich's changelog</a>.</em></p>
<blockquote>
<h2>[10.2.1] - 2021-05-17</h2>
<h3>Fixed</h3>
<ul>
<li>Fixed panel in Markdown exploding <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1234">willmcgugan/rich#1234</a></li>
</ul>
<h2>[10.2.0] - 2021-05-12</h2>
<h3>Added</h3>
<ul>
<li>Added syntax for call, i.e. &quot;Foo(bar)&quot;</li>
<li>Added Console.measure as a convenient alias for Measurement.get</li>
<li>Added support for pretty printing attrs objects</li>
<li>Added mappingproxy to pretty print</li>
<li>Added UserDict and UserList support to pretty printer</li>
</ul>
<h3>Changed</h3>
<ul>
<li>Changed colorama init to set strip=False</li>
<li>Changed highlighter for False, True, None to not match in the middle of a word. i.e. NoneType is no longer highlighted as None</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>Fixed initial blank lines removed from Syntax <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1214">willmcgugan/rich#1214</a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>690507d</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1239">#1239</a> from willmcgugan/fix-markdown-layout</li>
<li><a href=""><code>11242ad</code></a> fix for markdown in layout</li>
<li><a href=""><code>94661d3</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1233">#1233</a> from polyedre/fix-layout-doc-codebloc</li>
<li><a href=""><code>d1601f9</code></a> doc(layout): remove trailing spaces</li>
<li><a href=""><code>285937f</code></a> doc(layout): fix unrecognized codebloc</li>
<li><a href=""><code>7d02d29</code></a> attrs example, version bump</li>
<li><a href=""><code>22e95c9</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1203">#1203</a> from nathanrpage97/feat/mypy-strict-compliant</li>
<li><a href=""><code>b7bbbe5</code></a> Merge branch 'master' into feat/mypy-strict-compliant</li>
<li><a href=""><code>5c8a331</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1225">#1225</a> from willmcgugan/dependabot/pip/sphinx-4.0.1</li>
<li><a href=""><code>4357981</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/willmcgugan/rich/issues/1231">#1231</a> from willmcgugan/user-dict</li>
<li>Additional commits viewable in <a href="https://github.com/willmcgugan/rich/compare/v10.1.0...v10.2.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=rich&package-manager=pip&previous-version=10.1.0&new-version=10.2.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cd99cbe4b827`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.