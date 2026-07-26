# Paper Refinement Work Plan

Date: `July 26, 2026`

## Purpose

This work plan sets out how to refine `2002.11485v1.pdf` into a stronger paper while preserving it as an academic or position-paper style artifact rather than allowing it to drift into product, platform, or sales language.

The final target format for the refined paper is `LaTeX (.tex)`, with Markdown drafts used only as intermediate working material.

It is based on:

- [EXTRACTED-PAPER.md](./EXTRACTED-PAPER.md)
- [PAPER-REVISION-NOTES.md](./PAPER-REVISION-NOTES.md)

## Refinement goal

The target is not to turn the current draft into a marketing document or a deployment memo.

The target is to produce a more defensible paper with:

- a narrower and clearer thesis,
- a more scholarly tone,
- a better-structured argument,
- a cleaner mathematical section,
- clearer limits and contribution claims.

## Recommended end state

The strongest end state is:

`a revised position paper with a formal systems sketch`

That means the revised paper should:

- preserve the CyberSyn and causality idea,
- reduce rhetorical overreach,
- clearly distinguish historical grounding from proposed method,
- present the mathematics as a proposed framework unless it is fully derived and validated,
- state its limitations openly,
- and exist as a clean, paper-ready `.tex` manuscript.

## Work streams

There are six work streams that should be carried out in order.

### 1. Thesis and scope correction

Goal:

Reduce the paper from a civilization-scale claim to one argument that can be defended within the available space and evidence.

Tasks:

- choose a single central thesis,
- define what kind of paper this is,
- decide whether the mathematical contribution is formal, preliminary, or illustrative,
- remove claims that cannot be defended in the body.

Success criteria:

- the abstract and introduction make one main claim,
- the conclusion does not outrun the body,
- the paper no longer argues that the proposed system is the only path forward.

### 2. Structural rewrite

Goal:

Rebuild the paper so each section has one job and the reader can follow the argument cleanly.

Tasks:

- rewrite the abstract,
- rewrite the introduction,
- split historical background from normative commentary,
- add a problem formulation section,
- add a limitations and future work section,
- tighten the discussion section.

Recommended section order:

1. Abstract
2. Introduction
3. Historical background: CyberSyn, Beer, viable systems
4. Problem formulation
5. Proposed framework
6. Mathematical sketch
7. Discussion
8. Limitations and future work
9. References

Success criteria:

- each section answers a distinct question,
- the reader can identify the contribution without inference,
- political or ethical commentary appears mainly in discussion and limitations.

### 3. Tone and prose revision

Goal:

Make the paper sound like a serious scholarly document rather than a manifesto.

Tasks:

- replace absolute claims with bounded claims,
- shorten long sentences,
- remove or soften emotionally charged language,
- define technical and abstract terms when first introduced,
- separate descriptive statements from evaluative statements.

Priority phrases to revise:

- "It is a lie."
- "the only solution available to us"
- "survive the coming apocalypse"
- "the only way forward"

Success criteria:

- the paper reads as analytical rather than polemical,
- strong claims are paired with evidence or explicitly marked as conjecture,
- the prose becomes easier to parse at paragraph level.

### 4. Mathematical repair

Goal:

Turn the mathematical section from a suggestive sketch into a disciplined technical section.

Tasks:

- define all variables before using them,
- restate standard Bayesian classification cleanly,
- explain the independence assumption and why it matters,
- introduce Pearl's ladder as a conceptual bridge,
- clarify whether the `do()` notation is formal causal notation or heuristic reuse,
- label the proposed extension as preliminary unless a full derivation is provided,
- ensure every equation is explained in words immediately after it.

Minimum standard for this section:

- notation must be stable,
- symbols must be defined,
- proposed formulas must be framed honestly,
- the reader must know what is standard and what is novel.

Success criteria:

- a technically literate reader can follow the logic,
- the section no longer appears to jump from Bayes to causality without explanation,
- the novelty claim becomes modest and credible.

### 5. Citation and evidence strengthening

Goal:

Make the paper better grounded in cited literature and less dependent on broad assertion.

Tasks:

- add in-text citations where historical claims are made,
- verify the descriptions of CyberSyn and Cyberstride,
- cite Pearl exactly where causal and counterfactual reasoning enter,
- cite Medina where Chilean historical context is described,
- clarify what is drawn from Beer and what is the author's own proposal,
- add a short related-work paragraph if the revised draft allows space.

