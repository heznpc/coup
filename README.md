# Coup

This is a concept note, not a finished paper.

Research Program: 2 (Epistemic Failure and Correction)\
Status: Concept note\
Relationship to other work: Companion to ploidy

---

**Calibrated vs. Uncalibrated Hierarchy in Multi-Agent LLM Debate Protocols**

Multi-agent LLM frameworks assign role labels — Expert/Junior, Deep/Fresh, CEO/Engineer — to structure debate. The question this paper asks: do those labels produce *calibrated* hierarchies (deference tracking judgment quality) or *uncalibrated* hierarchies (deference stuck on structural rank, regardless of who is right)?

The distinction is operationalized via two metrics:

- **C(P) — Hierarchy Calibration Score.** `hit_rate − false_deference_rate`. Measures whether an agent's authority correlates with its actual correctness.
- **τ — Coup Threshold.** The minimum subordinate-error level at which the dominant agent's override becomes rational. A protocol with low τ tolerates premature override; a protocol with high τ stays stuck on rank.

The framing draws on human organizational research where calibration mechanisms — Crew Resource Management, Toyota's andon cord, the WHO Surgical Safety Checklist — preserve hierarchy while embedding structured override. The design goal is not flattening; it is calibration.

## Scope

Independent paper targeting general multi-agent debate protocols. Ploidy, MetaGPT, CrewAI, and AutoGen appear as case studies, not as the unit of analysis. Core experiments (Exp 1 — role-label effect; Exp 3 — coup threshold) require only `claude --print` with identical models under different role labels; no MCP or specialized infrastructure needed.

## Repository layout

```
paper/                 Manuscript source of truth (Domain)
  main.tex             April 2026 draft
  references.bib
  figures/             (placeholder — no figures yet)
experiments/           Skeleton — Exp 1 / 3 pilot forthcoming (Application)
literature/            Reading notes, gap analysis
planning/              decisions.md + drafts/outline.md (superseded v3)
```

## Currently implemented

- Draft manuscript (`paper/main.tex`) covering abstract, introduction, related work, six proposed experiments, and the C(P) / τ formalism
- Repository skeleton in DDD-style layout (paper = Domain / experiments = Application / literature / planning)

## Planned

- Pilot for Exp 1 (role-label effect on identical models)
- Pilot for Exp 3 (coup-threshold measurement)
- Case-study writeups for MetaGPT, CrewAI, AutoGen, Ploidy

## Design intent

The hierarchy-calibration framing is deliberately distinct from "anti-hierarchy" or "flatten the debate" framings in the multi-agent literature. Flattened protocols pay coordination costs without removing the underlying source of distortion (information volume, temporal primacy, label exposure to convergence engines). The paper argues that the engineering question is *which override mechanism gets embedded*, not *whether hierarchy exists*.

## Non-goals

- Not a benchmark of any single multi-agent framework
- Not an empirical claim — pilot data is not yet collected
- Not a prescription for a specific protocol; the contribution is the measurement apparatus

## Redacted

- External persons named in any draft material — not surfaced in published prose, citations, or acknowledgements
- Internal critique vocabulary about pilot scope or reviewer expectations — paraphrased into framing claims rather than reproduced verbatim
- Account identifiers, tokens, or session metadata — never committed; SECURITY.md is the private channel for any accidental leak

## Companion relationship

Coup sits next to ploidy in Program 2 (Epistemic Failure and Correction). Ploidy anchors the program with calibrated-vs-uncalibrated *judgment* between sessions; coup extends the same question to *hierarchy between agents inside a debate protocol*. The two papers share the calibration vocabulary but stand independently — coup does not require ploidy's machinery to read or reproduce.

## License

CC-BY-4.0 — see `LICENSE` for the full text and `CITATION.cff` for the canonical attribution name.
