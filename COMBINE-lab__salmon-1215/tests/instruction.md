# Issue

**Title:** chore(deps): bump devalue from 5.8.2 to 5.9.2 in /website

## Description

Bumps [devalue](https://github.com/sveltejs/devalue) from 5.8.2 to 5.9.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/sveltejs/devalue/releases">devalue's releases</a>.</em></p>
<blockquote>
<h2>v5.9.2</h2>
<h3>Patch Changes</h3>
<ul>
<li>8b2a456: fix: reject out-of-bounds indices</li>
</ul>
<h2>v5.9.1</h2>
<h3>Patch Changes</h3>
<ul>
<li>39457ce: fix: <code>uneval</code> emits valid JS for graphs with more than 65534 repeated references</li>
<li>686e379: fix: emit valid JS for Node <code>Buffer</code> in <code>uneval</code></li>
<li>376b65c: fix: preserve <code>-0</code> in float typed arrays in <code>uneval</code></li>
</ul>
<h2>v5.9.0</h2>
<h3>Minor Changes</h3>
<ul>
<li>07d6a38: feat: export <code>filterArrayIndices</code>, the array-index filtering used by the <code>indicesOf</code> stringify operation, so custom operations can reuse it instead of reimplementing it</li>
<li>07d6a38: feat: add pluggable <code>operations</code> option to <code>parse</code>/<code>unflatten</code>, allowing customization of how values are constructed while reviving (e.g. cross-realm or foreign-runtime revival)</li>
<li>5b53532: feat: add pluggable <code>operations</code> option to <code>stringify</code>/<code>stringifyAsync</code>, allowing customization of how values are introspected during serialization (e.g. side-effect-free or foreign-runtime serialization)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/sveltejs/devalue/blob/main/CHANGELOG.md">devalue's changelog</a>.</em></p>
<blockquote>
<h2>5.9.2</h2>
<h3>Patch Changes</h3>
<ul>
<li>8b2a456: fix: reject out-of-bounds indices</li>
</ul>
<h2>5.9.1</h2>
<h3>Patch Changes</h3>
<ul>
<li>39457ce: fix: <code>uneval</code> emits valid JS for graphs with more than 65534 repeated references</li>
<li>686e379: fix: emit valid JS for Node <code>Buffer</code> in <code>uneval</code></li>
<li>376b65c: fix: preserve <code>-0</code> in float typed arrays in <code>uneval</code></li>
</ul>
<h2>5.9.0</h2>
<h3>Minor Changes</h3>
<ul>
<li>07d6a38: feat: export <code>filterArrayIndices</code>, the array-index filtering used by the <code>indicesOf</code> stringify operation, so custom operations can reuse it instead of reimplementing it</li>
<li>07d6a38: feat: add pluggable <code>operations</code> option to <code>parse</code>/<code>unflatten</code>, allowing customization of how values are constructed while reviving (e.g. cross-realm or foreign-runtime revival)</li>
<li>5b53532: feat: add pluggable <code>operations</code> option to <code>stringify</code>/<code>stringifyAsync</code>, allowing customization of how values are introspected during serialization (e.g. side-effect-free or foreign-runtime serialization)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a3d30d9</code></a> Version Packages (<a href="">#180</a>)</li>
<li><a href=""><code>8b2a456</code></a> Merge commit from fork</li>
<li><a href=""><code>3e01a6c</code></a> Version Packages (<a href="">#179</a>)</li>
<li><a href=""><code>686e379</code></a> fix: emit valid JS for Node <code>Buffer</code> in <code>uneval</code> (<a href="">#175</a>)</li>
<li><a href=""><code>39457ce</code></a> fix: uneval emits valid JS for graphs with more than 65534 repeated reference...</li>
<li><a href=""><code>376b65c</code></a> fix: preserve -0 in float typed arrays in uneval (<a href="">#178</a>)</li>
<li><a href=""><code>e82bc08</code></a> Version Packages (<a href="">#174</a>)</li>
<li><a href=""><code>07d6a38</code></a> feat: pluggable operations for parse (<a href="">#173</a>)</li>
<li><a href=""><code>5b53532</code></a> feat: pluggable operations for stringify (<a href="">#172</a>)</li>
<li>See full diff in <a href="https://github.com/sveltejs/devalue/compare/v5.8.2...v5.9.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=devalue&package-manager=npm_and_yarn&previous-version=5.8.2&new-version=5.9.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3be8b31d312`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.