Success criteria:

- major claims have visible support,
- the paper distinguishes source material from interpretation,
- historical and mathematical claims are better anchored.

### 6. LaTeX manuscript assembly

Goal:

Ensure that the final refined paper exists as a maintainable `.tex` source document rather than stopping at Markdown.

Tasks:

- establish a LaTeX manuscript scaffold early,
- keep section structure synchronized between Markdown working drafts and the `.tex` manuscript,
- normalize equations into LaTeX math form,
- convert tables and references into LaTeX-friendly form,
- reserve a place for figure assets and captions even if figures are still provisional,
- perform a final formatting pass only after the text is substantively stable.

Success criteria:

- the repo contains a canonical `.tex` manuscript source,
- the structure of the paper is represented directly in LaTeX,
- the final revision effort does not end with a Markdown-only draft.

## Suggested execution phases

### Phase 1: Editorial framing

Deliverables:

- revised thesis sentence,
- paper type decision,
- revised section outline,
- list of claims to remove or soften.

Estimated outcome:

This phase determines what the revised paper is allowed to claim.

### Phase 2: Front-half rewrite

Deliverables:

- new abstract,
- new introduction,
- rewritten historical background,
- new problem formulation section.

Estimated outcome:

By the end of this phase, the paper should already read more clearly even before the math section is repaired.

### Phase 3: Technical core rewrite

Deliverables:

- rewritten proposed framework section,
- cleaned mathematical sketch,
- clarified table and figure references.

Estimated outcome:

This phase determines whether the paper feels intellectually coherent rather than merely ambitious.

### Phase 4: Back-half scholarly stabilization

Deliverables:

- revised discussion,
- new limitations and future work section,
- tightened conclusion language,
- improved in-text citations and references.

Estimated outcome:

This phase keeps the paper intellectually honest and prevents overclaiming.

### Phase 5: Final polish

Deliverables:

- paragraph-level copyedit,
- terminology consistency pass,
- citation consistency pass,
- final `.tex` manuscript for review,
- optional generated PDF after the LaTeX manuscript is stabilized.

Estimated outcome:

This phase makes the paper readable, defensible, and presentable.

## Proposed revision principles

During refinement, keep these rules in force:

- Do not add platform branding or go-to-market material.
- Do not convert the argument into a deployment pitch.
- Do not inflate the mathematical novelty.
- Do not remove the historical CyberSyn core.
- Do not claim empirical validation that the draft does not contain.
- Do not suppress limitations merely to sound stronger.

## Risks to manage

### Risk 1: Overcorrection into blandness

If the rhetoric is reduced too aggressively, the paper may lose the distinctive ambition that makes it interesting.

Mitigation:

- preserve the core idea,
- reduce overstatement rather than flattening the thesis.

### Risk 2: Technical overreach remains in place

If the math is not fully derivable, it should not be presented as settled.

Mitigation:

- label it as a proposed framework or sketch,
- state assumptions explicitly.

### Risk 3: Political content dominates the paper

If normative political material remains mixed into the technical sections, readers may stop trusting the analytical portions.

Mitigation:

- move normative implications to discussion and limitations.

### Risk 4: The paper becomes a platform document

Because later materials in adjacent repos are more operational, there is a risk of importing that language into this artifact.

Mitigation:

- keep this document focused on argument, method, and limits,
- leave platform and deployment positioning outside the paper rewrite itself.

## Immediate next actions

The best next sequence is:

1. finalize the revised thesis,
2. approve the new section structure,
3. rewrite the abstract and introduction,
4. then rewrite the mathematical section,
5. then complete discussion, limitations, and citations.

## Practical deliverables for this repo

The refinement effort should produce:

- this work plan,
- the extracted paper text,
- the revision notes,
- a revised paper draft in Markdown for working iteration,
- a canonical LaTeX manuscript,
- optionally a regenerated PDF after the LaTeX text is stabilized.

## Recommendation

Treat the current paper as an ambitious `v1` position draft from `February 23, 2020`, and treat the refinement as a scholarly rewrite rather than an update pass.

That posture will make it easier to produce a serious `v2` paper with a clearer contribution and a more credible technical core.
