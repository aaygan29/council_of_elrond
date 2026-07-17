# council_of_elrond

An empirical, adversarial research-review tool for Claude. It convenes a fixed panel of skeptics and withholds a verdict until the work has survived a hard empirical gate ladder, so a weak finding can fail here, in private, rather than later.

## What it does

- Works on two kinds of input:
  - **Manuscripts / write-ups** (Markdown, PDF, DOCX): drafts, proposals, preregistrations.
  - **Live artifacts** (code, results files, notebooks, statistical output): recomputes headline numbers from the source files instead of trusting the prose. A number in the text that disagrees with its source file is flagged.
- Returns a decision (ACCEPT, MAJOR REVISION, or REJECT), a severity-ranked list of findings, and the single highest-leverage change that would move the work up one level.

## Data & grounding

The gate ladder encodes empirical failure modes that have sunk real in-silico studies: single-run "improvements" that were seed variance, cross-system correlations that were scale-confounded, components that were functionally redundant under ablation, and synthetic-data pilots that "fingerprinted" random seeds rather than biology. No external dataset is required; it operates on whatever artifact you give it.

## License

MIT — see [LICENSE](LICENSE).
