# Issue

**Title:** Bump rust-htslib from 0.47.1 to 1.0.1

## Description

Bumps [rust-htslib](https://github.com/rust-bio/rust-htslib) from 0.47.1 to 1.0.1.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/rust-bio/rust-htslib/blob/master/CHANGELOG.md">rust-htslib's changelog</a>.</em></p>
<blockquote>
<h2><a href="https://github.com/rust-bio/rust-htslib/compare/v1.0.0...v1.0.1">1.0.1</a> (2026-06-29)</h2>
<h3>Bug Fixes</h3>
<ul>
<li>map unmapped reads (tid=-1) to correct index in slow_idxstats (<a href="">#511</a>) (<a href="">ebd7d99</a>)</li>
</ul>
<h2><a href="https://github.com/rust-bio/rust-htslib/compare/v0.51.0...v1.0.0">1.0.0</a> (2026-01-29)</h2>
<h3>⚠ BREAKING CHANGES</h3>
<ul>
<li>make the inner header pointer accessible again, although only through unsafe (<a href="">#504</a>)</li>
<li>Reason about Send/Sync-ness of types and change Rcs to Arcs (<a href="">#488</a>)</li>
<li>Use Arc instead of Rc in bam::buffer, such that the buffer can be used in a multithreaded context (<a href="">#495</a>)</li>
</ul>
<h3>Features</h3>
<ul>
<li>Reason about Send/Sync-ness of types and change Rcs to Arcs (<a href="">#488</a>) (<a href="">d743a34</a>)</li>
<li>Use Arc instead of Rc in bam::buffer, such that the buffer can be used in a multithreaded context (<a href="">#495</a>) (<a href="">229d5a2</a>)</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li>apply clippy suggestion to use unwrap_or instead of match (<a href="">#501</a>) (<a href="">161f759</a>)</li>
<li>empty_header was making a deep copy of header (<a href="">#499</a>) (<a href="">60aad09</a>), closes <a href="">#493</a></li>
<li>make the inner header pointer accessible again, although only through unsafe (<a href="">#504</a>) (<a href="">4dc0fba</a>)</li>
</ul>
<h3>Performance Improvements</h3>
<ul>
<li><strong>bam:</strong> Remove unnecessary heap allocation in <code>Record::aux</code> (<a href="">#498</a>) (<a href="">9680bb4</a>)</li>
</ul>
<h2><a href="https://github.com/rust-bio/rust-htslib/compare/v0.50.0...v0.51.0">0.51.0</a> (2025-10-15)</h2>
<h3>Features</h3>
<ul>
<li>Add support for updating existing aux tags inplace. (<a href="">#481</a>) (<a href="">f4a1106</a>)</li>
</ul>
<h2><a href="https://github.com/rust-bio/rust-htslib/compare/v0.49.0...v0.50.0">0.50.0</a> (2025-07-09)</h2>
<h3>Features</h3>
<ul>
<li>Add bam::Record::set_cigar (<a href="">#477</a>) (<a href="">f1bb470</a>)</li>
<li>Allow for non-diploid genotypes (<a href="">#476</a>) (<a href="">1c22ac5</a>)</li>
</ul>
<h3>Bug Fixes</h3>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>b576820</code></a> chore(master): release 1.0.1 (<a href="">#513</a>)</li>
<li><a href=""><code>ebd7d99</code></a> fix: map unmapped reads (tid=-1) to correct index in slow_idxstats (<a href="">#511</a>)</li>
<li><a href=""><code>0168666</code></a> chore(master): release 1.0.0 (<a href="">#496</a>)</li>
<li><a href=""><code>663b1af</code></a> enh: bcf: adds translate to Record so we don't need a writer (<a href="">#503</a>)</li>
<li><a href=""><code>4dc0fba</code></a> fix!: make the inner header pointer accessible again, although only through u...</li>
<li><a href=""><code>d743a34</code></a> feat!: Reason about Send/Sync-ness of types and change Rcs to Arcs (<a href="">#488</a>)</li>
<li><a href=""><code>93995ab</code></a> Add a method to push an aux tag without first checking for existence. (<a href="">#497</a>)</li>
<li><a href=""><code>161f759</code></a> fix: apply clippy suggestion to use unwrap_or instead of match (<a href="">#501</a>)</li>
<li><a href=""><code>9680bb4</code></a> perf(bam): Remove unnecessary heap allocation in <code>Record::aux</code> (<a href="">#498</a>)</li>
<li><a href=""><code>60aad09</code></a> fix: empty_header was making a deep copy of header (<a href="">#499</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/rust-bio/rust-htslib/compare/v0.47.1...v1.0.1">compare view</a></li>
</ul>
</details>
<br />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9ee7bcebd791`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.