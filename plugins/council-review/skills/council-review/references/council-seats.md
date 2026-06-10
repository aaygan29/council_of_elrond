# The Council of Elrond - seat charge sheets

The Council is a fixed panel. Each seat owns one angle of attack and is
responsible for the failure mode that angle catches. The point of fixed seats is
coverage: a lone reviewer forgets to check confounds when the stats look clean, or
waves through an overclaim because the method is elegant. Seven seats, each
relentless about one thing, leave fewer blind spots.

Give each seat its strongest one or two objections, tagged with severity
(**Blocker** invalidates a central claim · **Major** weakens it · **Minor** should
fix · **Nit** cosmetic). "No objection" is an honest and valuable entry - do not
manufacture complaints, but do not let a seat pass the work without genuinely
trying to break it.

Each seat below: its angle, the questions it asks, the gate(s) it owns, and the
tells it hunts for.

---

## 1. Elrond - Convener & Statistician
**Angle:** statistical validity and final synthesis.
**Owns:** the verdict; cross-cutting stats; Gate 1.
**Asks:**
- Is there an effect size and CI, or just a *p*-value waving its arms?
- How many comparisons were run, and do the "significant" ones survive correction?
- Is the test appropriate for the N and distribution (permutation/bootstrap for
  small or non-normal samples)?
- Is the study powered to detect the claimed effect, or is a null just silence?
**Tells:** bare *p* < .05; "trending toward significance"; uncorrected multiplicity;
N=3 with a parametric test and a confident conclusion.
**Synthesis duty:** after all seats report, Elrond maps objections to gates and
renders ACCEPT / MAJOR REVISION / REJECT. No seat overrides a Gate 0 failure.

---

## 2. Gandalf - Replication Skeptic
**Angle:** would it happen again?
**Owns:** Gates 1-2 (variance, specification robustness).
**Asks:**
- One seed or many? What is the seed-to-seed spread of the baseline?
- Is the headline bigger than that spread, or is it inside the noise?
- Were the decision rules / analysis choices pre-committed, or chosen after the
  data spoke?
- Does the effect survive a reasonable sweep of thresholds and preprocessing?
**Tells:** N=1 headline; no error bars; a result that lives at exactly one
hyperparameter value; "we found that the best configuration was..." (chosen
post-hoc).
**Signature line:** *"Show me it twenty times. The dramatic single run is almost
always variance wearing a costume."*

---

## 3. Aragorn - Provenance Auditor
**Angle:** is the ground real?
**Owns:** Gate 0 (provenance, leakage, baselines).
**Asks:**
- Is this real data or a synthetic stand-in being read as biology/reality?
- Where could test information have leaked into training, feature selection, or
  tuning?
- Is the split fixed and declared? Can I locate the authoritative results file?
- Where is the noise ceiling / chance baseline this number should be read against?
**Tells:** perfect or near-perfect separation (smells of leakage or artifact);
a decoding/fingerprinting score with no chance line; "results.json" ambiguity
between pilot and final; metrics quoted without a ceiling.
**Signature line:** *"A flawless result on unverified ground is not a triumph, it's
a warning."*

---

## 4. Galadriel - Construct Validity
**Angle:** does the measure mean what its name claims?
**Owns:** Gate 4 (confounds) jointly with Boromir's calibration.
**Asks:**
- Does this metric operationalize the construct, or a convenient proxy that drifts
  from it?
- What third variable co-varies with both axes? (Usually **size**.)
- If you partial out the obvious confound, does the effect survive?
- Is "alignment"/"similarity"/"brain-like" defined precisely enough to be falsified?
**Tells:** raw correlations across systems of different scale; a composite index
whose components aren't validated; "brain-like" used as an adjective with no
operational test; an effect that is really an effect of size/length/frequency.
**Signature line:** *"The mirror shows many things. Be sure you are reading the one
you claim to read."*

---

## 5. Boromir - Overclaim Sentinel
**Angle:** the gap between what was shown and what is said.
**Owns:** Gate 6 (claim calibration).
**Asks:**
- Does the verb match the evidence? "Causes/drives/enables" needs intervention,
  not correlation.
- Is in-silico evidence being narrated as in-vivo fact?
- Is a projected/illustrative scenario stated in the present tense as if
  demonstrated?
- Does the abstract promise what the results actually deliver?
**Tells:** causal language on correlational data; "the brain does X" from "our
network does X"; threat-model scenarios blurred into established fact; an abstract
sentence with no matching results figure/table.
**Signature line:** *"It is a gift to overstate. A gift that costs you the paper.
Say only what you have shown."*

---

## 6. Gimli - Single-Instrument Devil's Advocate
**Angle:** dependence on one favored tool, model, dataset, or metric.
**Owns:** robustness across instruments (supports Gates 2-3).
**Asks:**
- Strip away the signature instrument (the favorite model / dataset / index).
  Does the finding still stand?
- Would a different model family, atlas, corpus, or metric reproduce it?
- Is the conclusion a property of the phenomenon, or of the one tool that measures
  it?
- Is generalization claimed but only single-instrument evidence provided?
**Tells:** every result routed through one instrument; cross-model/dataset
generalization asserted from a single source; a conclusion that would dissolve if
the tool changed.
**Signature line:** *"One axe is loyalty. One axe for every problem is a blind
spot. What does a second instrument say?"*

---

## 7. Legolas - Literature Anchor
**Angle:** novelty and citation integrity.
**Owns:** prior-art and reference verification (orchestrates lookups).
**Asks:**
- Has this been done? Is the contribution actually new, or a rediscovery?
- Does each cited work support the *specific sentence* it's attached to, or is it
  decorative?
- Are there obvious competing results the work ignores?
- Is the framing fair to prior art, or strawmanning it to look novel?
**Tells:** thin related-work; citations that don't say what they're claimed to say;
a "first to show" claim with no search behind it; missing the obvious competing
paper.
**Orchestration:** Legolas is the seat that reaches for `literature-review`,
`deep-research`, or `pubmed-database` (biomedical) to actually check, rather than
asserting novelty from memory.
**Signature line:** *"I see far. Before you call it new, let me look down the road
you think is empty."*

---

## Running the panel efficiently

- You do not need a separate paragraph per seat for a clean work - a seat with no
  objection gets one line. Spend the words where the work is weak.
- If two seats land the same objection (common between Galadriel and Boromir on
  confound-driven overclaims), state it once and attribute jointly.
- The convener (Elrond) speaks last. The verdict is a synthesis of objections
  mapped onto the gate ladder, not a vote count - a single Blocker at Gate 0
  outweighs six clean seats.
