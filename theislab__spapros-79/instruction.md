# Issue

**Title:** [DEPENDABOT]: Bump pygments from 2.8.1 to 2.9.0

## Description

Bumps [pygments](https://github.com/pygments/pygments) from 2.8.1 to 2.9.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pygments/pygments/releases">pygments's releases</a>.</em></p>
<blockquote>
<h2>2.9.0</h2>
<ul>
<li>
<p>Added lexers:</p>
<ul>
<li>APDL, gcode (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1714">#1714</a>)</li>
<li>Kuin (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1300">#1300</a>)</li>
<li>NestedText (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1578">#1578</a>)</li>
<li>OMG IDL (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1595">#1595</a>)</li>
<li>TEAL (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1671">#1671</a>)</li>
<li>ThingsDB (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1295">#1295</a>)</li>
<li>WebAssembly (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1416">#1416</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1564">#1564</a>)</li>
</ul>
</li>
<li>
<p>Updated lexers:</p>
<ul>
<li>AMDGPU (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1717">#1717</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1775">#1775</a>)</li>
<li>APL (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1747">#1747</a>)</li>
<li>C/C++: Improve namespace handling (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1722">#1722</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1561">#1561</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1719">#1719</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1746">#1746</a>)</li>
<li>Chapel (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1743">#1743</a>)</li>
<li>Coq (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1721">#1721</a>)</li>
<li>Cython (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/853">#853</a>)</li>
<li>Groovy (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1765">#1765</a>)</li>
<li>JavaScript (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1741">#1741</a>)</li>
<li>Julia (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1715">#1715</a>)</li>
<li>Octave: Allow multiline and block-percent comments (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1726">#1726</a>)</li>
<li>PowerShell: Improve lexing of <code>:</code> (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1682">#1682</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1758">#1758</a>)</li>
<li>PromQL (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1783">#1783</a>)</li>
<li>Python: Improve float parsing (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1768">#1768</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1740">#1740</a>)</li>
<li>Rust (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1061">#1061</a>)</li>
<li>Scala: Rewrite to support Scala3 (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1694">#1694</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1035">#1035</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1121">#1121</a>)</li>
<li>Swift (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1767">#1767</a>)</li>
<li>Terraform: Support 0.14 syntax (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1756">#1756</a>)</li>
<li>Velocity: Detect multi-line patterns (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1776">#1776</a>)</li>
</ul>
</li>
<li>
<p>Add Pango formatter (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1727">#1727</a>)</p>
</li>
<li>
<p>Autopygmentize uses <code>file</code> first instead of <code>pygments -N</code> (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1786">#1786</a>)</p>
</li>
<li>
<p>Fix links (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1716">#1716</a>)</p>
</li>
<li>
<p>Fix issue with LaTeX formatter and <code>minted</code> (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1734">#1734</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1735">#1735</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1736">#1736</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1737">#1737</a>)</p>
</li>
<li>
<p>Improve alias order (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1780">#1780</a>)</p>
</li>
<li>
<p>Improve line number colors (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1779">#1779</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1778">#1778</a>)</p>
</li>
<li>
<p>Fix CTag related issue (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1724">#1724</a>)</p>
</li>
<li>
<p>Recognize <code>.leex</code> as Elixir templates</p>
</li>
<li>
<p>Updated <code>filename</code> handling in HTML formatter if <code>linenos='table'</code> (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1757">#1757</a>)</p>
<ul>
<li>Previously the filename would be emitted within the <code>&lt;td&gt;</code> holding the code, but outside the <code>&lt;pre&gt;</code>. This would invariably break the a lignment with line numbers.</li>
<li>Now if <code>filename</code> is specified, a separate <code>&lt;tr&gt;</code> is emitted before the table content which contains a single <code>&lt;th&gt;</code> with <code>colspan=2</code> so it
spans both the line number and code columns. The filename is still within <code>&lt;span class=&quot;filename&quot;&gt;...&lt;/span&gt;</code> so any existing styles
should still apply, although the CSS path may need to change.</li>
<li>For an example of the new output format see <code>table_cls_step_1_start_1_special_0_noanchor_filename.html</code>
in the <code>tests/html_linenos_expected_output/</code> directory.</li>
<li>For more details and discussion see the issue <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1757">pygments/pygments#1757</a></li>
</ul>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/pygments/pygments/blob/master/CHANGES">pygments's changelog</a>.</em></p>
<blockquote>
<h2>Version 2.9.0</h2>
<p>(released May 3rd, 2021)</p>
<ul>
<li>
<p>Added lexers:</p>
<ul>
<li>APDL, gcode (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1714">#1714</a>)</li>
<li>Kuin (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1300">#1300</a>)</li>
<li>NestedText (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1578">#1578</a>)</li>
<li>OMG IDL (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1595">#1595</a>)</li>
<li>TEAL (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1671">#1671</a>)</li>
<li>ThingsDB (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1295">#1295</a>)</li>
<li>WebAssembly (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1416">#1416</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1564">#1564</a>)</li>
</ul>
</li>
<li>
<p>Updated lexers:</p>
<ul>
<li>AMDGPU (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1717">#1717</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1775">#1775</a>)</li>
<li>APL (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1747">#1747</a>)</li>
<li>C/C++: Improve namespace handling (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1722">#1722</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1561">#1561</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1719">#1719</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1746">#1746</a>)</li>
<li>Chapel (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1743">#1743</a>)</li>
<li>Coq (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1721">#1721</a>)</li>
<li>Cython (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/853">#853</a>)</li>
<li>Groovy (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1765">#1765</a>)</li>
<li>JavaScript (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1741">#1741</a>)</li>
<li>Julia (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1715">#1715</a>)</li>
<li>Octave: Allow multiline and block-percent comments (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1726">#1726</a>)</li>
<li>PowerShell: Improve lexing of <code>:</code> (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1682">#1682</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1758">#1758</a>)</li>
<li>PromQL (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1783">#1783</a>)</li>
<li>Python: Improve float parsing (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1768">#1768</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1740">#1740</a>)</li>
<li>Rust (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1061">#1061</a>)</li>
<li>Scala: Rewrite to support Scala3 (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1694">#1694</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1035">#1035</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1121">#1121</a>)</li>
<li>Swift (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1767">#1767</a>)</li>
<li>Terraform: Support 0.14 syntax (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1756">#1756</a>)</li>
<li>Velocity: Detect multi-line patterns (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1776">#1776</a>)</li>
</ul>
</li>
<li>
<p>Add Pango formatter (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1727">#1727</a>)</p>
</li>
<li>
<p>Autopygmentize uses <code>file</code> first instead of <code>pygments -N</code> (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1786">#1786</a>)</p>
</li>
<li>
<p>Fix links (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1716">#1716</a>)</p>
</li>
<li>
<p>Fix issue with LaTeX formatter and <code>minted</code> (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1734">#1734</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1735">#1735</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1736">#1736</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1737">#1737</a>)</p>
</li>
<li>
<p>Improve alias order (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1780">#1780</a>)</p>
</li>
<li>
<p>Improve line number colors (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1779">#1779</a>, <a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1778">#1778</a>)</p>
</li>
<li>
<p>Fix CTag related issue (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1724">#1724</a>)</p>
</li>
<li>
<p>Recognize <code>.leex</code> as Elixir templates</p>
</li>
<li>
<p>Updated <code>filename</code> handling in HTML formatter if <code>linenos='table'</code> (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1757">#1757</a>)</p>
<ul>
<li>Previously the filename would be emitted within the <code>&lt;td&gt;</code> holding the
code, but outside the <code>&lt;pre&gt;</code>. This would invariably break the alignment
with line numbers.</li>
<li>Now if <code>filename</code> is specified, a separate <code>&lt;tr&gt;</code> is emitted before the</li>
</ul>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2c0ca2e</code></a> Prepare 2.9.0 release.</li>
<li><a href=""><code>708b1a7</code></a> Update CHANGES.</li>
<li><a href=""><code>631e8cf</code></a> Add support for elixir phoenix leex templates (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1577">#1577</a>)</li>
<li><a href=""><code>46c3ddc</code></a> Update CHANGES.</li>
<li><a href=""><code>3752e98</code></a> groovy lexer: detect quoted function names (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1765">#1765</a>)</li>
<li><a href=""><code>30cfa26</code></a> encode <code>str</code> into <code>bytes</code> for <code>_lookup_ctag</code> argument; (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1724">#1724</a>)</li>
<li><a href=""><code>ac40a66</code></a> Support Terraform 0.14 syntax (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1756">#1756</a>)</li>
<li><a href=""><code>7f85893</code></a> Support for OMG IDL (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1595">#1595</a>)</li>
<li><a href=""><code>f0b806f</code></a> autopygmentize: use file before pygmentize; add JSON support (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1786">#1786</a>)</li>
<li><a href=""><code>f0d433d</code></a> Add gruvbox styles (<a href="https://github-redirect.dependabot.com/pygments/pygments/issues/1763">#1763</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/pygments/pygments/compare/2.8.1...2.9.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=pygments&package-manager=pip&previous-version=2.8.1&new-version=2.9.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7b50348c8d53`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.