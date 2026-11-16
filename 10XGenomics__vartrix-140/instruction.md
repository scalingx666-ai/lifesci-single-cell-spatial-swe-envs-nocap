# Issue

**Title:** Bump tempfile from 3.8.0 to 3.27.0

## Description

Bumps [tempfile](https://github.com/Stebalien/tempfile) from 3.8.0 to 3.27.0.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/Stebalien/tempfile/blob/master/CHANGELOG.md">tempfile's changelog</a>.</em></p>
<blockquote>
<h2>3.27.0</h2>
<p>This release adds <code>TempPath::try_from_path</code> and deprecates <code>TempPath::from_path</code>.</p>
<p>Prior to this release, <code>TempPath::from_path</code> made no attempts to convert relative paths into absolute paths. The following code would have deleted the wrong file:</p>
<pre lang="rust"><code>let tmp_path = TempPath::from_path(&quot;foo&quot;)
std::env::set_current_dir(&quot;/some/other/path&quot;).unwrap();
drop(tmp_path);
</code></pre>
<p>Now:</p>
<ol>
<li><code>TempPath::from_path</code> will attempt to convert relative paths into absolute paths. However, this isn't always possible as we need to call <code>std::env::current_dir</code>, which can fail. If we fail to convert the relative path to an absolute path, we simply keep the relative path.</li>
<li>The <code>TempPath::try_from_path</code> behaves exactly like <code>TempPath::from_path</code>, except that it returns an error if we fail to convert a relative path into an absolute path (or if the passed path is empty).</li>
</ol>
<p>Neither function attempt to verify the existence of the file in question.</p>
<p>Thanks to <a href="https://github.com/meng-xu-cs"><code>@​meng-xu-cs</code></a> for reporting this issue.</p>
<h2>3.26.0</h2>
<ul>
<li>Support <code>NamedTempFile::persist</code> on RedoxOS (<a href="">#393</a>) (thanks to <a href="https://github.com/Andy-Python-Programmer"><code>@​Andy-Python-Programmer</code></a>).</li>
</ul>
<h2>3.25.0</h2>
<ul>
<li>Allow <code>getrandom</code> 0.4.x while retaining support for <code>getrandom</code> 0.3.x.</li>
</ul>
<h2>3.24.0</h2>
<ul>
<li>Actually support WASIp2 without the nightly feature. This library is now feature complete on WASIp2 without any additional feature flags.</li>
<li>Exclude CI scripts from the published crate.</li>
</ul>
<h2>3.23.0</h2>
<ul>
<li>Remove need for the &quot;nightly&quot; feature to compile with &quot;wasip2&quot;.</li>
</ul>
<h2>3.22.0</h2>
<ul>
<li>Updated <code>windows-sys</code> requirement to allow version 0.61.x</li>
<li>Remove <code>unstable-windows-keep-open-tempfile</code> feature.</li>
</ul>
<h2>3.21.0</h2>
<ul>
<li>Updated <code>windows-sys</code> requirement to allow version 0.60.x</li>
</ul>
<h2>3.20.0</h2>
<p>This release mostly unifies the behavior/capabilities around &quot;keeping&quot; temporary files:</p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>5c8fa12</code></a> chore: release 3.27.0</li>
<li><a href=""><code>e34e574</code></a> test: disable uds conflict test on redox</li>
<li><a href=""><code>772c795</code></a> test: add CWD guards</li>
<li><a href=""><code>2632fb9</code></a> fix: resolve relative paths when constructing <code>TempPath</code></li>
<li><a href=""><code>929a112</code></a> chore: release 3.26.0</li>
<li><a href=""><code>29d6ac5</code></a> Add Redox OS CI (<a href="">#394</a>)</li>
<li><a href=""><code>375067f</code></a> doc(README): document supported platforms</li>
<li><a href=""><code>d353717</code></a> feat(redox): implement persist() (<a href="">#393</a>)</li>
<li><a href=""><code>64114d7</code></a> Fix typos in documentation (<a href="">#392</a>)</li>
<li><a href=""><code>9a38b8d</code></a> chore: release 3.25.0</li>
<li>Additional commits viewable in <a href="https://github.com/Stebalien/tempfile/compare/v3.8.0...v3.27.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=tempfile&package-manager=cargo&previous-version=3.8.0&new-version=3.27.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d959b7e659cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.