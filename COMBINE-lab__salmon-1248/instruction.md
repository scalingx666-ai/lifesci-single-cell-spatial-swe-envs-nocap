# Issue

**Title:** chore(deps): bump smol-toml from 1.8.0 to 1.9.1 in /website

## Description

Bumps [smol-toml](https://github.com/squirrelchat/smol-toml) from 1.8.0 to 1.9.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/squirrelchat/smol-toml/releases">smol-toml's releases</a>.</em></p>
<blockquote>
<h2>v1.9.1</h2>
<h2>What's Changed</h2>
<ul>
<li>fix: reject invalid extra exponent sign by <a href="https://github.com/cyyynthia"><code>@​cyyynthia</code></a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/squirrelchat/smol-toml/compare/v1.9.0...v1.9.1">https://github.com/squirrelchat/smol-toml/compare/v1.9.0...v1.9.1</a></p>
<h2>v1.9.0</h2>
<p><strong>Huge update</strong>!!! This is most likely the largest update the library received since its release, with lots of new features and improvements.</p>
<h3>Performance improvements</h3>
<p>Significant parts of the internal parse logic have been rewritten, improving performance by <strong>1.5x-2x</strong>. The library was already comfortably ahead of the others, but it is now faster than ever, sitting at <strong>4x faster parse performance</strong> than the closest maintained implementation.</p>
<p>Problematic code paths have also been replaced by safer implementations, solving potential DoS vectors. See GHSA-r4xh-jqrq-34v2.</p>
<p>Note: the objects returned by the library now have a <em>null prototype</em>. This is a transparent change for 99.9% of users, and is one of the most significant contributors to the major performance gains in this version.</p>
<h3>Full Temporal support</h3>
<p>Version 1.8.0 brought support for Temporal in <code>stringify</code>; now the library is also able to emit Temporal objects instead of its own ad-hoc <code>TomlDate</code> object. It is not enabled by default, but it will become the default in v2. Enable by setting <code>useLegacyDate: false</code> in the parser's options.</p>
<h4>Better Temporal support in stringify</h4>
<p>Temporal support has been improved since it released: Temporal objects that cannot be represented (such as <code>Temporal.PlainMonthDay</code>) now throw an error (instead of silently emitting a bogus object).</p>
<p>A new option has been added to <code>stringify</code> to disallow Temporal objects that cannot be fully represented in TOML. This includes <code>ZonedDateTime</code> objects with a IANA timezone attached instead of a plain offset, and dates with a specific calendar value set. Enable by setting <code>strictTemporal: true</code> in the options.</p>
<h3>Handling of unsafe keys</h3>
<p>Since its release the library has been protected against prototype pollution attacks, setting properties like <code>__proto__</code> using safe mechanisms that do not trigger prototype pollution. However, while the returned objects are safe on their own, they may become problematic if used carelessly.</p>
<p>Inspired by <code>secure-json-parse</code>, the library now offers a way to either drop unsafe properties from the returned object, or to throw an error and reject documents altogether. By default, these potentially unsafe keys are preserved and returned.</p>
<h3>Miscellaneous updates</h3>
<ul>
<li>Unicode BOM is now gracefully accepted and ignored.</li>
<li>Table array headers are now properly checked again. Reported in <a href="">#65</a>.</li>
<li>Closed certain gaps where invalid whitespace would be accepted. Reported in <a href="">#61</a>.</li>
<li>Bogus local date and local time values with a UTC offset are no longer accepted.</li>
<li>Certain error messages are more accurate and handle errors at line boundaries better.</li>
<li>The default export of the lib is now formally deprecated; use a <code>import *</code> instead. Proposed in <a href="">#50</a>.</li>
<li>On Node 20+, strings that contain lone surrogates are now normalised to well-formed strings.</li>
<li>On Node 20+, keys that contain lone surrogates are now rejected.</li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/squirrelchat/smol-toml/compare/v1.8.0...v1.9.0">https://github.com/squirrelchat/smol-toml/compare/v1.8.0...v1.9.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>69aa050</code></a> fix: actually properly fix exponent issues</li>
<li><a href=""><code>7be7084</code></a> chore: version bump</li>
<li><a href=""><code>be3290d</code></a> chore: upgrade deps</li>
<li><a href=""><code>86c7613</code></a> fix: reject invalid extra exponent sign</li>
<li><a href=""><code>6f9739a</code></a> fix: gate <code>[is|to]WellFormed</code> (Node 18 compat)</li>
<li><a href=""><code>a73ca32</code></a> fix: no Temporal with toml-test when Node &lt; 26</li>
<li><a href=""><code>7727890</code></a> chore: version bump</li>
<li><a href=""><code>641903d</code></a> chore: rewrite README.md</li>
<li><a href=""><code>2df14c5</code></a> fix(types): make it work if Temporal doesn't exist</li>
<li><a href=""><code>3eaa44e</code></a> chore: update benchmark harness</li>
<li>Additional commits viewable in <a href="https://github.com/squirrelchat/smol-toml/compare/v1.8.0...v1.9.1">compare view</a></li>
</ul>
</details>
<br />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `987c2bdced4e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.