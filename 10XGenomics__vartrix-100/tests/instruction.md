# Issue

**Title:** Bump simplelog from 0.5.3 to 0.12.2

## Description

Bumps [simplelog](https://github.com/drakulix/simplelog.rs) from 0.5.3 to 0.12.2.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/Drakulix/simplelog.rs/blob/master/CHANGELOG.md">simplelog's changelog</a>.</em></p>
<blockquote>
<h2>Unreleased</h2>
<ul>
<li>The <code>new</code> method of loggers are now <code>#[must_use]</code> to prevent confusion when <code>new</code> is used called instead of <code>init</code></li>
<li>Adjusted dependency to support termcolor crate version 1.2 (PR <a href="">#131</a>, credits to <a href="https://github.com/danielparks"><code>@​danielparks</code></a>)</li>
</ul>
<h2>v0.12.0</h2>
<ul>
<li>Replaces the semingly unmaintained chrono library with the time crate.</li>
<li>Addresses through this update
<ul>
<li>RUSTSEC-2020-0159 (chrono)</li>
<li>RUSTSEC-2020-0071 (time)</li>
</ul>
</li>
<li><code>ConfigBuilder::set_time_to_local</code> is replaced by <code>ConfigBuilder::set_time_offset_to_local</code>.
<ul>
<li>This function requires the new (and by default activated) <code>local-offset</code> feature.</li>
<li>This function may fail, for more information read the docs.</li>
<li>simplelog will not determine the local offset dynamically anymore, but only once, when this config option is set.
<ul>
<li>Due to safety reasons there is no way to provide this property currently.</li>
</ul>
</li>
</ul>
</li>
<li><code>ConfigBuilder::set_time_offset</code> now takes a <code>time::UtcOffset</code> instead of a <code>chrono::FixedOffset</code>.</li>
<li><code>ConfigBuilder::set_time_format</code> has been replaced by three new variants
<ul>
<li><code>ConfigBuilder::set_time_format_rfc2822</code> sets the time format to use the format described by rfc2822.</li>
<li><code>ConfigBuilder::set_time_format_rfc3339</code> sets the time format to use the format described by rfc3339.</li>
<li><code>ConfigBuilder::set_time_format_custom</code> sets the time format to a custom time format best created using <code>time::macros::format_description</code>.
<ul>
<li>Runtime provided time format configuration is possible, but difficult due to lifetime constraints.</li>
<li>Fixing this will require a solution to <a href="">time-rs/time#429</a></li>
</ul>
</li>
<li><em>Note</em>: The default format is unchanged &quot;[hour]:[minute]:[second]&quot;</li>
</ul>
</li>
</ul>
<h2>v0.11.0</h2>
<ul>
<li>Add colored log levels using <code>ansi_term</code> (PR <a href="">#88</a>, credits to <a href="https://github.com/manio"><code>@​manio</code></a>)</li>
<li>Add target padding (PR <a href="">#85</a>, credits to <a href="https://github.com/bytebeamio"><code>@​bytebeamio</code></a>)</li>
<li>Add optional color and style support using <code>paris</code> crate (PR <a href="">#84</a>, credits to <a href="https://github.com/manio"><code>@​manio</code></a>)</li>
</ul>
<h2>v0.10.2</h2>
<ul>
<li>Fix flushing with <code>BufferedStandardStreams</code> (PR <a href="">#82</a>, credits to <a href="https://github.com/mrkline"><code>@​mrkline</code></a>)</li>
</ul>
<h2>v0.10.1</h2>
<ul>
<li>Fix TermLogger performance using <code>termcolor::BufferedStandardStream</code> (PR <a href="">#80</a>, credits to <a href="https://github.com/mrkline"><code>@​mrkline</code></a>)</li>
<li>Add write thread name support for <code>termlog</code> (PR <a href="">#76</a>, credits to <a href="https://github.com/zeroflaw"><code>@​zeroflaw</code></a>)</li>
</ul>
<h2>v0.10.0</h2>
<ul>
<li>Fix wrong argument naming (PR <a href="">#70</a>, credits to <a href="https://github.com/scvalex"><code>@​scvalex</code></a>)</li>
<li><em>Breaking</em>: More color customization options (PR <a href="">#72</a>, credits to <a href="https://github.com/mrkline"><code>@​mrkline</code></a>)</li>
<li>Clarify docs on config levels</li>
</ul>
<h2>v0.9.0</h2>
<ul>
<li>Add customizable level label colors (PR <a href="">#69</a>. credits to <a href="https://github.com/JarrettBillingsley"><code>@​JarrettBillingsley</code></a>)</li>
<li>Remove unneeded TermLogError</li>
<li>Future-proof config by adding <code>#[non_exhaustive]</code></li>
<li>Fix compiling with minimal-versions</li>
</ul>
<h2>v0.8.0</h2>
<ul>
<li>Switch from <code>term</code> to <code>termcolor</code> (PR <a href="">#59</a>. credits to <a href="https://github.com/raybritton"><code>@​raybritton</code></a>)</li>
<li>Fix typo in docs (PR <a href="">#58</a>, credits to <a href="https://github.com/anthonyjmartinez"><code>@​anthonyjmartinez</code></a>)</li>
<li>Switch default padding to <code>Off</code>. Padding is annoyingly controversial, just set it to whatever you prefer, if you want it.</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>47f02be</code></a> v0.12.2</li>
<li><a href=""><code>2f0dcf1</code></a> v0.12.1</li>
<li><a href=""><code>626467d</code></a> Merge pull request <a href="">#114</a> from lazorchakp/testlogger-remove-newline</li>
<li><a href=""><code>8481058</code></a> Remove newline from TestLogger time output</li>
<li><a href=""><code>c927c19</code></a> Merge pull request <a href="">#113</a> from rusty-snake/patch-1</li>
<li><a href=""><code>79493ec</code></a> Make CHANGELOG.md more readable</li>
<li><a href=""><code>95275c8</code></a> v0.12.0</li>
<li><a href=""><code>f137eb4</code></a> Merge pull request <a href="">#101</a> from jacobtread/patch-1</li>
<li><a href=""><code>ba17254</code></a> Merge pull request <a href="">#99</a> from zjp-CN/master</li>
<li><a href=""><code>44a294f</code></a> Merge pull request <a href="">#95</a> from Drakulix/fix/chrono_dep</li>
<li>Additional commits viewable in <a href="https://github.com/drakulix/simplelog.rs/compare/v0.5.3...v0.12.2">compare view</a></li>
</ul>
</details>
<br />

> **Note**
> Automatic rebases have been disabled on this pull request as it has been open for over 30 days.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c79e4564a9b9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.