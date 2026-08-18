# council_of_elrond

An empirical, adversarial research-review tool for Claude. It convenes a fixed panel of skeptics and withholds a verdict until the work has survived a hard empirical gate ladder, so a weak finding can fail here, in private, rather than later.

## What it does

- Works on two kinds of input:
  - **Documents / write-ups** (Markdown, PDF, DOCX): drafts, proposals, preregistrations.
  - **Live artifacts** (code, results files, notebooks, statistical output): recomputes headline numbers from the source files instead of trusting the prose. A number in the text that disagrees with its source file is flagged.
- Runs a twelve-seat skeptic panel (eight standing + four specialists) and an extended gate ladder. The empirical core (Gates 0-6) asks whether the finding is real: provenance/leakage, seed variance, specification robustness, specificity, confound control, mechanism/necessity, claim calibration. The methodology-completeness tier (Gates 7-11) asks whether the study was well built and reported: external validity/generalization, measurement validity and reliability, reproducibility/computational provenance, ethics/safety/responsible disclosure, and analytic integrity (preregistration, confirmatory-vs-exploratory). Each seat maps to a distinct pillar of experimental methodology, so the panel covers a study end to end.
- **Quantitative error analysis.** For every headline number it does the arithmetic a hostile methods reviewer would: which error is at risk here (Type I false positive vs Type II underpowered null), the multiple-comparisons expectation and binomial by-chance tail, survivors after correction, minimum detectable effect size, positive predictive value at the true prior, statcheck/GRIM consistency, p-curve/caliper p-hacking screens, and leave-one-out fragility. Adjectives are not allowed to stand in for the computed bound. See `statistical-robustness.md`.
- **Conditional figure review (Gate F).** When (and only when) the work contains figures, it judges each one on message/takeaway, honesty of the visual encoding (truncated axes, missing error bars, absent chance line), readability/colorblind-safety, and claim-figure correspondence. A figure that quietly contradicts a central claim is a Blocker. Text-only drafts skip it. See `figure-review.md`.
- **Optional NeurIPS-style score (Gate S).** When a NeurIPS-style venue is named or a rating is requested, Elrond translates the verdict onto the five-axis reviewer form - Soundness /4, Presentation /4, Contribution /4, Overall /10, Confidence /5. Every axis cites a gate result or a named finding, the Overall sits inside the verdict's band (REJECT 1-4, MAJOR REVISION 4-6, ACCEPT 6-9), and the score never overrides the ACCEPT/MAJOR REVISION/REJECT decision. See `neurips-scoring.md`.
- **Every gate has a reviewer.** Each gate is owned by a named Council seat accountable for that failure mode, so no failure mode is anyone's spare-time job. The full roster is in [The Council](#the-council) below.
- **Two stances.** A *gatekeeper* stance for pre-submission ("tear it apart") and a *development* stance that keeps the rigor but adds generative paper-writing feedback: an exposition/argument-chain pass, generative figure feedback, and a Reviewer-2 pre-mortem that pre-loads the objections a hostile reviewer will raise. See `paper-development.md`.
- Returns a decision (ACCEPT, MAJOR REVISION, or REJECT), a severity-ranked list of findings, and the single highest-leverage change that would move the work up one level.
- **Self-calibrates.** Every finding carries an explicit confidence and abstains (rather than guessing a severity) when the artifact is evidence-blocked; the Council runs a self-guard against its own reviewer biases (anchoring, halo, confirmation, severity inflation); the single load-bearing finding behind a REJECT/MAJOR REVISION is verified before it's allowed to drive the verdict; and a final coherence pass reconciles the gate ladder, Claim Ledger, Council objections, and verdict before output.
- **Scales to the ask.** Quick / Standard / Deep review scopes trade breadth and orchestration for speed without relaxing empirical rigor, and a conditional Gate T (theoretical soundness) fires for formal/mathematical claims.
- **Portable beyond in-silico neuro/AI.** The gate ladder maps onto non in-silico reporting standards - CONSORT, STROBE, PRISMA, ARRIVE, and general clinical-trial hooks - via `references/domain-adaptation.md`, so a clinical, biomedical, or observational study can be reviewed with the same ladder.

## The Council

A lone reviewer has blind spots: they wave through an overclaim because the method is elegant, or forget to check confounds when the stats look clean. The Council fixes this by making each failure mode *someone's* named responsibility. Every gate is ruled by one seat who is relentless about that one thing, so a study is covered end to end and nothing falls through the gaps between reviewers.

**Standing panel** (sits on every review):

