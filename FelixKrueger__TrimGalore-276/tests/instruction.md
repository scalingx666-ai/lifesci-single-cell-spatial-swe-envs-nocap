# Issue

**Title:** build(deps): bump anyhow from 1.0.75 to 1.0.102

## Description

Bumps [anyhow](https://github.com/dtolnay/anyhow) from 1.0.75 to 1.0.102.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/dtolnay/anyhow/releases">anyhow's releases</a>.</em></p>
<blockquote>
<h2>1.0.102</h2>
<ul>
<li>Remove backtrace dependency (<a href="">#438</a>, <a href="">#439</a>, <a href="">#440</a>, <a href="">#441</a>, <a href="">#442</a>)</li>
</ul>
<h2>1.0.101</h2>
<ul>
<li>Add #[inline] to anyhow::Ok helper (<a href="">#437</a>, thanks <a href="https://github.com/Ibitier"><code>@​Ibitier</code></a>)</li>
</ul>
<h2>1.0.100</h2>
<ul>
<li>Teach clippy to lint formatting arguments in <code>bail!</code>, <code>ensure!</code>, <code>anyhow!</code> (<a href="">#426</a>)</li>
</ul>
<h2>1.0.99</h2>
<ul>
<li>Allow build-script cleanup failure with NFSv3 output directory to be non-fatal (<a href="">#420</a>)</li>
</ul>
<h2>1.0.98</h2>
<ul>
<li>Add <a href="https://docs.rs/anyhow/1/anyhow/struct.Error.html#method.into_boxed_dyn_error"><code>self.into_boxed_dyn_error()</code></a> and <a href="https://docs.rs/anyhow/1/anyhow/struct.Error.html#method.reallocate_into_boxed_dyn_error_without_backtrace"><code>self.reallocate_into_boxed_dyn_error_without_backtrace()</code></a> methods for anyhow::Error (<a href="">#415</a>)</li>
</ul>
<h2>1.0.97</h2>
<ul>
<li>Documentation improvements</li>
</ul>
<h2>1.0.96</h2>
<ul>
<li>Documentation improvements</li>
</ul>
<h2>1.0.95</h2>
<ul>
<li>Add <a href="https://docs.rs/anyhow/1/anyhow/struct.Error.html#method.from_boxed"><code>Error::from_boxed</code></a> (<a href="">#401</a>, <a href="">#402</a>)</li>
</ul>
<h2>1.0.94</h2>
<ul>
<li>Documentation improvements</li>
</ul>
<h2>1.0.93</h2>
<ul>
<li>Update dev-dependencies to <code>thiserror</code> v2</li>
</ul>
<h2>1.0.92</h2>
<ul>
<li>Support Rust 1.82's <code>&amp;raw const</code> and <code>&amp;raw mut</code> syntax inside <code>ensure!</code> (<a href="">#390</a>)</li>
</ul>
<h2>1.0.91</h2>
<ul>
<li>Ensure OUT_DIR is left with deterministic contents after build script execution (<a href="">#388</a>)</li>
</ul>
<h2>1.0.90</h2>
<ul>
<li>Documentation improvements</li>
</ul>
<h2>1.0.89</h2>
<ul>
<li>Make anyhow::Error's <code>UnwindSafe</code> and <code>RefUnwindSafe</code> impl consistently available between versions of Rust newer and older than 1.72 (<a href="">#386</a>)</li>
</ul>
<h2>1.0.88</h2>
<ul>
<li>Documentation improvements</li>
</ul>
<h2>1.0.87</h2>
<ul>
<li>Support more APIs, including <code>Error::new</code> and <code>Error::chain</code>, in no-std mode on Rust 1.81+ (<a href="">#383</a>)</li>
</ul>
<h2>1.0.86</h2>
<ul>
<li>Fix parse error in <code>ensure!</code> with non-literal after minus sign (<a href="">#373</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>5c657b3</code></a> Release 1.0.102</li>
<li><a href=""><code>e737fb6</code></a> Merge pull request <a href="">#442</a> from dtolnay/backtrace</li>
<li><a href=""><code>7fe62b5</code></a> Further simply backtrace conditional compilation</li>
<li><a href=""><code>c8cb5ca</code></a> Merge pull request <a href="">#441</a> from dtolnay/backtrace</li>
<li><a href=""><code>de27df7</code></a> Delete CI use of --features=backtrace</li>
<li><a href=""><code>9b67e5d</code></a> Merge pull request <a href="">#440</a> from dtolnay/backtrace</li>
<li><a href=""><code>efdb11a</code></a> Simplify <code>std_backtrace</code> conditional code</li>
<li><a href=""><code>b8a9a70</code></a> Merge pull request <a href="">#439</a> from dtolnay/backtrace</li>
<li><a href=""><code>a42fc2c</code></a> Remove <code>feature = &quot;backtrace&quot;</code> conditional code</li>
<li><a href=""><code>2a2a3ce</code></a> Re-word backtrace feature comment</li>
<li>Additional commits viewable in <a href="https://github.com/dtolnay/anyhow/compare/1.0.75...1.0.102">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=anyhow&package-manager=cargo&previous-version=1.0.75&new-version=1.0.102)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3f6be57a7da5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.