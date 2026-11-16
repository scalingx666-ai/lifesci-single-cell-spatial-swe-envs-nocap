# Issue

**Title:** chore(deps): bump the cargo-patch group across 1 directory with 3 updates

## Description

Bumps the cargo-patch group with 3 updates in the / directory: [libc](https://github.com/rust-lang/libc), [realfft](https://github.com/HEnquist/realfft) and [ensure_simd](https://github.com/RagnarGrootKoerkamp/ensure_simd).

Updates `libc` from 0.2.190 to 0.2.191
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/rust-lang/libc/releases">libc's releases</a>.</em></p>
<blockquote>
<h2>0.2.191</h2>
<h3>Support</h3>
<ul>
<li>Emscripten: Support v4.0.12 to v6.0.11 (<a href="">#5610</a>)</li>
</ul>
<h3>Added</h3>
<ul>
<li>Apple: Add <code>F_SETNOSIGPIPE</code> and <code>F_GETNOSIGPIPE</code> (<a href="">#5609</a>)</li>
<li>Apple: add <code>ifaliasreq</code> and <code>in6_aliasreq</code> (<a href="">#5557</a>)</li>
<li>FreeBSD: Add <code>PT_*</code> constants (<a href="">#5625</a>)</li>
<li>Haiku: Add <code>AI_*</code> and <code>NI_*</code> constants from netdb.h (<a href="">#5585</a>)</li>
<li>Hurd: Add <code>POSIX_SPAWN_*</code> flags (<a href="">#5578</a>)</li>
<li>NuttX: Add <code>AT_SYMLINK_NOFOLLOW</code> (<a href="">#5614</a>)</li>
<li>OpenBSD: Add <code>sensordev</code> (<a href="">#5534</a>)</li>
<li>QuRT: Add <code>isatty</code> (<a href="">#5618</a>)</li>
<li>WASI: Add <code>pthread_condattr_{get,set}clock</code> (<a href="">#5626</a>)</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>FreeBSD-aarch64: Fix <code>gpregs</code> and <code>fpregs</code> (<a href="">#5603</a>)</li>
</ul>
<h3>Changed</h3>
<ul>
<li>AIX: Restore 'c_ulong' as the type of 'statvfs.f_fsid'. (<a href="">#5616</a>)</li>
<li>Android: Make <code>prop_info</code> an extern type (<a href="">#5561</a>)</li>
<li>Apple: Mach API is now available on non-MacOS targets again. This should resolve some issues building ecosystem crates. (<a href="https://redirect.github.com/rust-lang/libc/pulls/5612">#5612</a>), (<a href="">#5636</a>)</li>
<li>FreeBSD: Add back <code>NOTE_PCTRLMASK</code> with a deprecation warning (<a href="">#5600</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rust-lang/libc/blob/0.2.191/CHANGELOG.md">libc's changelog</a>.</em></p>
<blockquote>
<h2><a href="https://github.com/rust-lang/libc/compare/0.2.190...0.2.191">0.2.191</a> - 2026-10-16</h2>
<h3>Support</h3>
<ul>
<li>Emscripten: Support v4.0.12 to v6.0.11 (<a href="">#5610</a>)</li>
</ul>
<h3>Added</h3>
<ul>
<li>Apple: Add <code>F_SETNOSIGPIPE</code> and <code>F_GETNOSIGPIPE</code> (<a href="">#5609</a>)</li>
<li>Apple: add <code>ifaliasreq</code> and <code>in6_aliasreq</code> (<a href="">#5557</a>)</li>
<li>FreeBSD: Add <code>PT_*</code> constants (<a href="">#5625</a>)</li>
<li>Haiku: Add <code>AI_*</code> and <code>NI_*</code> constants from netdb.h (<a href="">#5585</a>)</li>
<li>Hurd: Add <code>POSIX_SPAWN_*</code> flags (<a href="">#5578</a>)</li>
<li>NuttX: Add <code>AT_SYMLINK_NOFOLLOW</code> (<a href="">#5614</a>)</li>
<li>OpenBSD: Add <code>sensordev</code> (<a href="">#5534</a>)</li>
<li>QuRT: Add <code>isatty</code> (<a href="">#5618</a>)</li>
<li>WASI: Add <code>pthread_condattr_{get,set}clock</code> (<a href="">#5626</a>)</li>
</ul>
<h3>Fixed</h3>
<ul>
<li>FreeBSD-aarch64: Fix <code>gpregs</code> and <code>fpregs</code> (<a href="">#5603</a>)</li>
</ul>
<h3>Changed</h3>
<ul>
<li>AIX: Restore 'c_ulong' as the type of 'statvfs.f_fsid'. (<a href="">#5616</a>)</li>
<li>Android: Make <code>prop_info</code> an extern type (<a href="">#5561</a>)</li>
<li>Apple: Mach API is now available on non-MacOS targets again. This should resolve some issues building ecosystem crates. (<a href="https://redirect.github.com/rust-lang/libc/pulls/5612">#5612</a>), (<a href="">#5636</a>)</li>
<li>FreeBSD: Add back <code>NOTE_PCTRLMASK</code> with a deprecation warning (<a href="">#5600</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ccc2ff4</code></a> libc: Release 0.2.191</li>
<li><a href=""><code>bce6efb</code></a> apple: Add <code>mach_task_self</code> and <code>mach_task_self_</code> to semver checks</li>
<li><a href=""><code>ecf4fd4</code></a> apple: Re-restrict <code>mach_vm_map</code> to MacOS-only</li>
<li><a href=""><code>b0e0423</code></a> Revert &quot;apple: Disable <code>mach.h</code> API on Apple mobile OSs&quot;</li>
<li><a href=""><code>9c7f568</code></a> apple: add <code>ifaliasreq</code> and <code>in6_aliasreq</code></li>
<li><a href=""><code>018c7e9</code></a> wasi: Add pthread_condattr_{get,set}clock</li>
<li><a href=""><code>2c77185</code></a> openbsd: add sensordev structure</li>
<li><a href=""><code>e10813c</code></a> hurd: Add missing <code>POSIX_SPAWN_*</code> flags</li>
<li><a href=""><code>2ea4bc1</code></a> Fix FreeBSD/aarch64</li>
<li><a href=""><code>6d666fd</code></a> dragonfly: Parse version from headers rather than CLI</li>
<li>Additional commits viewable in <a href="https://github.com/rust-lang/libc/compare/0.2.190...0.2.191">compare view</a></li>
</ul>
</details>
<br />

Updates `realfft` from 3.5.0 to 3.5.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/HEnquist/realfft/releases">realfft's releases</a>.</em></p>
<blockquote>
<h2>v3.5.1</h2>
<h2>What's Changed</h2>
<ul>
<li>Add missing license file, release 3.5.1 by <a href="https://github.com/HEnquist"><code>@​HEnquist</code></a> in <a href="">HEnquist/realfft#49</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/HEnquist/realfft/compare/v3.5.0...v3.5.1">https://github.com/HEnquist/realfft/compare/v3.5.0...v3.5.1</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>44f36c4</code></a> Merge pull request <a href="">#49</a> from HEnquist/license</li>
<li><a href=""><code>7602ffc</code></a> Declare minimum Rust version in Cargo.toml</li>
<li><a href=""><code>9fdcf59</code></a> Add MIT license file, bump version to 3.5.1</li>
<li>See full diff in <a href="https://github.com/HEnquist/realfft/compare/v3.5.0...v3.5.1">compare view</a></li>
</ul>
</details>
<br />

Updates `ensure_simd` from 0.1.0 to 0.1.1
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/RagnarGrootKoerkamp/ensure_simd/blob/master/CHANGELOG.md">ensure_simd's changelog</a>.</em></p>
<blockquote>
<h1>Changelog</h1>
<!-- raw HTML omitted -->
<h2>git</h2>
<ul>
<li>Also allow <code>simd128</code> on WASM.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>dc897bb</code></a> chore: Release ensure_simd version 0.1.1</li>
<li><a href=""><code>5251e98</code></a> Add <code>use ensure_simd as _;</code> hint to avoid unused-dependency warnings</li>
<li><a href=""><code>81485a6</code></a> Also allow simd128 on WASM</li>
<li><a href=""><code>141196c</code></a> Add link to blog for examples of workflows to distribute binaries</li>
<li>See full diff in <a href="https://github.com/RagnarGrootKoerkamp/ensure_simd/compare/v0.1.0...v0.1.1">compare view</a></li>
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
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore <dependency name> major version` will close this group update PR and stop Dependabot creating any more for the specific dependency's major version (unless you unignore this specific dependency's major version or upgrade to it yourself)
- `@dependabot ignore <dependency name> minor version` will close this group update PR and stop Dependabot creating any more for the specific dependency's minor version (unless you unignore this specific dependency's minor version or upgrade to it yourself)
- `@dependabot ignore <dependency name>` will close this group update PR and stop Dependabot creating any more for the specific dependency (unless you unignore this specific dependency or upgrade to it yourself)
- `@dependabot unignore <dependency name>` will remove all of the ignore conditions of the specified dependency
- `@dependabot unignore <dependency name> <ignore condition>` will remove the ignore condition of the specified dependency and ignore conditions

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0a55bc572ec0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.