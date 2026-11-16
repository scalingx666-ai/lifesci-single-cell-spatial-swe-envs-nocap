# Issue

**Title:** Bump rust-htslib from 0.36.0 to 0.47.1

## Description

Bumps [rust-htslib](https://github.com/rust-bio/rust-htslib) from 0.36.0 to 0.47.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/rust-bio/rust-htslib/releases">rust-htslib's releases</a>.</em></p>
<blockquote>
<h2>rust-htslib: v0.41.0</h2>
<h2><a href="https://github.com/rust-bio/rust-htslib/compare/rust-htslib-v0.40.2...rust-htslib-v0.41.0">0.41.0</a> (2023-03-02)</h2>
<h3>Features</h3>
<ul>
<li>Revised calculation of leading- and trailing-softclips (<a href="">#375</a>) (<a href="">b61dd2c</a>)</li>
</ul>
<h2>rust-htslib: v0.40.2</h2>
<h2><a href="https://github.com/rust-bio/rust-htslib/compare/rust-htslib-v0.40.1...rust-htslib-v0.40.2">0.40.2</a> (2022-10-13)</h2>
<h3>Performance Improvements</h3>
<ul>
<li>update htslib and corresponding bindings to 1.16 (<a href="">#366</a>) (<a href="">f597ce0</a>)</li>
</ul>
<h2>rust-htslib: v0.40.1</h2>
<h2><a href="https://github.com/rust-bio/rust-htslib/compare/rust-htslib-v0.40.0...rust-htslib-v0.40.1">0.40.1</a> (2022-08-24)</h2>
<h3>Bug Fixes</h3>
<ul>
<li>Header::to_hashmap skips <code>@CO</code> tags, add <code>comments()</code>  method (<a href="">#363</a>) (<a href="">c24a7f6</a>)</li>
</ul>
<h2>rust-htslib: v0.40.0</h2>
<h2><a href="https://github.com/rust-bio/rust-htslib/compare/rust-htslib-v0.39.5...rust-htslib-v0.40.0">0.40.0</a> (2022-07-05)</h2>
<h3>Features</h3>
<ul>
<li>Add wrapper of BGZF writer (<a href="">#349</a>) (<a href="">965ed88</a>)</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li>update to latest release-please (<a href="">b130634</a>)</li>
</ul>
<h2>rust-htslib rust-htslib-v0.39.5</h2>
<h3>Bug Fixes</h3>
<ul>
<li>set path in release-please config (<a href="">d8f7c6e</a>)</li>
</ul>
<h2>rust-htslib rust-htslib-v0.39.4</h2>
<h3>Bug Fixes</h3>
<ul>
<li>perform checkout before running release please (<a href="">cbc6a0a</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rust-bio/rust-htslib/blob/master/CHANGELOG.md">rust-htslib's changelog</a>.</em></p>
<blockquote>
<h2><a href="https://github.com/rust-bio/rust-htslib/compare/v0.47.0...v0.47.1">0.47.1</a> (2024-11-12)</h2>
<h3>Bug Fixes</h3>
<ul>
<li>allow leading deletions in read_pos method of CigarStringView. (<a href="">#447</a>) (<a href="">2986713</a>)</li>
</ul>
<h2><a href="https://github.com/rust-bio/rust-htslib/compare/v0.46.0...v0.47.0">0.47.0</a> (2024-05-22)</h2>
<h3>Features</h3>
<ul>
<li>Add fasta::build function + FaidxBuildError (<a href="">#418</a>) (<a href="">7c575ef</a>)</li>
<li>Add rust_htslib::bcf::index::build (<a href="">#408</a>) (<a href="">79d70cd</a>)</li>
<li>derive PartialEq and Eq for bam:: and bcf::Format (<a href="">#428</a>) (<a href="">528e543</a>)</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li>bam::Record:new should return a valid record (<a href="">#361</a>) (<a href="">87f2011</a>)</li>
<li>build for macOS (<a href="">#431</a>) (<a href="">d869fdd</a>)</li>
<li>in bam record buffer, change the start of the window to the first added item in last iteration (<a href="">#430</a>) (<a href="">56ee2bd</a>)</li>
<li>Panic on trailing omitted FORMAT records (<a href="">#417</a>) (<a href="">9f575ee</a>)</li>
</ul>
<h2><a href="https://github.com/rust-bio/rust-htslib/compare/v0.45.0...v0.46.0">0.46.0</a> (2024-02-22)</h2>
<h3>Features</h3>
<ul>
<li>making several RecordBuffer methods public (<a href="">6757f52</a>)</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li>fix building libz-sys (<a href="">#420</a>) (<a href="">01c8849</a>)</li>
</ul>
<h2><a href="https://github.com/rust-bio/rust-htslib/compare/v0.44.1...v0.45.0">0.45.0</a> (2024-02-07)</h2>
<h3>Features</h3>
<ul>
<li>adding function to get sequence length to faidx mod (<a href="">#410</a>) (<a href="">ae79eba</a>)</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li>Loosen acceptable types to support current linux build on aarch64 (<a href="">#415</a>) (<a href="">1d78d12</a>)</li>
</ul>
<h2><a href="https://github.com/rust-bio/rust-htslib/compare/v0.44.0...v0.44.1">0.44.1</a> (2023-06-21)</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>fc8ab72</code></a> chore(master): release 0.47.1 (<a href="">#451</a>)</li>
<li><a href=""><code>2986713</code></a> fix: allow leading deletions in read_pos method of CigarStringView. (<a href="">#447</a>)</li>
<li><a href=""><code>01fb5b8</code></a> ci: Add Dependabot (<a href="">#435</a>)</li>
<li><a href=""><code>4b3cbcb</code></a> chore(master): release 0.47.0 (<a href="">#426</a>)</li>
<li><a href=""><code>87f2011</code></a> fix: bam::Record:new should return a valid record (<a href="">#361</a>)</li>
<li><a href=""><code>56ee2bd</code></a> fix: in bam record buffer, change the start of the window to the first added ...</li>
<li><a href=""><code>d869fdd</code></a> fix: build for macOS (<a href="">#431</a>)</li>
<li><a href=""><code>f73ebc3</code></a> Revert &quot;fix type&quot;</li>
<li><a href=""><code>18c9bcc</code></a> fix type</li>
<li><a href=""><code>528e543</code></a> feat: derive PartialEq and Eq for bam:: and bcf::Format (<a href="">#428</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/rust-bio/rust-htslib/compare/v0.36.0...v0.47.1">compare view</a></li>
</ul>
</details>
<br />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3ea839e879f2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.