| Seat | Rules over | Why that gate matters |
|---|---|---|
| **Elrond** — Convener & Statistician | **Gate T** (theoretical soundness) · **Gate S** (venue scoring) · verdict synthesis | Aggregates every seat's objection into the ACCEPT/MAJOR REVISION/REJECT decision, checks the statistics under it, validates any formal/mathematical claim, and — when a venue is named — translates the verdict onto the NeurIPS five-axis score. A wrong synthesis or an ungrounded score is the review's own failure. |
| **Gandalf** — Replication Skeptic | **Gate 1** (variance) · **Gate 2** (specification robustness) | The most common way a finding is fake: a dramatic single run that is really seed variance, or a result that lives at exactly one hyperparameter. If it does not survive twenty seeds and a sweep of reasonable choices, it is noise in a costume. |
| **Aragorn** — Provenance Auditor | **Gate 0** (provenance, leakage, baselines) | If the ground is not real, nothing above it can be. Synthetic data read as biology, test-set leakage, or a score with no chance baseline makes every downstream gate moot — which is why Gate 0 is terminal. |
| **Galadriel** — Construct & Measurement Validity | **Gate 4** (confounds) · **Gate 8** (measurement validity & reliability) | A metric that measures a convenient proxy instead of the named construct, or an effect that is really an effect of size/length/frequency, produces a "result" about the wrong thing. If the instrument is unreliable, the effect may be noise it lets through. |
| **Boromir** — Overclaim Sentinel | **Gate 6** (claim calibration) | The gap between what was shown and what is said is where papers die in review. "Causes/drives/enables" needs intervention, not correlation; in-silico is not in-vivo. Language must never exceed the evidence tier. |
| **Gimli** — Single-Instrument Devil's Advocate | **Gate 3** (specificity) · **Gate 5** (mechanism / necessity) | Strip away the favorite model, dataset, or metric: does the finding stand? Is the *named* mechanism specifically responsible, or would any generic alternative do as well — and does it actually carry the functional load, or is it present-but-redundant under ablation? |
| **Legolas** — Literature Anchor | novelty & citation integrity (feeds the Contribution axis of Gate S) | A rediscovery dressed as a first, or citations that do not say what they are claimed to say, sinks a contribution regardless of how sound the method is. Legolas checks prior art by actually searching, not asserting from memory. |
| **Samwise** — Figure & Exposition Auditor | **Gate F** (figure integrity, fires only when figures are present) | Figures are where encoding quietly lies — truncated axes, missing error bars, a hand-picked example narrated as typical. A figure that contradicts a central claim is a Blocker. On text-only work he runs the exposition/argument-chain pass instead. |

**Specialist seats** (convene when the design invites them):

| Seat | Rules over | Why that gate matters |
|---|---|---|
| **Faramir** — External Validity | **Gate 7** (generalization, boundary conditions) | "Generalizes" claimed from one dataset/model/site, or a convenience sample the claim silently outgrows, breaks the moment it meets the far shore. Faramir demands the OOD or transfer test behind a general claim. |
| **Eowyn** — Reproducibility & Open Science | **Gate 9** (reproducibility, computational provenance) | A result no independent party can re-run is a rumor. Seeds, configs, exact splits, code, environment, and compute must be released so "better" is separable from "bigger budget." |
| **Bilbo** — Preregistration & Analytic Integrity | **Gate 11** (confirmatory vs exploratory, HARKing, forking paths) | An exploratory finding narrated as an a priori prediction is a false confirmatory claim. Bilbo checks whether the analysis was specified before the data spoke, or the map was drawn after the treasure was found. |
| **Treebeard** — Ethics, Safety & Responsible Disclosure | **Gate 10** (ethics, safety, dual-use, broader impact, fairness) | Consent/IRB gaps, unaddressed licensing/PII, or a misuse-capable capability released without a disclosure thought can be terminal on their own, independent of technical quality — a sound method done irresponsibly is still a reject. |

Full seat charge sheets — each seat's questions, tells, and signature line — are in [`references/council-seats.md`](plugins/council-review/skills/council-review/references/council-seats.md).

## Data & grounding

The gate ladder encodes empirical failure modes that have sunk real in-silico studies: single-run "improvements" that were seed variance, cross-system correlations that were scale-confounded, components that were functionally redundant under ablation, and synthetic-data pilots that "fingerprinted" random seeds rather than biology. No external dataset is required; it operates on whatever artifact you give it.

## License

MIT - see [LICENSE](LICENSE).
