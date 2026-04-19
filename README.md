# Coup

**Calibrated vs. Uncalibrated Hierarchy in Multi-Agent LLM Debate Protocols**

Multi-agent LLM frameworks assign role labels (Expert/Junior, Deep/Fresh, CEO/Engineer) to structure debate. This paper asks: do those labels produce *calibrated* hierarchies (deference tracking judgment quality) or *uncalibrated* hierarchies (deference stuck on structural rank)? The distinction is operationalized via a Hierarchy Calibration Score C(P) and a Coup Threshold τ (the minimum subordinate-error level at which override becomes rational).

## Repository Structure

```
coup/
  paper/                      Domain -- manuscript source of truth
    main.tex
    references.bib
    figures/
  experiments/                Application (skeleton)
  literature/                 Reading notes, gap analysis
  planning/                   decisions log
    drafts/                   outline.md (superseded v3)
```

## License

CC-BY 4.0
