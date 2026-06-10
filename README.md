# council-review

An empirical, adversarial research-review skill for Claude.

Council Review convenes a fixed panel of skeptics (the Council of Elrond) and refuses to render a verdict until the work has survived a hard empirical gate ladder. The goal: let a finding die here, in private, rather than in front of a reviewer or after publication.

Works on two kinds of input:

- **Manuscripts** -- papers, proposals, preregistrations, drafts (Markdown, PDF, DOCX)
- **Live artifacts** -- code, results files, notebooks, statistical output. In this mode it recomputes headline numbers from the source files instead of trusting the prose. A number in the text that disagrees with the file it came from is a finding.

Output is a decision (ACCEPT, MAJOR REVISION, or REJECT), a severity-ranked list of findings, and the single highest-leverage experiment or edit that would move the work up one decision level.

---

## Why it exists

The gate ladder encodes empirical failure modes that have sunk real in-silico studies:

- A single-run "improvement" that was **seed variance** once run across 20 seeds
- A cross-system correlation that was real but **scale-confounded**: significant raw, not significant after partialling out size
- A component that was present but **functionally redundant** under ablation (8.6x less load-bearing than the parts doing the actual work)
- A synthetic-data pilot that fingerprinted "subjects" perfectly because they were different random seeds, not biology

A reviewer who only reads prose misses all four. A reviewer who recomputes and walks a fixed ladder catches them.

---

## Install

### Claude Code (one command)
