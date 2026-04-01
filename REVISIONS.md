# Revision To-Do List

Items sorted by estimated effort (low to high). Types: **D** = document edits, **W** = written response, **N** = numerical experiment.

## Low effort

1. [x] **[D] Insert missing references [1]--[5]** (R4)
   Add the cited works to the bibliography with correct formatting and cross-referencing. Verify the cited works are 1) in the body of the text and 2) are actually cited correctly. Another agent attempted to update the bibitems and I suspect there are errors/bugs. Make sure the new bibitems are formatted consistently versus the other bib items.

2. [ ] **[D] Correct typos, grammar, and word-choice errors throughout** (R2, R3)
   Full copy-editing pass: fix "it sufficient" -> "it is sufficient", "elude" -> "allude", difficult-to-parse sentences, and similar issues. When complete, make a new markdown file summarizing detailed changes to grammar.

3. [ ] **[D] Introduce all acronyms on first use (SST, HS, CLO, PRRTI, etc.)** (R3)
   Define each acronym at its first occurrence. Use LaTeX definition environments for CLO and PRRTI. Double check that SST and HS definitions are defined in the text as well.

4. [ ] **[D] Formalize statements of lemmas, theorems, and definitions** (R3)
   Rewrite Lemma 1, Lemma 3, and Theorem 1 in standard formal style ("Let c in C_d, then ..."). Fix Lemma 2 wording (use `:=` notation). Number all definitions and use definition environments. Note that the LaTeX command used for `:=` notation is \coloneqq

5. [ ] **[D] Revise title, abstract, and hypothesis-testing terminology** (R1, R2, R4)
   - Update title to "Explainable Imaging Discrepancies with Separable Shape Ensembles".
   - Revise abstract to foreground the statistical comparison / hypothesis-testing contribution. However, make a point that hypothesis-testing can be concieved of as a binary mapping from pairs of distributions into a binary conlcusion consistent with the descriptions in section 4.1
   - Add a brief justification for hypothesis testing over clustering (R4 asks why not use clustering given the proposed distance) -> Answer: hypothesis testing offers a binary conclusion while clustering simply aggregates similar features. However, clustering is just as valid an approach to understanding SSTs. An example can be added using the /Git/GitHub/TDA-SST/python/g2_image pipeline with the sun image.

## Medium effort

6. [ ] **[D] Simplify notation in Sections 2--3 and add illustrative figures** (R1, R3, R4)
   Reduce heavy notation to improve readability. Add clear diagrams for: (a) landmark representation and registration, (b) manifold feature spaces, (c) nonlinear undulation vs. linear scale/rotation/shear (the schematic requested by R2). Also add a pipeline algorithm figure (flowchart or pseudocode of the full method, explicitly requested by R4).

7. [ ] **[D] Restructure manuscript: foreground contributions, move background to supplement** (R2)
   Move detailed background (Sections 2--3) to supplementary material. Place core contributions earlier in the main text. Clearly delineate which results are from prior work vs. new to this manuscript (R2 found this hard to distinguish).

8. [ ] **[W] Discuss separability assumption; propose a diagnostic for violations** (R2)
   Analyze whether undulation and scale can be assumed independent in real data. Propose a diagnostic (e.g., correlation analysis of Grassmannian and SPD normal coordinates) to detect violations. Discuss ramifications for tangent PCA and MMD tests.

9. [ ] **[W] Detail the MMD hypothesis-test procedure** (R1, R2, R4)
   Specify: number of permutations, full algorithmic workflow, how cyclic Procrustes is applied within each permutation (R1 notes ensemble changes require re-registration), kernel choice and justification, and p-value computation formula.

10. [ ] **[W] Add multiple-testing correction for joint product-MMD** (R2)
    Discuss Type I error inflation when testing undulation and scale separately. Implement and report a correction (Bonferroni or Holm-Bonferroni) for the joint test. Reconcile with the DeMorgan equivalence argument in Section 3.5.

11. [ ] **[W] Provide guidelines for selecting r and n** (R2)
    Offer criteria (cumulative variance threshold, MMD stability, etc.) for choosing retained dimensions r and quadrature nodes n. Discuss impact on test power, noting that discrepancies may only appear in later dimensions with low variance contribution.

12. [ ] **[W] Replace random Procrustes template with Frechet mean or justify** (R1, R4)
    Implement a Frechet-mean-based template for cyclic Procrustes to improve stability. If retaining the random template, provide detailed justification of adequacy, sensitivity analysis, and computational trade-offs.

## High effort

13. [ ] **[N] Conduct simulated-data study for Type I error and power** (R1, R2)
    Generate synthetic curve ensembles to evaluate the MMD test's Type I error rate and statistical power under controlled conditions.

14. [ ] **[N] Include a non-EBSD dataset or benchmark comparison** (R1, R4)
    Add a comparative experiment on a standard shape dataset (e.g., MPEG-7 or similar to Kaltenmark et al. 2017). R4 specifically requests evaluation beyond EBSD.

15. [ ] **[W/N] Demonstrate interpretability and compare with AI/varifold methods** (R4)
    Show how extracted shape features correspond to physical differences. Cite recent AI and varifold approaches (Kaltenmark 2017, Pierson 2022, Bauer 2017, Hartman 2023, Hartman 2021). Include a comparative experiment if feasible.

16. [ ] **[N] Report computational cost / runtime estimates per pipeline stage** (R1, R4)
    Measure or estimate runtime for preprocessing, cyclic Procrustes, dimensionality reduction, and hypothesis testing. Summarize in a table.

## Reviewer cross-reference

| Reviewer | Points | To-do items |
|----------|--------|-------------|
| R1 | 6 | 1, 5, 6, 9, 12, 13, 14, 16 |
| R2 | 8 | 2, 5, 7, 8, 9, 10, 11, 6 |
| R3 | 4 | 2, 3, 4, 6 |
| R4 | 7 | 1, 5, 6, 9, 12, 14, 15, 16 |
