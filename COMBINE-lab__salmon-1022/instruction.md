# Issue

**Title:** fix(sketch): wire piscem hit positions into sketch mappings

## Description

Sketch mappings discarded the positions piscem already computes (SimpleHit.pos/mate_pos/fragment_length), so `--sketch --writeMappings` wrote POS=1 for every record, sketch bias collected from position 0 (degenerate), and the orphan ambiguous-fragment FLD term couldn't fire.

This wires ref_pos/fw_pos/rc_pos/read_len/r1_pos/r2_pos from the hit positions (approximate k-mer-anchor coords), mirroring selective-alignment conventions.

**Validation:** sketch quant.sf unchanged on concordant data (positions don't alter eq-classes); SAM POS now realistic (17/149, TLEN 183, 2298 distinct vs 1); sketch+bias now position-aware; full workspace tests + clippy green; real-data sketch mapping rate stable (~92.6%).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7a028056f2ed`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.