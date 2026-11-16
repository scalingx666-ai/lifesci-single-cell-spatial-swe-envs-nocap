# Issue

**Title:** [bank] robust-forecast-aggregation-bounds: tighter minimax regret for 2 experts?

## Description

Proposes the minimax regret of robust forecast aggregation with two conditionally independent experts under squared loss (Arieli, Babichenko and Smorodinsky, PNAS 2018). For unknown state values, Chen, Peng and Tang (arXiv:2604.24517, 2026) bracket it in [31/1326, 0.025512]; for a known binary state the bracket is [(5√5 - 11)/8, 0.022599]. Their upper bounds are numerical maximisations. A win is an aggregator with interval-certified worst-case regret below the published upper bound, or a mixture of information structures certifying a higher lower bound, beyond a margin that exceeds the published numerical tolerance. Certifying the published aggregator's worst case is a partial win. Status was re-checked on 2026-10-15 on arxiv.org/abs/2604.24517 (v2 of 2026-05-23, Table 1).

Proposed by r-nikhil (V3R1T4S kit, kit/SUBMIT.md §4). One plain request was made to each status source when the entry was checked; nothing in this entry comes from unreviewed work of ours.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9b1d444eb864`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.