# Issue

**Title:** chore(deps): bump rdkit from 2026.3.3 to 2026.3.4

## Description

Bumps [rdkit](https://github.com/rdkit/rdkit) from 2026.3.3 to 2026.3.4.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/rdkit/rdkit/releases">rdkit's releases</a>.</em></p>
<blockquote>
<h2>2026_03_4 (Q1 2026) Release</h2>
<h1>Release_2026.03.4</h1>
<p>(Changes relative to Release_2026.03.3)</p>
<h2>Acknowledgements</h2>
<p>(Note: I'm no longer attempting to manually curate names. If you would like to
see your contribution acknowledged with your name, please set your name in
GitHub)</p>
<p>Rody Arantes, Katharina Buchthal, David Cosgrove, Tad Hurst, Steven Kearnes,
Brian Kelley, Niels Maeder, John Mayfield, Dan Nealschneider, Yakov Pechersky,
Ricardo Rodriguez, Jon Swain, Rachel Walker, Inwan Yoo, Nic Zonta, ankar-dav,
ajeyabsf, thomp-j, vwe-ibm</p>
<h2>Backwards incompatible changes:</h2>
<ul>
<li><code>MolTransforms.h</code> now includes <code>&lt;Eigen/Core&gt;</code> instead of <code>&lt;Eigen/Dense&gt;</code>. C++
code that included <code>MolTransforms.h</code> and relied on it to transitively pull in the
Eigen dense modules (LU/QR/SVD/etc.) must now include <code>&lt;Eigen/Dense&gt;</code> directly.</li>
<li>The <code>DistGeomHelpers::EmbedParameters</code> struct no longer has a constructor that
takes arguments in C++. If you want to initialize data members to non-default
values, use the designated initialization syntax. This change does not affect
Python.</li>
</ul>
<h2>New Features and Enhancements:</h2>
<ul>
<li>Add spiro flipping to 2D coord generation
(github pull <a href="">#9204</a> from ZontaNicola)</li>
<li>Adds SVE to BFGSOpt
(github pull <a href="">#9216</a> from ajeyabsf)</li>
<li>Multi conf gaussian shape
(github pull <a href="">#9265</a> from DavidACosgrove)</li>
<li>All-In-One coordinate refinement for ETKDG
(github pull <a href="">#9292</a> from nmaeder)</li>
<li>Synthon substructure search 2x performance
(github pull <a href="">#9307</a> from d-b-w)</li>
<li>Configurable stereo labels in MolDraw2D
(github pull <a href="">#9311</a> from DavidACosgrove)</li>
<li>Replace combineMols with RWMol::insertMol in SynthonSpaceSearch
(github pull <a href="">#9319</a> from DavidACosgrove)</li>
<li>Add opt-in unity (jumbo) builds + fix latent missing include guards
(github pull <a href="">#9342</a> from skearnes)</li>
<li>Make substructure search Ctrl+c interruptible
(github pull <a href="">#9349</a> from ricrogz)</li>
</ul>
<h2>Documentation:</h2>
<ul>
<li><code>rdchem.pyi</code> typing issue: non-default parameter following default parameter
(github issue <a href="">#9335</a> from ankar-dav)</li>
</ul>
<h2>Bug Fixes:</h2>
<ul>
<li>Update RDKit_Book.rst
(github pull <a href="">#7946</a> from johnmay)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/rdkit/rdkit/commits">compare view</a></li>
</ul>
</details>
<br />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fba240efa246`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.