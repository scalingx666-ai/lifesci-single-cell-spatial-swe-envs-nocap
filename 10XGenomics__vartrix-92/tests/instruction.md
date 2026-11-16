# Issue

**Title:** Bump tempfile from 3.1.0 to 3.6.0

## Description

Bumps [tempfile](https://github.com/Stebalien/tempfile) from 3.1.0 to 3.6.0.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/Stebalien/tempfile/blob/master/CHANGELOG.md">tempfile's changelog</a>.</em></p>
<blockquote>
<h2>3.6.0</h2>
<ul>
<li>Update windows-sys to 0.48.</li>
<li>Update rustix min version to 0.37.11</li>
<li>Forward some <code>NamedTempFile</code> and <code>SpooledTempFile</code> methods to the underlying <code>File</code> object for
better performance (especially vectorized writes, etc.).</li>
<li>Implement <code>AsFd</code> and <code>AsHandle</code>.</li>
<li>Misc documentation fixes and code cleanups.</li>
</ul>
<h2>3.5.0</h2>
<ul>
<li>Update rustix from 0.36 to 0.37.1. This makes wasi work on rust stable</li>
<li>Update <code>windows-sys</code>, <code>redox_syscall</code></li>
<li>BREAKING: Remove the implementation of <code>Write for &amp;NamedTempFile&lt;F&gt; where &amp;F: Write</code>. Unfortunately, this can cause compile issues in unrelated code (<a href="">Stebalien/tempfile#224</a>).</li>
</ul>
<h2>3.4.0</h2>
<p>SECURITY: Prior <code>tempfile</code> releases depended on <code>remove_dir_all</code> version 0.5.0 which was vulnerable to a <a href="https://github.com/XAMPPRocky/remove_dir_all/security/advisories/GHSA-mc8h-8q98-g5hr">TOCTOU race</a>. This same race is present in rust versions prior to 1.58.1.</p>
<p>Features:</p>
<ul>
<li>Generalized temporary files: <code>NamedTempFile</code> can now abstract over different kinds of files (e.g.,
unix domain sockets, pipes, etc.):
<ul>
<li>Add <code>Builder::make</code> and <code>Builder::make_in</code> for generalized temp file
creation.</li>
<li>Add <code>NamedTempFile::from_parts</code> to complement <code>NamedTempFile::into_parts</code>.</li>
<li>Add generic parameter to <code>NamedTempFile</code> to support wrapping non-File types.</li>
</ul>
</li>
</ul>
<p>Bug Fixes/Improvements:</p>
<ul>
<li>Don't try to create a temporary file multiple times if the file path has been fully specified by
the user (no random characters).</li>
<li><code>NamedTempFile::persist_noclobber</code> is now always atomic on linux when <code>renameat_with</code> is
supported. Previously, it would first link the new path, then unlink the previous path.</li>
<li>Fix compiler warnings on windows.</li>
</ul>
<p>Trivia:</p>
<ul>
<li>Switch from <code>libc</code> to <code>rustix</code> on wasi/unix. This now makes direct syscalls instead of calling
through libc.</li>
<li>Remove <code>remove_dir_all</code> dependency. The rust standard library has optimized their internal version
significantly.</li>
<li>Switch to official windows-sys windows bindings.</li>
</ul>
<p>Breaking:</p>
<ul>
<li>The minimum rust version is now <code>1.48.0</code>.</li>
<li>Mark most functions as <code>must_use</code>.</li>
<li>Uses direct syscalls on linux by default, instead of libc.</li>
<li>The new type parameter in <code>NamedTempFile</code> may lead to type inference issues in some cases.</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>86b3136</code></a> chore: release 3.6.0</li>
<li><a href=""><code>a2b45b3</code></a> fix(docs): Change <code>dir</code> and <code>file</code> variable names to match existing comments ...</li>
<li><a href=""><code>f474e6a</code></a> Remove comment on SetFileInformationByHandle (<a href="">#236</a>)</li>
<li><a href=""><code>141c773</code></a> feat: implement default methods for SpooledTempFile Read/Write (<a href="">#232</a>)</li>
<li><a href=""><code>3590dbf</code></a> chore: modern rust (<a href="">#231</a>)</li>
<li><a href=""><code>c76b783</code></a> feat: implement AsFd/AsHandle to mirror the AsRaw* variants (<a href="">#230</a>)</li>
<li><a href=""><code>ae4f4c8</code></a> chore: bump rustix min version to 0.37.11 (<a href="">#229</a>)</li>
<li><a href=""><code>9488362</code></a> Forward default NamedTempFile methods (<a href="">#226</a>)</li>
<li><a href=""><code>c41ee48</code></a> build(deps): update windows-sys requirement from 0.45 to 0.48 (<a href="">#227</a>)</li>
<li><a href=""><code>c773849</code></a> chore: release 3.5.0</li>
<li>Additional commits viewable in <a href="https://github.com/Stebalien/tempfile/compare/v3.1.0...v3.6.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=tempfile&package-manager=cargo&previous-version=3.1.0&new-version=3.6.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

Dependabot will resolve any conflicts with this PR as long as you don't alter it yourself. You can also trigger a rebase manually by commenting `@dependabot rebase`.

[//]: # (dependabot-automerge-start)
Dependabot will merge this PR once it's up-to-date and CI passes on it, as requested by @bgianfo.

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `91091cc5b22f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.