# Reviewer Responses (working notes)

Working notes supporting `reviewer_response.tex` (the to-be-submitted reply) and `REVISIONS.md` (the revision to-do list). The `.tex` file contains only dialog addressing reviewer concerns or describing changes already made to the manuscript; anything speculative, planned, or "in preparation" lives here.

Note: large manuscript additions are color-coded blue; small changes are logged in `CHANGES.md`.

---

## Pending work ported out of `reviewer_response.tex`

These statements were removed from the submission copy so that it strictly reflects completed changes. They remain tracked here for coauthor discussion and future revisions.

- **Simulated-curve Type I / power study.** (REVISIONS item 9; R1.5)
  Synthetic ensembles with controlled $(\boldsymbol{t},\boldsymbol{\ell})$ differences; sweep effect size; report empirical Type I at the null and power on the alternative. One table plus one small figure panel in §`sec:experiments`. Current reply R1.5 in the `.tex` file cites decision-landscape ambiguity as empirical stability evidence; the simulated-curve table would formalize it.

- **Clustering-within-an-image demonstration.** (REVISIONS item 8; R4.2, R4.3)
  Optional upgrade: short demo of clustering over $(\boldsymbol{t},\boldsymbol{\ell})$ features within a single image. An optional placeholder for this still exists at line ~1036 of `sn-article-revised.tex`. Minimal-effort path: delete the placeholder.

- **Speculative additional demonstrations (shelved for this submission).** (R4.3)
  Removed from R4.3 reply: a SUVI solar-ultraviolet clustering demonstration (clustering over $(\boldsymbol{t},\boldsymbol{\ell})$ within a single image), a pairwise MNIST digit-classification experiment, and a curve-comparison evaluation along the lines of Kaltenmark et al. (2017). These were not ready for inclusion and the reply now points instead to the already-promoted non-EBSD lithium-ion battery SEM study in §`sec:intro` and §`sec:experiments`.

---

## Reviewer 1

### R1.1 — Notation and illustrations (Sections 2–3)
> cumbersome to read due to heavy notation and lack of illustrations

**Status:** Done. Lemma/theorem reformatting, CLO/PRRTI definitions, appendix relocation, and three new illustrations (Figure 3 = piecewise-linear polygon undulation schematic in §`subsec:geo_interp`; Figure 4 = SRQD; Figure 8 = pipeline diagram) are all in place.

### R1.2 — Terminology ("classification" vs. hypothesis testing; Table 1 "Accept" → "FTR")
**Status:** Done. Blue text in §`sec:intro` and §`subsec:MMD` formalizes the binary mapping $H$; Table 1 and adjacent text use "FTR."

### R1.3 — Cyclic Procrustes: random template vs. Fréchet mean
**Status:** Done. Blue-text justification in §`subsec:cycl_Pro` after Theorem~\ref{thm:cycl_Procrustes}.

### R1.4 — MMD test details (permutations, p-value, Procrustes within permutations)
**Status:** Done. Blue text in §`subsec:MMD` specifies biased $\widehat{\mathrm{MMD}}^2$ estimator, Gaussian RBF with median heuristic, $B=1000$ sample permutations, and Bonferroni-adjusted rejection; explicitly separates row-level cyclic Procrustes permutation from ensemble-label sample permutation.

### R1.5 — Simulations (Type I error and power)
**Status:** Pending (REVISIONS item 9). Decision-landscape ambiguity is the currently reported empirical-stability proxy.

### R1.6 — Computational cost
**Status:** Done (REVISIONS item 10). New Subsection 4.3 ``Timings'' contains Table~\ref{tab:timing} with sequential wall-clock entries for cyclic Procrustes, SRQD, tPCA, and $B=1000$-permutation pMMD over $N\in\{100,\dots,2000\}$; a summary row reports the empirical scaling exponent $\widehat{\eta}$. Discussion paragraph partitions stages into embarrassingly-parallel (per-curve, pMMD permutations) versus intrinsically-sequential (tPCA Karcher reduction), quantifies a Numba parallel-JIT speedup that removes pMMD from the critical path, and cites an independent MATLAB R2024b \texttt{parfor} run on a separate workstation as a $\sim 50\times$ demonstration of SRQD acceleration headroom.

