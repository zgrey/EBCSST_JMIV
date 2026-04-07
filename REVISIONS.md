# Revision To-Do List

Items sorted by estimated effort (low to high). Types: **D** = document edits, **W** = written response only, **N** = numerical experiment.

NOTE: I AM MOVING ITEMS AROUND TO BETTER ALIGN WITH THE EFFORT REQUIRED BUT KEEPING ITEM NUMBERS FIXED FOR REFERENCE.

## Low effort

1. ZG [x] **[D] Insert missing references [1]--[5]** (R4)
   Add the cited works to the bibliography with correct formatting and cross-referencing. Verify the cited works are 1) in the body of the text and 2) are actually cited correctly.

2. ZG [x] **[D] Correct typos, grammar, and word-choice errors throughout** (R2, R3)
   Full copy-editing pass: fix "it sufficient" -> "it is sufficient", "elude" -> "allude", difficult-to-parse sentences, and similar issues. When complete, make a new markdown file summarizing detailed changes to grammar.

3. ZG [x] **[D] Introduce all acronyms on first use (SST, HS, CLO, PRRTI, etc.)** (R3)
   Define each acronym at its first occurrence. Use LaTeX definition environments for CLO and PRRTI. Double check that SST and HS definitions are defined in the text as well.

4. ZG [x] **[D] Formalize statements of lemmas, theorems, and definitions** (R3)
   Rewrite Lemma 1, Lemma 3, and Theorem 1 in standard formal style ("Let c in C_d, then ..."). Fix Lemma 2 wording (use `:=` notation). Number all definitions and use definition environments. Note that the LaTeX command used for `:=` notation is \coloneqq

5. ZG [x] **[D] Revise abstract and add hypothesis-testing vs. clustering justification** (R1, R2, R4)
   - Revised abstract to foreground statistical comparison / hypothesis-testing contribution while preserving "explainable binary classification" framing.
   - Added sentence framing hypothesis testing as a binary mapping from pairs of distributions into a binary conclusion (reject/FTR).
   - Added paragraph in Sec. 1.1 justifying hypothesis testing over clustering (R4): hypothesis testing implies a classification with statistical guarantees; clustering is complementary for exploratory analysis.

6. ZG [x] **[D] Justify hypothesis testing as explainable binary classification** (R1, R2, R4)
   - Write a technical description (in Sec. 1 or Sec. 3.5) explaining how two-sample hypothesis testing constitutes a binary classification: the test maps pairs of distributions to {reject, fail to reject}, which is a binary decision rule.
   - Connect this to the title: "explainable binary classification" = hypothesis testing that also explains *why* the discrepancy exists via interpretable SST features.
   - Address reviewer concerns that the paper is not about classification in the supervised-learning sense—clarify the distinction between statistical binary decisions and labeled classification.
   - Respond to R1/R2/R4 who questioned the title/terminology mismatch.

18. [ ] **[W] Demonstrate interpretability and compare with AI/varifold methods** (R4)
    Show how extracted shape features correspond to physical differences. Cite recent AI and varifold approaches (Kaltenmark 2017, Pierson 2022, Bauer 2017, Hartman 2023, Hartman 2021). Include a comparative experiment if feasible.

    **Plan for response**: Citations have been added. Section 2.2 discusses an extensive example of physical differences. We will not be doing exhaustive comparison since the two methods are apples and oranges (distinct representations).

10. ZG [ ] **[W] Discuss separability assumption; propose a diagnostic for violations** (R2)
   Separability does not imply independence. MMD can be used to test independence (see Gretton et al.). We do not study it here but it is an easy modification to run this test.

    **Plan for response**: Add additional clarification to document that separability is not independence.

18. [ ] **[W] Replace random Procrustes template with Frechet mean or justify** (R1, R4)
    Provide detailed justification of adequacy, sensitivity analysis, and computational trade-offs.

    **Plan for response**: Can't replace Procrustes template with Frechet mean (Frechment comes after registration). This will be clarify by addressing item 7. Add detailed justification that a unique solution is sufficient: see figures 8 versus 9 and 5 (stability argument).

## Medium effort

9. AG [ ] **[D] Restructure manuscript: foreground contributions, move background to supplement** (R2)
   ~Move detailed background (Sections 2--3) to supplementary material.~
   - Place core contributions earlier in the main text. Clearly delineate which results are from prior work vs. new to this manuscript (R2 found this hard to distinguish).
  
   **Plan for response**: More clearly delineate new results from old results (SST 4 aero) in section 1.3. Argue against a large scale restructuring of the document unless explicitly requested by the editor (see drafted response). Incorporate edits to be more concise over the entire document.

