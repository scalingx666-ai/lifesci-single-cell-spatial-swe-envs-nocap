# Issue

**Title:** Bump flate2 from 1.0.11 to 1.1.10

## Description

Bumps [flate2](https://github.com/rust-lang/flate2-rs) from 1.0.11 to 1.1.10.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/rust-lang/flate2-rs/releases">flate2's releases</a>.</em></p>
<blockquote>
<h2>1.1.10</h2>
<h2>What's Changed</h2>
<ul>
<li>feat: reuse zlib's decoder buffer by <a href="https://github.com/Vaiz"><code>@​Vaiz</code></a> in <a href="">rust-lang/flate2-rs#532</a></li>
<li>feat: add reset method for read::GzDecoder and buffered::GzDecoder by <a href="https://github.com/Vaiz"><code>@​Vaiz</code></a> in <a href="">rust-lang/flate2-rs#534</a></li>
<li>Drop cloudflare-zlib by <a href="https://github.com/kornelski"><code>@​kornelski</code></a> in <a href="">rust-lang/flate2-rs#539</a></li>
<li>Add a wrapper for the <code>Crc</code> struct by <a href="https://github.com/MikkelPaulson"><code>@​MikkelPaulson</code></a> in <a href="">rust-lang/flate2-rs#540</a></li>
<li>Bump miniz_oxide to 0.9 by <a href="https://github.com/oscargus"><code>@​oscargus</code></a> in <a href="">rust-lang/flate2-rs#543</a></li>
<li>Upgrade miniz_oxide and add unit tests of the different flush kinds by <a href="https://github.com/fintelia"><code>@​fintelia</code></a> in <a href="">rust-lang/flate2-rs#498</a></li>
<li>Fix infinite loop in writing gzip header/footer by <a href="https://github.com/Shnatsel"><code>@​Shnatsel</code></a> in <a href="">rust-lang/flate2-rs#547</a></li>
<li>test: generate corrupt gzip fixture at runtime by <a href="https://github.com/nanookclaw"><code>@​nanookclaw</code></a> in <a href="">rust-lang/flate2-rs#550</a></li>
<li>Reject oversized gzip extra fields by <a href="https://github.com/Byron"><code>@​Byron</code></a> in <a href="">rust-lang/flate2-rs#553</a></li>
<li>Reject incomplete deflate streams at EOF by <a href="https://github.com/Guflly"><code>@​Guflly</code></a> in <a href="">rust-lang/flate2-rs#556</a></li>
<li>Include <code>README.md</code> in a private module by <a href="https://github.com/bushrat011899"><code>@​bushrat011899</code></a> in <a href="">rust-lang/flate2-rs#562</a></li>
<li>Add <code>no_std</code> support using nightly <code>alloc_io</code> by <a href="https://github.com/bushrat011899"><code>@​bushrat011899</code></a> in <a href="">rust-lang/flate2-rs#559</a></li>
<li>Update <code>get_mut()</code> documentation to make clear how 'inner` can be used by <a href="https://github.com/Byron"><code>@​Byron</code></a> in <a href="">rust-lang/flate2-rs#558</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/Vaiz"><code>@​Vaiz</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#532</a></li>
<li><a href="https://github.com/MikkelPaulson"><code>@​MikkelPaulson</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#540</a></li>
<li><a href="https://github.com/oscargus"><code>@​oscargus</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#543</a></li>
<li><a href="https://github.com/nanookclaw"><code>@​nanookclaw</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#550</a></li>
<li><a href="https://github.com/Guflly"><code>@​Guflly</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#556</a></li>
<li><a href="https://github.com/bushrat011899"><code>@​bushrat011899</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#562</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/rust-lang/flate2-rs/compare/1.1.9...1.1.10">https://github.com/rust-lang/flate2-rs/compare/1.1.9...1.1.10</a></p>
<h2>1.1.9 - upgrade zlib-rs to version <code>0.6.0</code></h2>
<h2>What's Changed</h2>
<ul>
<li>use <code>zlib-rs</code> for crc32 (when available) by <a href="https://github.com/folkertdev"><code>@​folkertdev</code></a> in <a href="">rust-lang/flate2-rs#526</a></li>
<li>Add tests to check data CRC by <a href="https://github.com/jongiddy"><code>@​jongiddy</code></a> in <a href="">rust-lang/flate2-rs#527</a></li>
<li>update LICENSE-MIT by <a href="https://github.com/wgyt"><code>@​wgyt</code></a> in <a href="">rust-lang/flate2-rs#528</a></li>
<li>upgrade zlib-rs to version <code>0.6.0</code> by <a href="https://github.com/folkertdev"><code>@​folkertdev</code></a> in <a href="">rust-lang/flate2-rs#529</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/wgyt"><code>@​wgyt</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#528</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/rust-lang/flate2-rs/compare/1.1.8...1.1.9">https://github.com/rust-lang/flate2-rs/compare/1.1.8...1.1.9</a></p>
<h2>1.1.8</h2>
<h2>What's Changed</h2>
<ul>
<li>Document feature flags using document-features crate by <a href="https://github.com/Copilot"><code>@​Copilot</code></a> in <a href="">rust-lang/flate2-rs#519</a></li>
<li>Complete the zlib-rs support without the need for C-bindings by <a href="https://github.com/Byron"><code>@​Byron</code></a> in <a href="">rust-lang/flate2-rs#524</a></li>
<li>test zlib API for all compatible backends by <a href="https://github.com/Byron"><code>@​Byron</code></a> in <a href="">rust-lang/flate2-rs#525</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/Copilot"><code>@​Copilot</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#519</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/rust-lang/flate2-rs/compare/1.1.7...1.1.8">https://github.com/rust-lang/flate2-rs/compare/1.1.7...1.1.8</a></p>
<h2>1.1.7 - depend on <code>zlib-rs</code> directly and remove <code>libz-rs-sys</code></h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ed93d4f</code></a> Merge pull request <a href="">#558</a> from rust-lang/lib-doc-update</li>
<li><a href=""><code>fb5228d</code></a> Merge pull request <a href="">#559</a> from bushrat011899/no_std</li>
<li><a href=""><code>6ed3ba3</code></a> Add executable <code>no_std</code> example</li>
<li><a href=""><code>faed8a0</code></a> Expand CI to test <code>no_std</code> compatibility and correctness</li>
<li><a href=""><code>2ba8e7e</code></a> Add unstable <code>no_std</code> support behind <code>flate2_unstable_nightly_alloc_io</code></li>
<li><a href=""><code>3fe1126</code></a> Centralize usage of <code>std</code> for <code>error</code> and <code>io</code></li>
<li><a href=""><code>98e313a</code></a> Add <code>GzHeader::mtime_as_duration</code></li>
<li><a href=""><code>0642965</code></a> Switch to <code>core</code> implicit prelude and only use <code>std</code> where required</li>
<li><a href=""><code>454a63c</code></a> Remove left-over <code>dbg!</code> statement</li>
<li><a href=""><code>2a490b7</code></a> Add <code>runtime_detection</code> feature</li>
<li>Additional commits viewable in <a href="https://github.com/rust-lang/flate2-rs/compare/1.0.11...1.1.10">compare view</a></li>
</ul>
</details>
<br />

> **Note**
> Automatic rebases have been disabled on this pull request as it has been open for over 30 days.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c79e4564a9b9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.