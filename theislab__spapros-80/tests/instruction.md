# Issue

**Title:** [DEPENDABOT]: Bump black from 20.8b1 to 21.5b0

## Description

Bumps [black](https://github.com/psf/black) from 20.8b1 to 21.5b0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/psf/black/releases">black's releases</a>.</em></p>
<blockquote>
<h2>21.5b0</h2>
<h4><em>Black</em></h4>
<ul>
<li>Set <code>--pyi</code> mode if <code>--stdin-filename</code> ends in <code>.pyi</code> (<a href="https://github-redirect.dependabot.com/psf/black/issues/2169">#2169</a>)</li>
<li>Stop detecting target version as Python 3.9+ with pre-PEP-614 decorators that are
being called but with no arguments (<a href="https://github-redirect.dependabot.com/psf/black/issues/2182">#2182</a>)</li>
</ul>
<h4><em>Black-Primer</em></h4>
<ul>
<li>Add <code>--no-diff</code> to black-primer to suppress formatting changes (<a href="https://github-redirect.dependabot.com/psf/black/issues/2187">#2187</a>)</li>
</ul>
<h2>21.4b2</h2>
<h4><em>Black</em></h4>
<ul>
<li>
<p>Fix crash if the user configuration directory is inaccessible. (<a href="https://github-redirect.dependabot.com/psf/black/issues/2158">#2158</a>)</p>
</li>
<li>
<p>Clarify
<a href="https://github.com/psf/black/blob/master/docs/the_black_code_style.md#pragmatism">circumstances</a>
in which <em>Black</em> may change the AST (<a href="https://github-redirect.dependabot.com/psf/black/issues/2159">#2159</a>)</p>
</li>
</ul>
<h4><em>Packaging</em></h4>
<ul>
<li>Install <code>primer.json</code> (used by <code>black-primer</code> by default) with black. (<a href="https://github-redirect.dependabot.com/psf/black/issues/2154">#2154</a>)</li>
</ul>
<h2>21.4b1</h2>
<h4><em>Black</em></h4>
<ul>
<li>
<p>Fix crash on docstrings ending with &quot;\ &quot;. (<a href="https://github-redirect.dependabot.com/psf/black/issues/2142">#2142</a>)</p>
</li>
<li>
<p>Fix crash when atypical whitespace is cleaned out of dostrings (<a href="https://github-redirect.dependabot.com/psf/black/issues/2120">#2120</a>)</p>
</li>
<li>
<p>Reflect the <code>--skip-magic-trailing-comma</code> and <code>--experimental-string-processing</code> flags
in the name of the cache file. Without this fix, changes in these flags would not take
effect if the cache had already been populated. (<a href="https://github-redirect.dependabot.com/psf/black/issues/2131">#2131</a>)</p>
</li>
<li>
<p>Don't remove necessary parentheses from assignment expression containing assert /
return statements. (<a href="https://github-redirect.dependabot.com/psf/black/issues/2143">#2143</a>)</p>
</li>
</ul>
<h4><em>Packaging</em></h4>
<ul>
<li>Bump pathspec to &gt;= 0.8.1 to solve invalid .gitignore exclusion handling</li>
</ul>
<h2>21.4b0</h2>
<h4><em>Black</em></h4>
<ul>
<li>Fixed a rare but annoying formatting instability created by the combination of
optional trailing commas inserted by <code>Black</code> and optional parentheses looking at
pre-existing &quot;magic&quot; trailing commas. This fixes issue <a href="https://github-redirect.dependabot.com/psf/black/issues/1629">#1629</a> and all of its many many
duplicates. (<a href="https://github-redirect.dependabot.com/psf/black/issues/2126">#2126</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/psf/black/blob/master/CHANGES.md">black's changelog</a>.</em></p>
<blockquote>
<h3>21.5b0</h3>
<h4><em>Black</em></h4>
<ul>
<li>Set <code>--pyi</code> mode if <code>--stdin-filename</code> ends in <code>.pyi</code> (<a href="https://github-redirect.dependabot.com/psf/black/issues/2169">#2169</a>)</li>
<li>Stop detecting target version as Python 3.9+ with pre-PEP-614 decorators that are
being called but with no arguments (<a href="https://github-redirect.dependabot.com/psf/black/issues/2182">#2182</a>)</li>
</ul>
<h4><em>Black-Primer</em></h4>
<ul>
<li>Add <code>--no-diff</code> to black-primer to suppress formatting changes (<a href="https://github-redirect.dependabot.com/psf/black/issues/2187">#2187</a>)</li>
</ul>
<h3>21.4b2</h3>
<h4><em>Black</em></h4>
<ul>
<li>
<p>Fix crash if the user configuration directory is inaccessible. (<a href="https://github-redirect.dependabot.com/psf/black/issues/2158">#2158</a>)</p>
</li>
<li>
<p>Clarify
<a href="https://github.com/psf/black/blob/master/docs/the_black_code_style.md#pragmatism">circumstances</a>
in which <em>Black</em> may change the AST (<a href="https://github-redirect.dependabot.com/psf/black/issues/2159">#2159</a>)</p>
</li>
</ul>
<h4><em>Packaging</em></h4>
<ul>
<li>Install <code>primer.json</code> (used by <code>black-primer</code> by default) with black. (<a href="https://github-redirect.dependabot.com/psf/black/issues/2154">#2154</a>)</li>
</ul>
<h3>21.4b1</h3>
<h4><em>Black</em></h4>
<ul>
<li>
<p>Fix crash on docstrings ending with &quot;\ &quot;. (<a href="https://github-redirect.dependabot.com/psf/black/issues/2142">#2142</a>)</p>
</li>
<li>
<p>Fix crash when atypical whitespace is cleaned out of dostrings (<a href="https://github-redirect.dependabot.com/psf/black/issues/2120">#2120</a>)</p>
</li>
<li>
<p>Reflect the <code>--skip-magic-trailing-comma</code> and <code>--experimental-string-processing</code> flags
in the name of the cache file. Without this fix, changes in these flags would not take
effect if the cache had already been populated. (<a href="https://github-redirect.dependabot.com/psf/black/issues/2131">#2131</a>)</p>
</li>
<li>
<p>Don't remove necessary parentheses from assignment expression containing assert /
return statements. (<a href="https://github-redirect.dependabot.com/psf/black/issues/2143">#2143</a>)</p>
</li>
</ul>
<h4><em>Packaging</em></h4>
<ul>
<li>Bump pathspec to &gt;= 0.8.1 to solve invalid .gitignore exclusion handling</li>
</ul>
<h3>21.4b0</h3>
<h4><em>Black</em></h4>
<ul>
<li>Fixed a rare but annoying formatting instability created by the combination of</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/psf/black/commits">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=black&package-manager=pip&previous-version=20.8b1&new-version=21.5b0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8af8b6058e6c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.