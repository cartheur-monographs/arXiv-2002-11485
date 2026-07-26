# arXiv v.2 Submission Bundle

This directory contains the `v.2` arXiv submission materials for the
revised `arXiv-2002-11485` paper.

Working title:

- `A machine-learning software-systems approach to capture social, regulatory, governance, and climate problems`

## Primary files

- `main.tex`: LaTeX source for the paper prepared for arXiv upload
- `main.pdf`: locally compiled reference PDF for visual comparison

## Local build

```bash
cd arxiv/v.2
pdflatex -interaction=nonstopmode -halt-on-error main.tex
pdflatex -interaction=nonstopmode -halt-on-error main.tex
```

## Submission package

For arXiv submission, upload source rather than PDF-only.

Current source bundle:

- `main.tex`

This paper currently uses an inline bibliography rather than a separate
`.bib` database, so no `references.bib` or `.bbl` file is required for the
submission source set.

The local `main.pdf` should be treated as a comparison artifact, not the
upload format.

Prepared source archive:

- `../2002.11485v2-arxiv.tar.gz`

That archive currently contains the arXiv upload source set for this revision.

## Recommended arXiv metadata

Primary category:

- `cs.CY`

Reason:

- The manuscript focuses on governance, coordination, cybernetics, and the
  structure of advisory systems in complex social and institutional settings.

Secondary category:

- `cs.AI`

Reason:

- The paper also argues for a layered advisory architecture involving
  Bayesian inference, intervention analysis, and counterfactual reasoning.

Optional alternative secondary:

- `stat.ML` if a later revision becomes substantially more formal on the
  probabilistic side.

Recommended license:

- `arXiv.org perpetual, non-exclusive license 1.0`

Why:

- This is the safest default if later journal submission is likely, because
  it keeps the preprint available on arXiv while minimizing reuse
  complications.

Alternative:

- `CC BY 4.0` if broad reuse is desired and the eventual journal clearly
  permits preprints under that license.

Comments field draft:

- `11 pages. Position paper with a formal systems sketch.`

Keywords for internal tracking:

- `governance, cybernetics, CyberSyn, Bayesian inference, causal reasoning, counterfactuals, policy intelligence`

## arXiv submission requirements

- Upload source rather than PDF-only submission for this LaTeX manuscript.
- arXiv prefers `(La)TeX, AMS(La)TeX, PDFLaTeX`.
- arXiv does not accept a PDF generated from TeX as the submitted source
  format.
- If the submitter is new to arXiv or new to the chosen category,
  endorsement may be required.
- The selected license is irrevocable for that version.

## Submission checklist

1. Confirm the final title, author name, contact email, and ORCID.
2. Confirm the abstract in `main.tex` is the one to submit.
3. Confirm the chosen primary category is `cs.CY` or adjust it if the paper
   is reframed before submission.
4. Confirm whether endorsement is needed for the submitting author.
5. Upload LaTeX source rather than PDF-only.
6. Preview arXiv's compiled PDF and compare it against local `main.pdf`.
7. Verify references, title metadata, and abstract metadata before final submission.
8. Re-check journal preprint compatibility on the day of submission if a journal target is already preferred.

## Notes on local artifacts

The files `main.aux`, `main.log`, and `main.out` are local build artifacts.
They are useful for compilation and troubleshooting, but they are not part of
the paper's intellectual content.
