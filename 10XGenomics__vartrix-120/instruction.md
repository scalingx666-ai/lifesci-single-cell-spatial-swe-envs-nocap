# Issue

**Title:** Bump clap from 2.33.0 to 4.5.13 and sprs from 0.7 to 0.11

## Description

Bumps [clap](https://github.com/clap-rs/clap) from 2.33.0 to 4.5.13.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/clap-rs/clap/releases">clap's releases</a>.</em></p>
<blockquote>
<h2>v4.5.13</h2>
<h2>[4.5.13] - 2024-07-31</h2>
<h3>Fixes</h3>
<ul>
<li><em>(derive)</em> Improve error message when <code>#[flatten]</code>ing an optional <code>#[group(skip)]</code></li>
<li><em>(help)</em> Properly wrap long subcommand descriptions in help</li>
</ul>
<h2>v4.5.12</h2>
<h2>[4.5.12] - 2024-07-31</h2>
<h2>v4.5.10</h2>
<h2>[4.5.10] - 2024-07-23</h2>
<h2>v4.5.9</h2>
<h2>[4.5.9] - 2024-07-09</h2>
<h3>Fixes</h3>
<ul>
<li><em>(error)</em> When defining a custom help flag, be sure to suggest it like we do the built-in one</li>
</ul>
<h2>v4.5.8</h2>
<h2>[4.5.8] - 2024-06-28</h2>
<h3>Fixes</h3>
<ul>
<li>Reduce extra flushes</li>
</ul>
<h2>v4.5.7</h2>
<h2>[4.5.7] - 2024-06-10</h2>
<h3>Fixes</h3>
<ul>
<li>Clean up error message when too few arguments for <code>num_args</code></li>
</ul>
<h2>v4.5.6</h2>
<h2>[4.5.6] - 2024-06-06</h2>
<h2>v4.5.4</h2>
<h2>[4.5.4] - 2024-03-25</h2>
<h3>Fixes</h3>
<ul>
<li><em>(derive)</em> Allow non-literal <code>#[arg(id)]</code> attributes again</li>
</ul>
<h2>v4.5.3</h2>
<h2>[4.5.3] - 2024-03-15</h2>
<h3>Internal</h3>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/clap-rs/clap/blob/main/CHANGELOG.md">clap's changelog</a>.</em></p>
<blockquote>
<h2>[4.5.13] - 2024-07-31</h2>
<h3>Fixes</h3>
<ul>
<li><em>(derive)</em> Improve error message when <code>#[flatten]</code>ing an optional <code>#[group(skip)]</code></li>
<li><em>(help)</em> Properly wrap long subcommand descriptions in help</li>
</ul>
<h2>[4.5.12] - 2024-07-31</h2>
<h2>[4.5.11] - 2024-07-25</h2>
<h2>[4.5.10] - 2024-07-23</h2>
<h2>[4.5.9] - 2024-07-09</h2>
<h3>Fixes</h3>
<ul>
<li><em>(error)</em> When defining a custom help flag, be sure to suggest it like we do the built-in one</li>
</ul>
<h2>[4.5.8] - 2024-06-28</h2>
<h3>Fixes</h3>
<ul>
<li>Reduce extra flushes</li>
</ul>
<h2>[4.5.7] - 2024-06-10</h2>
<h3>Fixes</h3>
<ul>
<li>Clean up error message when too few arguments for <code>num_args</code></li>
</ul>
<h2>[4.5.6] - 2024-06-06</h2>
<h2>[4.5.5] - 2024-06-06</h2>
<h3>Fixes</h3>
<ul>
<li>Allow <code>exclusive</code> to override <code>required_unless_present</code>, <code>required_unless_present_any</code>, <code>required_unless_present_all</code></li>
</ul>
<h2>[4.5.4] - 2024-03-25</h2>
<h3>Fixes</h3>
<ul>
<li><em>(derive)</em> Allow non-literal <code>#[arg(id)]</code> attributes again</li>
</ul>
<h2>[4.5.3] - 2024-03-15</h2>
<h3>Internal</h3>
<ul>
<li><em>(derive)</em> Update <code>heck</code></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d222ae4</code></a> chore: Release</li>
<li><a href=""><code>a8abcb4</code></a> docs: Update changelog</li>
<li><a href=""><code>2690e1b</code></a> Merge pull request <a href="">#5621</a> from shannmu/dynamic_valuehint</li>
<li><a href=""><code>7fd7b3e</code></a> feat(clap_complete): Support to complete custom value of argument</li>
<li><a href=""><code>fc6aaca</code></a> Merge pull request <a href="">#5638</a> from epage/cargo</li>
<li><a href=""><code>631e54b</code></a> docs(cookbook): Style cargo plugin</li>
<li><a href=""><code>6fb49d0</code></a> Merge pull request <a href="">#5636</a> from gibfahn/styles_const</li>
<li><a href=""><code>6f215ee</code></a> refactor(styles): make styles example use a const</li>
<li><a href=""><code>bbb2e6f</code></a> test: Add test case for completing custom value of argument</li>
<li><a href=""><code>999071c</code></a> fix: Change <code>visible</code> to <code>hidden</code></li>
<li>Additional commits viewable in <a href="https://github.com/clap-rs/clap/compare/v2.33.0...clap_complete-v4.5.13">compare view</a></li>
</ul>
</details>
<br />

> **Note**
> Automatic rebases have been disabled on this pull request as it has been open for over 30 days.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c9281daa23fd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.