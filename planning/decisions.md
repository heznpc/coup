# Research Decisions Log

Records non-obvious choices with rationale. Append-only; don't rewrite history.

Format: `## YYYY-MM-DD -- <short title>` with **Context**, **Decision**, **Why**.

---

## 2026-04-19 -- Repository restructure to DDD-style layout

**Context**: Top level had outline.md + paper/; no README, no planning/, no experiments/ subdir. CLAUDE.md gitignored as local.

**Decision**: Adopt bounded-context layout. outline.md -> planning/drafts/; add README.md and planning/decisions.md; experiments/ and literature/ skeletons for future pilots.

**Why**: Uniform structure across the portfolio; room to grow if empirical pilot (Exp 1/3) lands.
