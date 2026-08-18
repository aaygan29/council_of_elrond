# council_of_elrond

An empirical, adversarial research-review tool for Claude. It convenes a fixed panel of skeptics and withholds a verdict until the work has survived a hard empirical gate ladder, so a weak finding can fail here, in private, rather than later.

## What it does

- Works on two kinds of input:
  - **Documents / write-ups** (Markdown, PDF, DOCX): drafts, proposals, preregistrations.
  - **Live artifacts** (code, results files, notebooks, statistical output): recomputes headline numbers from the source files instead of trusting the prose. A number in the text that disagrees with its source file is flagged.
- Runs a twelve-seat skeptic panel (eight standing + four specialists) and an extended gate ladder. The empirical core (Gates 0-6) asks whether the finding is real: provenance/leakage, seed variance, specification robustness, specificity, confound control, mechanism/necessity, claim calibration. The methodology-completeness tier (Gates 7-11) asks whether the study was well built and reported: external validity/generalization, measurement validity and reliability, reproducibility/computational provenance, ethics/safety/responsible disclosure, and analytic integrity (preregistration, confirmatory-vs-exploratory). Each seat maps to a distinct pillar of experimental methodology, so the panel covers a study end to end.
- **Quantitative error analysis.** For every headline number it does the arithmetic a hostile methods reviewer would: which error is at risk here (Type I false positive vs Type II underpowered null), the multiple-comparisons expectation and binomial by-chance tail, survivors after correction, minimum detectable effect size, positive predictive value at the true prior, statcheck/GRIM consistency, p-curve/caliper p-hacking screens, and leave-one-out fragility. Adjectives are not allowed to stand in for the computed bound. See `statistical-robustness.md`.
- **Conditional figure review (Gate F).** When (and only when) the work contains figures, it judges each one on message/takeaway, honesty of the visual encoding (truncated axes, missing error bars, absent chance line), readability/colorblind-safety, and claim-figure correspondence. A figure that quietly contradicts a central claim is a Blocker. Text-only drafts skip it. See `figure-review.md`.
- **Two stances.** A *gatekeeper* stance for pre-submission ("tear it apart") and a *development* stance that keeps the rigor but adds generative paper-writing feedback: an exposition/argument-chain pass, generative figure feedback, and a Reviewer-2 pre-mortem that pre-loads the objections a hostile reviewer will raise. See `paper-development.md`.
- Returns a decision (ACCEPT, MAJOR REVISION, or REJECT), a severity-ranked list of findings, and the single highest-leverage change that would move the work up one level.

## Data & grounding

The gate ladder encodes empirical failure modes that have sunk real in-silico studies: single-run "improvements" that were seed variance, cross-system correlations that were scale-confounded, components that were functionally redundant under ablation, and synthetic-data pilots that "fingerprinted" random seeds rather than biology. No external dataset is required; it operates on whatever artifact you give it.

## License

MIT — see [LICENSE](LICENSE).
