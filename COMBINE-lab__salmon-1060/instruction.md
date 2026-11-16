# Issue

**Title:** build(deps): bump svgo from 4.0.1 to 4.0.2 in /website

## Description

Bumps [svgo](https://github.com/svg/svgo) from 4.0.1 to 4.0.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/svg/svgo/releases">svgo's releases</a>.</em></p>
<blockquote>
<h2>v4.0.2</h2>
<h2>What's Changed</h2>
<h3>Security</h3>
<ul>
<li><a href="https://svgo.dev/docs/plugins/removeScripts/">removeScripts</a>, remove JavaScript URIs case-insensitively and make <code>&lt;script&gt;</code> handling namespace aware. By <a href="https://github.com/SethFalco"><code>@​SethFalco</code></a></li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li><a href="https://svgo.dev/docs/plugins/convertColors/">convertColors</a>, skip case-normalization for CSS custom properties. By <a href="https://github.com/SethFalco"><code>@​SethFalco</code></a> in <a href="">svg/svgo#2213</a></li>
<li><a href="https://svgo.dev/docs/plugins/convertPathData/">convertPathData</a>, improve handling of consecutive <code>t</code> commands. By <a href="https://github.com/KTibow"><code>@​KTibow</code></a> in <a href="">svg/svgo#2156</a></li>
<li><a href="https://svgo.dev/docs/plugins/convertPathData/">convertPathData</a>, safer handling of paths. By <a href="https://github.com/KTibow"><code>@​KTibow</code></a> in <a href="">svg/svgo#2158</a></li>
<li>Improve parsing of negative (or +) arc radii. By <a href="https://github.com/KTibow"><code>@​KTibow</code></a> in <a href="">svg/svgo#2205</a></li>
<li>When converting to a data URI, only encode it as a data URI once. By <a href="https://github.com/johnkenny54"><code>@​johnkenny54</code></a> in <a href="">svg/svgo#2053</a></li>
</ul>
<h3>Performance</h3>
<ul>
<li><a href="https://svgo.dev/docs/plugins/mergePaths/">mergePaths</a>, speed up child node removal. By <a href="https://github.com/mozzie"><code>@​mozzie</code></a> in <a href="">svg/svgo#2216</a></li>
</ul>
<h3>Other Changes</h3>
<ul>
<li><a href="https://svgo.dev/docs/plugins/removeAttributesBySelector/">removeAttributesBySelector</a>, log warning and noop if missing parameters. By <a href="https://github.com/KTibow"><code>@​KTibow</code></a> in <a href="">svg/svgo#2215</a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>b2309cf</code></a> chore: sync version with api</li>
<li><a href=""><code>f529cfc</code></a> Merge commit from fork</li>
<li><a href=""><code>581fe68</code></a> performance: speed up mergePath child node removal (<a href="">#2216</a>)</li>
<li><a href=""><code>eb4c8b6</code></a> docs(removeAttributesBySelector): properly document and check types (<a href="">#2215</a>)</li>
<li><a href=""><code>6fd5872</code></a> fix(convertColors): skip convertCase on css custom properties (<a href="">#2213</a>)</li>
<li><a href=""><code>7414f73</code></a> fix: properly parse negative (or +) arc radii (<a href="">#2205</a>)</li>
<li><a href=""><code>a8c19aa</code></a> fix: only call encodeSVGDatauri once and add test case (<a href="">#2053</a>)</li>
<li><a href=""><code>65548f4</code></a> fix(convertPathData): properly handle consecutive t commands (<a href="">#2156</a>)</li>
<li><a href=""><code>a41a7c1</code></a> fix(convertPathData): introducing isSafeToRemove (<a href="">#2164</a>)</li>
<li><a href=""><code>38625dd</code></a> test: handle charm icons (<a href="">#2203</a>)</li>
<li>See full diff in <a href="https://github.com/svg/svgo/compare/v4.0.1...v4.0.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=svgo&package-manager=npm_and_yarn&previous-version=4.0.1&new-version=4.0.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/COMBINE-lab/salmon/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b09e8e10af65`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.