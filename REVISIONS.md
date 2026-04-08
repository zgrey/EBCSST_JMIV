# Revision To-Do List

Items sorted by estimated effort (low to high). Types: **D** = document edits, **W** = written response only, **N** = numerical experiment.

## Completed

1. ZG [x] **[D] Insert missing references [1]--[5]** (R4)
   Add the cited works to the bibliography with correct formatting and cross-referencing. Verify the cited works are 1) in the body of the text and 2) are actually cited correctly.

2. ZG [x] **[D] Correct typos, grammar, and word-choice errors throughout** (R2, R3)
   Full copy-editing pass: fix "it sufficient" → "it is sufficient", "elude" → "allude", difficult-to-parse sentences, and similar issues. Detailed changes documented in CHANGES.md.

3. ZG [x] **[D] Introduce all acronyms on first use (SST, HS, CLO, PRRTI, etc.)** (R3)
   Define each acronym at its first occurrence. Use LaTeX definition environments for CLO and PRRTI.

4. ZG [x] **[D] Formalize statements of lemmas, theorems, and definitions** (R3)
   Rewrite Lemma 1, Lemma 3, and Theorem 1 in standard formal style ("Let c in C_d, then ..."). Fix Lemma 2 wording (use \coloneqq notation). Number all definitions and use definition environments.

5. ZG [x] **[D] Revise abstract and add hypothesis-testing vs. clustering justification** (R1, R2, R4)
   Revised abstract to foreground statistical comparison / hypothesis-testing contribution while preserving "explainable binary classification" framing. Added paragraph in Sec. 1.1 justifying hypothesis testing over clustering.

## Low effort

6. ZG [x] **[D] Justify hypothesis testing as explainable binary classification** (R1, R2, R4)
   Write a technical justification in Sec. 3.5 that two-sample hypothesis testing constitutes a binary classification: the test maps pairs of distributions to {reject, FTR}. Connect to the title; distinguish from supervised-learning classification.

   **Status**: Complete. Intro-level framing in Sec. 1.1 (blue text) and formal justification in Sec. 3.5 (blue text) mirroring the same notation.

7. ZG [x] **[W] Discuss separability assumption; propose a diagnostic for violations** (R2)
   Separability does not imply independence. MMD can test independence (see Gretton et al.). Add clarification that separability is not independence.

8. [x] **[D/W] Demonstrate interpretability and compare with AI/varifold methods** (R4)
   Show how extracted shape features correspond to physical differences. Qualitative comparison with varifold methods (Kaltenmark 2017, Bauer 2017) and deep learning (Hartman 2023, Hartman 2021, Pierson 2022).

   **Plan**: Citations added. Section 2.2 discusses an extensive example. No exhaustive comparison since methods use distinct representations.

9. [x] **[W] Justify random Procrustes template over Fréchet mean** (R1, R4)
   Justify adequacy, sensitivity analysis, and computational trade-offs.

   **Plan**: Can't replace Procrustes template with Fréchet mean (Fréchet mean comes after registration). Clarify via Item 13 diagrams. Justify uniqueness via Figs. 8–9 and 5 (stability argument).

## Medium effort

10. AG [ ] **[D] Restructure manuscript: foreground contributions, improve concision** (R2)
    Clearly delineate which results are from prior work (G2Aero, Grey 2023) versus new to this manuscript in Sec. 1.3. Incorporate concision edits throughout. Argue against large-scale restructuring unless explicitly requested by the editor.

11. ZG [ ] **[D] Detail MMD hypothesis-test procedure and multiple-testing correction** (R1, R2, R4)
    Specify: number of permutations (1000, over ensemble not landmarks), kernel choice (Gaussian RBF, universality), permutation scheme, p-value formula, and role of pre-registration (cyclic Procrustes applied once beforehand). Discuss Type I error inflation for joint product-MMD; apply Bonferroni correction ($\alpha/2$). Reconcile with De Morgan equivalence.

12. ZG [ ] **[D] Provide guidelines for selecting r and n** (R2)
    Offer criteria (cumulative variance threshold, MMD stability) for choosing retained dimensions $r$ and quadrature nodes $n$. Decision landscapes are the primary mechanism. Clarify existing discussion with Figs. 8–9 (smoothing study). Consider supplemental experiment.

## High effort

13. ZG [ ] **[D] Simplify notation in Sections 2–3 and add illustrative figures** (R1, R3, R4)
    Reduce heavy notation. Add diagrams: (a) landmark representation and registration, (b) manifold feature spaces, (c) nonlinear undulation vs. linear scale schematic (R2). Add pipeline algorithm figure---flowchart or pseudocode (R4).

    **Plan**: TikZ diagram designed. Will create visualizations of curves moving through the pipeline. Add pseudocode algorithm.

14. [ ] **[W/N] Simulated-data study and computational cost** (R1, R2, R4)
    Generate synthetic curve ensembles to evaluate Type I error and power. Report runtime per pipeline stage in a table.

    **Plan**: Determine if Type I/power is already addressed by the smoothing study (Figs. 8–9). Report runtimes for a standard laptop build.

15. [ ] **[D/N] Non-EBSD evaluation and benchmark comparison** (R1, R4)
    Expand evaluation beyond EBSD. R4 specifically requests broader datasets.

    **Plan** (pending coauthor review):
    - SUVI sun image clustering: demonstrate clustering over proposed features within a single image
    - MNIST pairwise digit classification: demonstrate a supervised classification task
    - Discuss including existing battery results more prominently (Sec. 4.2) since these already extend beyond EBSD

## Reviewer cross-reference

| Reviewer | Points | To-do items |
|----------|--------|-------------|
| R1 | 6 | 5, 6, 9, 11, 13, 14 |
| R2 | 8 | 2, 5, 6, 7, 10, 11, 12, 13 |
| R3 | 4 | 2, 3, 4, 13 |
| R4 | 7 | 1, 5, 6, 8, 10, 13, 15 |
