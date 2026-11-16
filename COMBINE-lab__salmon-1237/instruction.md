# Issue

**Title:** chore(deps): bump the cargo-patch group across 1 directory with 7 updates

## Description

[//]: # (dependabot-start)
⚠️  **Dependabot is rebasing this PR** ⚠️

Rebasing might not happen immediately, so don't worry if this takes some time.

Note: if you make any changes to this PR yourself, they will take precedence over the rebase.

---

[//]: # (dependabot-end)

Bumps the cargo-patch group with 7 updates in the / directory:

| Package | From | To |
| --- | --- | --- |
| [thiserror](https://github.com/dtolnay/thiserror) | `2.0.20` | `2.0.21` |
| [serde_json](https://github.com/serde-rs/json) | `1.0.151` | `1.0.154` |
| [xxhash-rust](https://github.com/DoumanAsh/xxhash-rust) | `0.8.18` | `0.8.19` |
| [zstd](https://github.com/gyscos/zstd-rs) | `0.14.0` | `0.14.2` |
| [sha2](https://github.com/RustCrypto/hashes) | `0.11.0` | `0.11.1` |
| [libc](https://github.com/rust-lang/libc) | `0.2.189` | `0.2.190` |
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

Updates `zstd` from 0.14.0 to 0.14.2
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>1e52c7e</code></a> Release zstd 0.14.2</li>
<li><a href=""><code>42fc51f</code></a> Add reader-preserving fallible decoder constructors</li>
<li><a href=""><code>78170db</code></a> Add Decoder::into_inner for reader recovery without additional input</li>
<li><a href=""><code>9167d35</code></a> Release zstd 0.14.1, zstd-safe 8.1.0, and zstd-sys 2.1.1</li>
<li><a href=""><code>b59becf</code></a> Propagate C API deprecations through Rust bindings and wrappers</li>
<li><a href=""><code>d8a325a</code></a> Simplify Rust allocator constructors and test support</li>
<li><a href=""><code>594e743</code></a> Delegate panicking dictionary constructors to fallible variants</li>
<li><a href=""><code>779d39a</code></a> Add fallible constructors for prepared dictionaries</li>
<li><a href=""><code>fc5d2b7</code></a> Merge pull request <a href="">#379</a> from gyscos/fix/pr-378-rust-allocator</li>
<li><a href=""><code>18028cd</code></a> Count actual newline bytes in dictionary training samples</li>
<li>Additional commits viewable in <a href="https://github.com/gyscos/zstd-rs/compare/v0.14.0...v0.14.2">compare view</a></li>
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

Updates `libc` from 0.2.189 to 0.2.190
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/rust-lang/libc/releases">libc's releases</a>.</em></p>
<blockquote>
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
<p>Note that there may still be some changes to features gated by this config option, hence &quot;unstable&quot;
in its name. In the near future we will rename it to just <code>libc_time64</code>. Until then, please test it
out and report any bugs you find!</p>
<h3>Support</h3>
<ul>
<li>Add initial support for HelenOS (<a href="">#4355</a>)</li>
</ul>
<h3>Added</h3>
<p>We are slowly filling out the <code>Default</code> implementations, to reduce the need for <code>mem::zeroed()</code> in user code:</p>
<ul>
<li>Unix: Implement <code>Default</code> for a number of structs, especially on Apple platforms (<a href="">#5576</a>)</li>
<li>Linux, NetBSD: Give <code>statvfs</code> a <code>Default</code> impl (<a href="">#5583</a>)</li>
<li>Linux: Add <code>Default</code> to a <code>linux/can.rs</code> structs (<a href="">#5257</a>)</li>
</ul>
<p>Other additions:</p>
<ul>
<li>Expose the <code>libc_unstable_time64</code> cfg (<a href="">#5411</a>)</li>
<li>Android, Glibc: Add <code>pthread_gettid_np</code> (<a href="">#5359</a>)</li>
<li>Android: Add <code>RTLD_NEXT</code> (<a href="">#5323</a>)</li>
<li>Android: Add reuseport BPF socket options (<a href="">#5366</a>)</li>
<li>Apple: Add TCP header flags, options and SACK limits (<a href="">#5358</a>)</li>
<li>Apple: Add <code>NET_RT_DUMP2</code> (<a href="">#5442</a>)</li>
<li>Apple: Add <code>posix_spawn_file_actions_add(f)chdir(_np)</code> (<a href="">#5558</a>)</li>
<li>BSD: Add <code>BPF_WORDALIGN</code> (<a href="">#5320</a>)</li>
<li>BSD: Add <code>lchmod</code> and <code>lchflags</code> where supported (<a href="">#5400</a>)</li>
<li>BSD: Add <code>minherit</code> and related constants (<a href="">#4849</a>)</li>
<li>Docs: Add more links to public headers and manual pages (<a href="">#5407</a>), (<a href="">#5485</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rust-lang/libc/blob/0.2.190/CHANGELOG.md">libc's changelog</a>.</em></p>
<blockquote>
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
</code></pre>
<p>Note that there may still be some changes to features gated by this config option, hence &quot;unstable&quot;
in its name. In the near future we will rename it to just <code>libc_time64</code>. Until then, please test it
out and report any bugs you find!</p>
<h3>Support</h3>
<ul>
<li>Add initial support for HelenOS (<a href="">#4355</a>)</li>
</ul>
<h3>Added</h3>
<p>We are slowly filling out the <code>Default</code> implementations, to reduce the need for <code>mem::zeroed()</code> in user code:</p>
<ul>
<li>Unix: Implement <code>Default</code> for a number of structs, especially on Apple platforms (<a href="">#5576</a>)</li>
<li>Linux, NetBSD: Give <code>statvfs</code> a <code>Default</code> impl (<a href="">#5583</a>)</li>
<li>Linux: Add <code>Default</code> to a <code>linux/can.rs</code> structs (<a href="">#5257</a>)</li>
</ul>
<p>Other additions:</p>
<ul>
<li>Expose the <code>libc_unstable_time64</code> cfg (<a href="">#5411</a>)</li>
<li>Android, Glibc: Add <code>pthread_gettid_np</code> (<a href="">#5359</a>)</li>
<li>Android: Add <code>RTLD_NEXT</code> (<a href="">#5323</a>)</li>
<li>Android: Add reuseport BPF socket options (<a href="">#5366</a>)</li>
<li>Apple: Add TCP header flags, options and SACK limits (<a href="">#5358</a>)</li>
<li>Apple: Add <code>NET_RT_DUMP2</code> (<a href="">#5442</a>)</li>
<li>Apple: Add <code>posix_spawn_file_actions_add(f)chdir(_np)</code> (<a href="">#5558</a>)</li>
<li>BSD: Add <code>BPF_WORDALIGN</code> (<a href="">#5320</a>)</li>
<li>BSD: Add <code>lchmod</code> and <code>lchflags</code> where supported (<a href="">#5400</a>)</li>
<li>BSD: Add <code>minherit</code> and related constants (<a href="">#4849</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7b0ab55</code></a> ci: Rename <code>publish_0.2.yml</code> to <code>release.yaml</code></li>
<li><a href=""><code>ac85dde</code></a> ci: Sync release permissions with <code>main</code></li>
<li><a href=""><code>8f8cd20</code></a> libc: Release 0.2.190</li>
<li><a href=""><code>052c6e6</code></a> changelog: Fix an incorrect commit link</li>
<li><a href=""><code>ea19fd7</code></a> test: Remove explicit <code>libc</code> version</li>
<li><a href=""><code>6dbf3a2</code></a> dragonfly: Move <code>INHERIT_ZERO</code> to the freebsd module</li>
<li><a href=""><code>8a64766</code></a> apple: add <code>posix_spawn_file_actions_add(f)chdir(_np)</code></li>
<li><a href=""><code>28de514</code></a> linux, netbsd: Give statvfs a <code>Default</code> impl</li>
<li><a href=""><code>a58a95f</code></a> cygwin: Change <code>POSIX_SPAWN_*</code> flags to <code>c_short</code></li>
<li><a href=""><code>d175264</code></a> apple: <code>timeval32</code> is exhaustive</li>
<li>Additional commits viewable in <a href="https://github.com/rust-lang/libc/compare/0.2.189...0.2.190">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cf7c8ef0af3e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.