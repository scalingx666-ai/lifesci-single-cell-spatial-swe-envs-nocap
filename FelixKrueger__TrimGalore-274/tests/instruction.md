# Issue

**Title:** build(deps): bump flate2 from 1.1.5 to 1.1.9

## Description

Bumps [flate2](https://github.com/rust-lang/flate2-rs) from 1.1.5 to 1.1.9.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/rust-lang/flate2-rs/releases">flate2's releases</a>.</em></p>
<blockquote>
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
<h2>What's Changed</h2>
<ul>
<li>chore: make some documents clearer by <a href="https://github.com/reddaisyy"><code>@​reddaisyy</code></a> in <a href="">rust-lang/flate2-rs#510</a></li>
<li>Explain rationale for choosing bufread,read,write modules by <a href="https://github.com/jongiddy"><code>@​jongiddy</code></a> in <a href="">rust-lang/flate2-rs#512</a></li>
<li>use Decompress::reset() instead of recreating in DeflateDecoder by <a href="https://github.com/amirshukayev"><code>@​amirshukayev</code></a> in <a href="">rust-lang/flate2-rs#514</a></li>
<li>use <code>zlib_rs</code> api by <a href="https://github.com/folkertdev"><code>@​folkertdev</code></a> in <a href="">rust-lang/flate2-rs#513</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/reddaisyy"><code>@​reddaisyy</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#510</a></li>
<li><a href="https://github.com/amirshukayev"><code>@​amirshukayev</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#514</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/rust-lang/flate2-rs/compare/1.1.5...1.1.6">https://github.com/rust-lang/flate2-rs/compare/1.1.5...1.1.6</a></p>
<h2>1.1.6 - YANKED</h2>
<p>It caused <a href="">rust-lang/flate2-rs#515</a>.</p>
<h2>What's Changed</h2>
<ul>
<li>chore: make some documents clearer by <a href="https://github.com/reddaisyy"><code>@​reddaisyy</code></a> in <a href="">rust-lang/flate2-rs#510</a></li>
<li>Explain rationale for choosing bufread,read,write modules by <a href="https://github.com/jongiddy"><code>@​jongiddy</code></a> in <a href="">rust-lang/flate2-rs#512</a></li>
<li>use Decompress::reset() instead of recreating in DeflateDecoder by <a href="https://github.com/amirshukayev"><code>@​amirshukayev</code></a> in <a href="">rust-lang/flate2-rs#514</a></li>
<li>use <code>zlib_rs</code> api by <a href="https://github.com/folkertdev"><code>@​folkertdev</code></a> in <a href="">rust-lang/flate2-rs#513</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/reddaisyy"><code>@​reddaisyy</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#510</a></li>
<li><a href="https://github.com/amirshukayev"><code>@​amirshukayev</code></a> made their first contribution in <a href="">rust-lang/flate2-rs#514</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/rust-lang/flate2-rs/compare/1.1.5...1.1.6">https://github.com/rust-lang/flate2-rs/compare/1.1.5...1.1.6</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>19ddb18</code></a> Merge pull request <a href="">#529</a> from folkertdev/update-zlib-rs-0.6.0</li>
<li><a href=""><code>c956e12</code></a> upgrade zlib-rs to version <code>0.6.0</code></li>
<li><a href=""><code>21d5eeb</code></a> Merge pull request <a href="">#528</a> from wgyt/wgyt/patch</li>
<li><a href=""><code>54f8484</code></a> update LICENSE-MIT</li>
<li><a href=""><code>f4924fe</code></a> Merge pull request <a href="">#527</a> from jongiddy/crc-tests</li>
<li><a href=""><code>8b9b7a6</code></a> Add tests to check data CRC</li>
<li><a href=""><code>fd17c74</code></a> Merge pull request <a href="">#526</a> from folkertdev/zlib-rs-crc32</li>
<li><a href=""><code>aef26ac</code></a> check that zlib-rs no longer compiles crc32fast</li>
<li><a href=""><code>5ec7647</code></a> make <code>crc32fast</code> an optional dependency</li>
<li><a href=""><code>c584e97</code></a> use <code>zlib-rs</code> for crc32 (when available)</li>
<li>Additional commits viewable in <a href="https://github.com/rust-lang/flate2-rs/compare/1.1.5...1.1.9">compare view</a></li>
</ul>
</details>
<br />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1f46af74dd11`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.