---

## Reviewer 2

### R2.1 — Separability assumption (undulation vs. scale independence)
**Status:** Done. Blue text in §`subsec:MMD` clarifies separability is an algebraic decomposition distinct from statistical independence, and sketches an HSIC-style diagnostic.

### R2.2 — Terminology ("explainable binary classification")
**Status:** Done. See R1.2.

### R2.3 — Statistical detail (non-parametric two-sample test procedure)
**Status:** Done. See R1.4.

### R2.4 — Multiple testing (joint product-MMD Type I error)
**Status:** Done. Bonferroni paragraph added in §`subsec:MMD` with De Morgan (logical) vs Bonferroni (statistical) compatibility note.

### R2.5 — Selecting r, n
**Status:** Done. Blue text at the start of the decision-landscape discussion in §`sec:experiments`: $n\in[100,500]$ by Nyström spectral convergence; $r$ selected via ambiguity metric~\eqref{eq:ambiguity} beyond the ambiguity peak.

### R2.6 — Writing and organization (contributions buried, background too long)
**Status:** Done. `[prior art]`/`[new]` contribution bullets, SST-background relocation to Appendix~A, concision pass, and the new undulation-vs-scale schematic (Figure 3, §`subsec:geo_interp`) are all in place.

### R2.7 — Undulation-vs-scale illustration
**Status:** Done (REVISIONS item 6). New Figure 3 (`fig:PL_SST` in §`subsec:geo_interp`) shows piecewise-linear polygons with identical generalized scales but increasing face count, alongside their orthonormal eigenfunctions.

### R2.8 — Typo: "it sufficient"
**Status:** Done. See `CHANGES.md`.

---

## Reviewer 3

### R3.1 — Formalize lemma/theorem statements
**Status:** Done.

### R3.2 — Definition environments for CLO and PRRTI
**Status:** Done.

### R3.3 — Acronyms not introduced on first use (SST, HS)
**Status:** Done.

### R3.4 — Typos and grammar
**Status:** Done. See `CHANGES.md`.

---

## Reviewer 4

### R4.1 — Presentation quality (overcomplicated, missing visualizations)
**Status:** Done. Appendix relocation, three new figures (Figures 3, 4, 8 — undulation schematic, SRQD, pipeline), CLO/PRRTI definitions, expanded Notation subsection, `\mathcal{C}_d` defined at `eq:reg_Hilbert_space`, and concision pass are all complete.

### R4.2 — Problem statement unclear; why not clustering?
**Status:** Done. Problem Statement subsection plus blue-text paragraphs formalizing hypothesis testing as a binary decision rule; R4.2 reply now notes the $(\boldsymbol{t},\boldsymbol{\ell})$ feature space supports clustering when that is the downstream objective (without forward-referencing a planned demo).

### R4.3 — Evaluation limited to EBSD
**Status:** Done. Non-EBSD lithium-ion battery SEM study is now promoted in the §`sec:intro` Contributions bullet and developed in §`sec:experiments` ("Segmentation Efficacy"). Speculative SUVI/MNIST/Kaltenmark promises removed from the `.tex` reply (see Pending work).

### R4.4 — Pipeline algorithm figure
**Status:** Done. `fig:placeholder` in §`subsec:mfld_learn` renders `pipeline_diagram.tex`; a concise `algorithm` block (Algorithm~\ref{alg:pipeline}, `algo.tex`) has been placed at the end of §`subsec:MMD` stating the full pipeline as pseudocode in manuscript notation with section cross-references.

### R4.5 — Interpretability claims not demonstrated; AI methods not cited or compared
**Status:** Done. Truth-table walkthrough in §`sec:experiments` and varifold/Sobolev/deep-learning comparison in the §`sec:intro` contributions discussion.

### R4.6 — Missing/wrong references [1]–[5]
**Status:** Done. All five references added with sn-aps formatting; Kaltenmark et al. (2017) replaces the prior incorrect varifold citation. See `CHANGES.md`.

### R4.7 — Conclusion: rejection
No action required beyond the substantive revisions above.
