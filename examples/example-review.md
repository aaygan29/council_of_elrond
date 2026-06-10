# Example: a Council Review in full

This is an illustrative sample on a fictional manuscript, included so you can see the output format and the level of scrutiny. The study, numbers, and author are invented.

---

**Target:** *"Sparse Autoencoder Features Align with Human Visual Cortex, Demonstrating Emergent Brain-Like Semantics in Vision Transformers"* (draft.md), with code in `./study/` and results in `./study/results/rsa.json`.

**Mode:** Manuscript plus live artifacts.

---

# Council Review: Sparse Autoencoder Features Align with Human Visual Cortex

## Verdict: MAJOR REVISION

The core observation (SAE features correlate with fMRI responses in a ventral-stream ROI) appears real and the analysis pipeline runs, but the central claim outruns the evidence on three fronts: the headline RSA value comes from a single model checkpoint with no variance estimate, the correlation is not controlled for the most obvious confound (low-level image statistics), and the word "demonstrating" promises a causal, mechanistic result the design cannot deliver. None of these is fatal, so this is a revision rather than a rejection, but the causal framing is a Blocker for the abstract as written.

## Claim Ledger
| # | Claim (as stated) | Asserted tier | Actual tier | Decisive gate |
|---|-------------------|---------------|-------------|---------------|
| 1 | "SAE features align with human visual cortex" | T3 | T2 (single checkpoint, no CI) | Gate 1 |
| 2 | "demonstrating emergent brain-like semantics" | T5 (mechanistic) | T2 (correlational) | Gate 6 |
| 3 | "alignment is specific to semantic features, not low-level structure" | T4 | T1 (untested) | Gate 4 |

## Gate Ladder
- Gate 0 Provenance ........... PASS. Real fMRI (NSD subset), fixed train/test split declared in `data_loader.py:41`, noise ceiling reported. No leakage found in the feature-selection step.
- Gate 1 Variance ............. FAIL. Headline RSA rho = 0.31 comes from one model checkpoint and one random seed. No CI, no across-seed or across-subject spread reported. Recomputed from `rsa.json`: the per-subject values range 0.12 to 0.44, so the single reported 0.31 hides substantial spread.
- Gate 2 Spec robustness ...... PARTIAL. Result holds at the one RSA distance metric used (correlation distance); not tested under Euclidean or cosine. ROI definition is single-atlas.
- Gate 3 Specificity .......... UNTESTED. No comparison against a non-semantic feature set of equal dimensionality.
- Gate 4 Confound ............. FAIL. No control for low-level image statistics (luminance, spatial frequency, contrast), which co-vary with both SAE activations and early-visual fMRI responses. The "semantic" interpretation is not separable from a low-level account on the current evidence.
- Gate 5 Necessity ............ N/A. Correlational design; no intervention claimed. Acceptable, but see Gate 6.
- Gate 6 Claim calibration .... FAIL (Blocker). "Demonstrating emergent brain-like semantics" is a mechanistic, causal claim resting on a single correlational RSA value.

## Council Objections
- **Elrond (stats):** A single rho with no interval is not a result, it is a point. Report a bootstrap CI across subjects and the noise-ceiling-normalized value. [Major]
- **Gandalf (replication):** One checkpoint, one seed. Re-run across at least five seeds and report the spread before any "alignment" claim. [Major]
- **Aragorn (provenance):** Clean. Split is fixed, ceiling is present, no leakage. No objection.
- **Galadriel (construct validity):** "Semantic" is the entire load-bearing word and it is never operationalized against a low-level baseline. What is the partial RSA after regressing out luminance and spatial frequency? [Blocker]
- **Boromir (overclaim):** "Demonstrating emergent brain-like semantics" from rho = 0.31 is the claim outrunning the data by two tiers. Retract to "is consistent with." [Blocker]
- **Gimli (single-instrument):** One model family, one atlas, one distance metric, one dataset. Does a second ViT family reproduce it? [Major]
- **Legolas (literature):** The "first to show" framing needs a check against the existing model-to-brain RSA literature, which is large. [Minor, needs lookup]

## Severity-ranked findings
1. [Blocker] Causal language on correlational evidence (abstract and title). Fix: replace "demonstrating emergent brain-like semantics" with "is consistent with semantic alignment."
2. [Blocker] No confound control for low-level image statistics. Fix: report partial RSA controlling for luminance, contrast, and spatial frequency. If the effect survives, the semantic claim is earned; if not, it is reframed.
3. [Major] Single checkpoint and seed. Fix: five or more seeds, bootstrap CI, noise-ceiling normalization.
4. [Major] Single-instrument. Fix: replicate on a second model family.
5. [Minor] Untested distance metrics and atlas; novelty claim needs a literature check.

## What would change the verdict
Add the partial RSA controlling for low-level image statistics (finding 2). That one analysis, with no new data collection, settles whether the alignment is semantic or low-level, and it is the hinge the entire contribution turns on. Pair it with a five-seed spread and a recalibrated abstract, and this moves toward ACCEPT.

## Evidence log
- `study/results/rsa.json`: reported rho = 0.31; recomputed per-subject range 0.12 to 0.44 (n = 8); noise ceiling 0.39.
- `study/data_loader.py:41`: fixed train/test split confirmed.
- Abstract, sentence 1: "demonstrating emergent brain-like semantics" (causal verb on correlational design).
- No covariate file for low-level image statistics found in `study/`; confound control is absent, not merely unreported.