12. ZG [ ] **[D] Detail the MMD hypothesis-test procedure** (R1, R2, R4)
    Specify: number of permutations, full algorithmic workflow, how cyclic Procrustes is applied within each permutation (R1 notes ensemble changes require re-registration), kernel choice and justification, and p-value computation formula.

    **Plan for response**: Add details to the MMD section regarding the actual tests: number of permutations is 1000 (over ensemble not landmarks), algorithmic workflow is addressed in item 7, cyclic Procrustes is applied once beforehand (will be clarified in algorithmic workflow), Gaussian kernel for universality, p-value computation.

14. [ ] **[D] Add multiple-testing correction for joint product-MMD** (R2)
    Discuss Type I error inflation when testing undulation and scale separately. Maybe implement and report a correction (Bonferroni or Holm-Bonferroni) for the joint test. Reconcile with the DeMorgan equivalence argument in Section 3.5.

    **Plan for response**: Add short discussion of error types but mostly point to Gretton et al.'s work. DeMorgran equivalence is based on the new construction of d(\mathcal{E}_1, \mathcal{E}_2) in section 1.1.

16. ZG [ ] **[D] Provide guidelines for selecting r and n** (R2)
    Offer criteria (cumulative variance threshold, MMD stability, etc.) for choosing retained dimensions r and quadrature nodes n. Discuss impact on test power, noting that discrepancies may only appear in later dimensions with low variance contribution.

    **Plan for response**: Including a test power study if possible. Note, decision landscapes are the machanism for studying MMD stability and choices of r and n. CLARIFY THIS POINT. Clarify existing discussion: we have already addressed the reviewer's concerns with Fig 8 and 9 using the smooting study which "adds noisy wiggles" to the exact same curves by smoothing or not. We make errors when r is small but MMD is stable over both and grows monotonically for fixed registration versus random registrations. We could run another supplemental experiment for the appendix.

## High effort

7. ZG [ ] **[D] Simplify notation in Sections 2--3 and add illustrative figures** (R1, R3, R4)
   Reduce heavy notation to improve readability. Add clear diagrams for: (a) landmark representation and registration (registration in Fig. 4 and 5, landmarks config in Fig. 3), (b) manifold feature spaces, (c) nonlinear undulation vs. linear scale/rotation/shear (the schematic requested by R2). Also add a pipeline algorithm figure (flowchart or pseudocode of the full method, explicitly requested by R4).

   **Plan for response**: I have written down a diagram which I believe tells the story in a precise manner. I will work on creating a tikz picture for this diagram as well as visualizations of curves as they move through the diagram. We should also add simple "psuedo-code" as an algorithm to explain the full procedure.

14. [ ] **[W/N] Conduct simulated-data study for Type I error and power** (R1, R2)
    Generate synthetic curve ensembles to evaluate the MMD test's Type I error rate and statistical power under controlled conditions.

    **Plan for resonse**: Determine if this is already addressed by the smoothing study described by Fig 8 and 9. Discuss adding a new numerical experiment.

16. [ ] **[W] Include a non-EBSD dataset or benchmark comparison** (R1, R4)
    Add a comparative experiment on a standard shape dataset (e.g., MPEG-7 or similar to Kaltenmark et al. 2017). R4 specifically requests evaluation beyond EBSD.

    **Plan for response** We have several results beyond EBSD. Discuss including the clustering example with SUVI data to make this more explicit since EBSD data looks so similar to lithium-ion data. Also discuss including the simple MNIST example to demonstrate a "classification" task.

20. ZG [ ] **[N] Report computational cost / runtime estimates per pipeline stage** (R1, R4)
    Measure or estimate runtime for preprocessing, cyclic Procrustes, dimensionality reduction, and hypothesis testing. Summarize in a table.

    **Plan for response**: Report runtimes in a table for a standard "laptop" build.

## Reviewer cross-reference

| Reviewer | Points | To-do items |
|----------|--------|-------------|
| R1 | 6 | 1, 5, 6, 7, 10, 13, 14, 15, 17 |
| R2 | 8 | 2, 5, 6, 7, 8, 9, 10, 11, 12 |
| R3 | 4 | 2, 3, 4, 7 |
| R4 | 7 | 1, 5, 6, 7, 10, 13, 15, 16, 17 |
