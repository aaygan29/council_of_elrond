---
name: council-review
description: >-
  Empirical, adversarial research review. Convenes a "Council of Elrond" - a
  standing panel of skeptical reviewers - and judges a scientific work against a
  hard empirical gate ladder (provenance/leakage, seed-variance, specification
  robustness, specificity ablation, confound control, mechanism/necessity, claim
  calibration). Reviews BOTH manuscripts (papers, proposals, preregistrations,
  drafts in md/pdf/docx) AND live artifacts (code, results JSON, statistical
  output). Emits an ACCEPT / MAJOR REVISION / REJECT decision plus
  severity-ranked findings and the single experiment that would change the
  verdict. Use this whenever the user wants a rigorous critique of a paper,
  proposal, experiment, result, or claim - especially in-silico neuro/AI work -
  or asks any of: "is this finding real?", "would this survive more seeds?",
  "am I overclaiming?", "is this publishable?", "tear this apart", "review my
  results", "is my method sound?", "what's wrong with this experiment?". Trigger
  even when the user doesn't say the word "review" but is clearly asking for
  empirical scrutiny of a scientific claim or artifact.
---

# Council Review

## What this is

A scientific work is only as strong as the worst objection it survives. This skill
stops you from being a polite reviewer. It convenes the **Council of Elrond** - a
fixed panel of skeptics who each attack from one angle - and forces the work
through an **empirical gate ladder** before any verdict is allowed.

The gates are not generic peer-review etiquette. They encode the empirical
discipline that has actually killed real findings in this user's own work:

- A headline single-run improvement that turned out to be **seed variance**
  (Cohen's *d* = -1.20 across 20 seeds once tested properly).
- A correlation that was **real but scale-confounded** (raw p = -0.83, *p* = .04;
  partial correlation controlling for log-params p = -0.67, *p* = .14, NS).
- A "brain-like" component that was present but **functionally redundant** under
  ablation (8.6x less load-bearing than the components doing the actual work).
- A synthetic-data pilot that fingerprinted "subjects" perfectly because they
  were different random seeds, archived forever as `DO_NOT_CITE`.

The Council exists so that the work being reviewed dies *here*, in private, rather
than in front of a NeurIPS reviewer or - worse - after publication.

## When to use it

Use it whenever the user wants empirical scrutiny of a scientific claim or
artifact: reviewing a paper/proposal/preregistration, auditing their own results
before submission, deciding whether a finding is real, checking whether an
abstract overclaims, or pressure-testing a method. It works on external papers
*and* on the user's own running experiments.

It is domain-tuned for in-silico neuroscience / neuro-AI (encoding models, RSA,
attention-topology, fMRI alignment, manipulation/footprint metrics) but the gate
ladder is general to any quantitative empirical claim.

## How to run a review

### 1. Establish the target and mode

Identify what you're reviewing and in which mode:

- **Manuscript mode** - a paper, proposal, preregistration, or draft. Read it
  fully. Extract the *central claims* (what the abstract/contributions assert),
  not just the prose.
- **Artifact mode** - a repo, results JSON, notebook, or stats output. Open the
  actual numbers. Do not trust the prose summary of a result you can recompute.
- **Both** (most powerful) - a manuscript *with* its code/results present.
  Cross-check every headline number in the text against the artifact that
  produced it. Mismatches are findings.

State the mode and list the central claims before judging anything. A review that
hasn't named the claims is just vibes.

### 2. Build the Claim Ledger

For each central claim, record: the claim as stated, the **evidence tier** it
actually rests on, and which gates it must pass. Evidence tiers, weakest to
strongest:

| Tier | Description |
|---|---|
| T0 | Assertion / intuition, no evidence |
| T1 | Single run / anecdote / illustrative example |
| T2 | Descriptive statistic, no inference (means, single *p*) |
| T3 | Inferential with effect size + CI, but no robustness/confound control |
| T4 | Robust: multi-seed, confound-controlled, specificity-tested |
| T5 | Mechanistic: necessity established (ablation/lesion), pre-registered confirmatory |

A claim's language must not exceed its tier. "X causes Y" on T3 evidence is an
overclaim finding, full stop.

### 3. Walk the gate ladder

Run every claim through the gates **in order**. Read
`references/empirical-gates.md` for the full definition, worked examples, and the
exact statistical checks each gate demands. The ladder in brief:

- **Gate 0 - Provenance & Integrity.** Is the data real (not synthetic stand-in)?
  Any train/test leakage? Is the split fixed and honest? Is a noise ceiling /
  chance baseline established? A failure here is terminal. → **REJECT** if it fails.
- **Gate 1 - Variance / Replication.** Is the headline from one run or many seeds?
  Effect size *and* CI reported, not *p* alone? Could this be seed variance?
- **Gate 2 - Specification Robustness.** Does it survive reasonable analytic
  choices (thresholds, preprocessing, hyperparameters)? Or is it knife-edge?
- **Gate 3 - Specificity.** Is the *named* mechanism specifically responsible, or
  would a generic alternative of equal strength do as well? (The ablation test.)
- **Gate 4 - Confound Control.** Does the effect survive controlling for the
  obvious confounds (scale/size, length, surprisal, base rate)?
- **Gate 5 - Mechanism / Necessity.** Is there a necessity test? Does the proposed
  driver actually carry the functional load, or is it present-but-redundant?
- **Gate 6 - Claim Calibration.** Does each claim's language match its evidence
  tier? In-silico is not in-vivo. Correlational is not causal.

Mark each gate **PASS / FAIL / N/A** with the specific evidence (a recomputed
number, a `file:line`, a quote).

### 4. Convene the Council

Each seat attacks from one fixed angle. The full charge sheet is in
`references/council-seats.md`. The panel:

1. **Elrond - Convener & Statistician.** Verdict synthesis and statistical rigor.
2. **Gandalf - Replication Skeptic.** "Would this survive 20 seeds?"
3. **Aragorn - Provenance Auditor.** "Is this data real? Where is the noise ceiling?"
4. **Galadriel - Construct Validity.** "Does the metric measure what it claims?"
5. **Boromir - Overclaim Sentinel.** "Where did the claim outrun the data?"
6. **Gimli - Single-Instrument Devil's Advocate.** "Strip the favorite instrument. Does the finding stand?"
7. **Legolas - Literature Anchor.** "Is this novel? Do citations support the sentences they attach to?"

### 5. Orchestrate supporting skills

See `references/orchestration.md` for the routing table. In short:

- Novelty / prior-art → `literature-review` or `deep-research`
- Biomedical claims, citation verification → `pubmed-database`
- Scholarly-writing quality → `scholar-evaluation`
- Recomputing code/results → `verification-loop`

### 6. Render the verdict

- **REJECT** - any Gate 0 failure, or the central claim collapses below what it asserts.
- **MAJOR REVISION** - plausibly real but a gate fails fixably.
- **ACCEPT** - all relevant gates pass and every claim's language matches its tier.

Always end with **"What would change the verdict"**: the single most efficient
experiment or edit that moves the work up one decision level.

## Output format

```
# Council Review - <title>

## Verdict: ACCEPT | MAJOR REVISION | REJECT

## Claim Ledger
| # | Claim (as stated) | Asserted tier | Actual tier | Gate status |

## Gate Ladder
- Gate 0 Provenance .......... PASS/FAIL/N/A - <evidence>
- Gate 1 Variance ............ PASS/FAIL/N/A - <evidence>
- Gate 2 Spec Robustness ..... PASS/FAIL/N/A - <evidence>
- Gate 3 Specificity ......... PASS/FAIL/N/A - <evidence>
- Gate 4 Confound Control .... PASS/FAIL/N/A - <evidence>
- Gate 5 Mechanism ........... PASS/FAIL/N/A - <evidence>
- Gate 6 Claim Calibration ... PASS/FAIL/N/A - <evidence>

## Council Objections      (Blocker | Major | Minor | Nit)
- **Elrond (stats):** ...
- **Gandalf (replication):** ...
- **Aragorn (provenance):** ...
- **Galadriel (construct validity):** ...
- **Boromir (overclaim):** ...
- **Gimli (single-instrument):** ...
- **Legolas (literature):** ...

## Severity-ranked findings
1. [Blocker] ... Fix: ...
2. [Major] ...
3. [Minor] ...

## What would change the verdict
<the single highest-leverage experiment / analysis / edit>

## Evidence log
<citations, file:line refs, every recomputed number with its source>
```

## Operating principles

- **Recompute before you trust.** In artifact mode, verify every number you can.
- **Severity honestly.** A Blocker invalidates a central claim. A Nit is cosmetic.
- **Attack the work, support the author.** Every finding pairs with the fix.
- **No verdict without the ladder.** The ladder is the empiricism; the rest is presentation.
