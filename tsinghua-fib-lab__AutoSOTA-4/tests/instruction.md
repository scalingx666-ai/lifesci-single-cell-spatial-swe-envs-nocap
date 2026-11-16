# Issue

**Title:** Redesign results page with enhanced paper display and filtering

## Description

## Summary

Redesign the GitHub Pages site to provide a comprehensive view of all 105 optimized papers:
- **Compact table layout** — all papers visible in a scrollable list with ID, title, gain, and grade
- **Grade-based filtering** — Strong (≥10%), Moderate (3-10%), Modest (<3%)
- **Search** — filter by paper ID, title, or method name
- **Sort** — by best gain, paper ID, or smallest gain
- **Detail modal** — click any paper to see full optimization summary, metrics, and links
- **Feedback section** — links to GitHub Issues for community feedback
- **Stats cards** — total papers, strong wins, best gain, average gain
- **Responsive** — works on mobile, tablet, and desktop

## Files changed

| File | Description |
|------|-------------|
| `docs/index.html` | New page structure with hero, featured, papers table, modal, feedback |
| `docs/styles.css` | Enhanced dark theme with modal, table, tag, and feedback styles |
| `docs/script.js` | Parses README.md, renders stats/featured/table, search/filter/sort/modal |
| `index.html` | Synced with docs/ version |
| `styles.css` | Synced with docs/ version |
| `script.js` | Synced with docs/ version |

## Design

Keeps the existing Space Grotesk + IBM Plex Mono typography and dark theme. The data source remains `site-data/README.md` — no build step required.

## Test plan

- [x] 105 papers render correctly
- [x] Strong filter shows 26 papers
- [x] Search filters results in real-time
- [x] Sort by gain shows CertifiedUnlearning (63.64%) first
- [x] Modal opens on click with full details
- [x] Responsive layout on mobile viewport
- [x] No JavaScript errors

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4dd1b9746a78`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.