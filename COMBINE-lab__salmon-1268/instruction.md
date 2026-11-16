# Issue

**Title:** chore(deps): bump the cargo-patch group with 8 updates

## Description

Bumps the cargo-patch group with 8 updates:

| Package | From | To |
| --- | --- | --- |
| [thiserror](https://github.com/dtolnay/thiserror) | `2.0.20` | `2.0.21` |
| [serde_json](https://github.com/serde-rs/json) | `1.0.151` | `1.0.154` |
| [xxhash-rust](https://github.com/DoumanAsh/xxhash-rust) | `0.8.18` | `0.8.19` |
| [sha2](https://github.com/RustCrypto/hashes) | `0.11.0` | `0.11.1` |
| [libc](https://github.com/rust-lang/libc) | `0.2.189` | `0.2.191` |
| [realfft](https://github.com/HEnquist/realfft) | `3.5.0` | `3.5.1` |
| [ensure_simd](https://github.com/RagnarGrootKoerkamp/ensure_simd) | `0.1.0` | `0.1.1` |
| [jiff](https://github.com/BurntSushi/jiff) | `0.2.37` | `0.2.38` |

Updates `thiserror` from 2.0.20 to 2.0.21
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/dtolnay/thiserror/releases">thiserror's releases</a>.</em></p>
<blockquote>
<h2>2.0.21</h2>
<ul>
<li>Fix parsing of generic unit variants in display expressions (<a href="">#459</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>b1827ee</code></a> Release 2.0.21</li>
<li><a href=""><code>58037b5</code></a> Merge pull request <a href="">#459</a> from dtolnay/turbofish</li>
<li><a href=""><code>f82a0cf</code></a> Keep track of nested turbofish depth</li>
<li><a href=""><code>72ea492</code></a> Raise required compiler to Rust 1.77</li>
<li><a href=""><code>72eea0d</code></a> Resolve io_other_error clippy lint in tests</li>
<li><a href=""><code>07f09a2</code></a> Raise required compiler to Rust 1.74</li>
<li><a href=""><code>2715388</code></a> Update ui test suite to nightly-2026-09-22</li>
<li><a href=""><code>5a306c7</code></a> Update ui test suite to nightly-2026-09-05</li>
<li><a href=""><code>ef9383b</code></a> Update ui test suite to nightly-2026-08-22</li>
<li><a href=""><code>8336b84</code></a> Update ui tests for version 2.0.20</li>
<li>See full diff in <a href="https://github.com/dtolnay/thiserror/compare/2.0.20...2.0.21">compare view</a></li>
</ul>
</details>
<br />

Updates `serde_json` from 1.0.151 to 1.0.154
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/serde-rs/json/releases">serde_json's releases</a>.</em></p>
<blockquote>
<h2>v1.0.154</h2>
<ul>
<li>Support preserve_order in no_std builds (<a href="">#1333</a>, thanks <a href="https://github.com/razmser"><code>@​razmser</code></a>)</li>
</ul>
<h2>v1.0.153</h2>
<ul>
<li>Report invalid UTF-8 at the first bad byte (<a href="">#1345</a>, thanks <a href="https://github.com/00200200"><code>@​00200200</code></a>)</li>
</ul>
<h2>v1.0.152</h2>
<ul>
<li>Preserve sign of <code>-0</code> in arbitrary_precision mode (<a href="">#1346</a>, thanks <a href="https://github.com/yuxi-liu-wired"><code>@​yuxi-liu-wired</code></a>)</li>
<li>Fix comparison of large non-integer values with f32::INFINITY (<a href="">#1347</a>, thanks <a href="https://github.com/yuxi-liu-wired"><code>@​yuxi-liu-wired</code></a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>20572a6</code></a> Release 1.0.154</li>
<li><a href=""><code>a91bfaf</code></a> Fix RandomState links in map documentation</li>
<li><a href=""><code>3c932c0</code></a> Merge pull request <a href="">#1333</a> from razmser/no-std-preserve-order</li>
<li><a href=""><code>4b2d726</code></a> Release 1.0.153</li>
<li><a href=""><code>83335ee</code></a> Touch up PR 1345</li>
<li><a href=""><code>4b4810a</code></a> Resolve range_plus_one pedantic clippy lint</li>
<li><a href=""><code>8af71cc</code></a> Merge pull request <a href="">#1345</a> from 00200200/fix-invalid-utf8-error-column</li>
<li><a href=""><code>452afa2</code></a> Correct multiline raw UTF-8 error positions and simplify indexing</li>
<li><a href=""><code>c9f1e3b</code></a> Release 1.0.152</li>
<li><a href=""><code>854fc70</code></a> Touch up PR 1347</li>
<li>Additional commits viewable in <a href="https://github.com/serde-rs/json/compare/v1.0.151...v1.0.154">compare view</a></li>
</ul>
</details>
<br />

Updates `xxhash-rust` from 0.8.18 to 0.8.19
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/DoumanAsh/xxhash-rust/commits">compare view</a></li>
</ul>
</details>
<br />

Updates `sha2` from 0.11.0 to 0.11.1
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>138dc5a</code></a> Release sha2 v0.11.1 (<a href="">#927</a>)</li>
<li><a href=""><code>cf01056</code></a> sha2: fix <code>unsafe_op_in_unsafe_fn</code> lint, bump MSRV to 1.88 (<a href="">#926</a>)</li>
<li><a href=""><code>7c59cad</code></a> Update Cargo.lock (<a href="">#921</a>)</li>
<li><a href=""><code>f57b947</code></a> streebog: tweak internal implementation (<a href="">#925</a>)</li>
<li><a href=""><code>336611f</code></a> Fix <code>cargo::manual_readme</code> lint (<a href="">#924</a>)</li>
<li><a href=""><code>1df8877</code></a> md2: fix <code>clippy::needless_range_loop</code> lint (<a href="">#923</a>)</li>
<li><a href=""><code>6075989</code></a> sha2: fix loading of round constants on AArch64 backends (<a href="">#922</a>)</li>
<li><a href=""><code>eadfd90</code></a> Update Cargo.lock (<a href="">#913</a>)</li>
<li><a href=""><code>fa30840</code></a> blake2 v0.11.0 (<a href="">#911</a>)</li>
<li><a href=""><code>f6c786d</code></a> ci: bump the all-deps group across 1 directory with 3 updates (<a href="">#896</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/RustCrypto/hashes/compare/sha2-v0.11.0...sha2-v0.11.1">compare view</a></li>
</ul>
</details>
<br />

Updates `libc` from 0.2.189 to 0.2.191
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
<h2>0.2.190</h2>
<p>There is now a single config for enabling 64-bit <code>time_t</code>: <code>libc_unstable_time64</code>. This can be set
unconditionally; it opts in to 64-bit <code>time_t</code> on the following platforms that use 32-bit by
default:</p>
<ul>
<li>32-bit Linux-GNU</li>
<li>32-bit Linux-uClibc</li>
<li>32-bit Linux-musl. Note that setting this flag also enables some other changes that happend in
musl v1.2.</li>
<li>32-bit Windows-GNU</li>
<li>ESP-IDF (all targets with this environment are 32-bit)</li>
</ul>
<p>Most other 32-bit platforms are either already using 64-bit <code>time_t</code>, or are considered legacy
and will not be gaining support from their upstream maintainers.</p>
<p>You can enable this using <code>RUSTFLAGS</code>:</p>
<pre lang="sh"><code>RUSTFLAGS='--cfg=libc_unstable_time64' cargo ...
</code></pre>
<p>Note that there may still be some changes to features gated by this config option, hence &quot;unstable&quot;</p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
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
<h2><a href="https://github.com/rust-lang/libc/compare/0.2.189...0.2.190">0.2.190</a> - 2026-10-02</h2>
<p>There is now a single config for enabling 64-bit <code>time_t</code>: <code>libc_unstable_time64</code>. This can be set
unconditionally; it opts in to 64-bit <code>time_t</code> on the following platforms that use 32-bit by
default:</p>
<ul>
<li>32-bit Linux-GNU</li>
<li>32-bit Linux-uClibc</li>
<li>32-bit Linux-musl. Note that setting this flag also enables some other changes that happend in
musl v1.2.</li>
<li>32-bit Windows-GNU</li>
<li>ESP-IDF (all targets with this environment are 32-bit)</li>
</ul>
<p>Most other 32-bit platforms are either already using 64-bit <code>time_t</code>, or are considered legacy
and will not be gaining support from their upstream maintainers.</p>
<p>You can enable this using <code>RUSTFLAGS</code>:</p>
<pre lang="sh"><code>RUSTFLAGS='--cfg=libc_unstable_time64' cargo ...
&lt;/tr&gt;&lt;/table&gt;
</code></pre>
</blockquote>
<p>... (truncated)</p>
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
<li>Additional commits viewable in <a href="https://github.com/rust-lang/libc/compare/0.2.189...0.2.191">compare view</a></li>
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

Updates `jiff` from 0.2.37 to 0.2.38
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/BurntSushi/jiff/blob/master/CHANGELOG.md">jiff's changelog</a>.</em></p>
<blockquote>
<h1>0.2.38 (2026-10-06)</h1>
<p>This release updates Jiff's bundled copy of the [IANA Time Zone Database]
to <code>2026e</code>. See the <a href="https://lists.iana.org/hyperkitty/list/tz-announce@iana.org/thread/VXIA4AU73OQL3OZ3ZBZHWIASIIVBGUJV/"><code>2026e</code> release announcement</a> for more details.</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4ce3e20</code></a> 0.2.38</li>
<li><a href=""><code>bca7bb9</code></a> jiff-tzdb-0.1.9</li>
<li><a href=""><code>374afc2</code></a> jiff-tzdb: update to tzdb 2026e</li>
<li><a href=""><code>5416198</code></a> doc: include readme in published crate</li>
<li>See full diff in <a href="https://github.com/BurntSushi/jiff/compare/jiff-static-0.2.37...jiff-static-0.2.38">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f70de74d5092`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.