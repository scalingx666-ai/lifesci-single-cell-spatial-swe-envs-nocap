# Issue

**Title:** Bump tempfile from 3.6.0 to 3.8.0

## Description

Bumps [tempfile](https://github.com/Stebalien/tempfile) from 3.6.0 to 3.8.0.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/Stebalien/tempfile/blob/master/CHANGELOG.md">tempfile's changelog</a>.</em></p>
<blockquote>
<h2>3.8.0</h2>
<ul>
<li>Added <code>with_prefix</code> and <code>with_prefix_in</code> to <code>TempDir</code> and <code>NamedTempFile</code> to make it easier to create temporary files/directories with nice prefixes.</li>
<li>Misc cleanups.</li>
</ul>
<h2>3.7.1</h2>
<ul>
<li>Tempfile builds on haiku again.</li>
<li>Under the hood, we've switched from the unlinkat/linkat syscalls to the regular unlink/link syscalls where possible.</li>
</ul>
<h2>3.7.0</h2>
<p>BREAKING: This release updates the MSRV to 1.63. This isn't an API-breaking change (so no major
release) but it's still a breaking change for some users.</p>
<ul>
<li>Update fastrand from 1.6 to 2.0</li>
<li>Update rustix to 0.38</li>
<li>Updates the MSRV to 1.63.</li>
<li>Provide AsFd/AsRawFd on wasi.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ded4c25</code></a> chore: release 3.8.0</li>
<li><a href=""><code>32ef2ac</code></a> chore: more test cleanups (<a href="">#253</a>)</li>
<li><a href=""><code>b4a2f64</code></a> feat: add convenience methods for creating temp files with prefixes (<a href="">#250</a>)</li>
<li><a href=""><code>f994e9f</code></a> chore: cleanup tempdir tests (<a href="">#252</a>)</li>
<li><a href=""><code>8b3703c</code></a> chore: clippy fixes (<a href="">#251</a>)</li>
<li><a href=""><code>bf8f7ea</code></a> chore: release 3.7.1</li>
<li><a href=""><code>a5c236c</code></a> Use <code>rename</code>/<code>unlink</code>/<code>etc. instead of </code>renameat<code>/</code>unlinkat`/etc. (<a href="">#247</a>)</li>
<li><a href=""><code>d258544</code></a> chore: release 3.7.0</li>
<li><a href=""><code>da36cd5</code></a> Provide implementations for I/O safety traits unconditionally (<a href="">#244</a>)</li>
<li><a href=""><code>74f9fbc</code></a> Update to rustix 0.38 and update MSRV to 1.63 (<a href="">#241</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/Stebalien/tempfile/compare/v3.6.0...v3.8.0">compare view</a></li>
</ul>
</details>
<br />

> **Note**
> Automatic rebases have been disabled on this pull request as it has been open for over 30 days.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2e1112b38649`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.