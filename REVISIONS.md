# Revision To‑Do List

1. [ ] **Simplify notation in Sections 2‑3 and add illustrative figures** (Reviewer 1, Reviewer 3, Reviewer 4)  
   Reduce heavy mathematical notation to improve readability. Provide clear diagrams for landmark representation, registration process, and manifold features to aid comprehension.

2. [ ] **Revise abstract to highlight statistical comparison; replace “Accept” with “Fail to Reject Null” in Table 1 and Section 3.5** (Reviewer 1, Reviewer 2, Reviewer 4)  
   Update the manuscript's explainable binary classification definition to reflect hypothesis‑testing focus. Adjust abstract language accordingly. Change decision terminology in Table 1 and Section 3.5 to “Fail to Reject Null” for consistency with statistical conventions.

3. [ ] **Replace random template in cyclic Procrustes with Fréchet‑mean template or provide justification** (Reviewer 1, Reviewer 4)  
   Implement a Fréchet‑mean based template for cyclic Procrustes registration to improve stability. If retaining the random template, add a detailed justification of its adequacy and computational trade‑offs.

4. [ ] **Detail MMD hypothesis‑test procedure: number of permutations, algorithmic steps, integration of cyclic Procrustes, kernel choice, and p‑value computation** (Reviewer 1, Reviewer 2, Reviewer 4)  
   Specify the exact number of permutations used and outline the algorithmic workflow. Explain how cyclic Procrustes is applied within each permutation and describe the kernel selection. Provide a clear formula for p‑value calculation.

5. [ ] **Add multiple‑testing correction for joint product‑MMD test (e.g., Bonferroni, Holm‑Bonferroni)** (Reviewer 2)  
   Discuss the inflation of Type I error when testing undulation and scale separately. Implement and report a correction method such as Bonferroni or Holm‑Bonferroni for the joint test.

6. [ ] **Provide guidelines for selecting dimensionality r and quadrature nodes n** (Reviewer 2)  
   Offer criteria (e.g., cumulative variance threshold, stability of MMD statistic) for choosing the number of retained dimensions r and quadrature nodes n. Include a short discussion of the impact on test power.

7. [ ] **Conduct simulated‑data study to assess type I error and power; include at least one non‑EBSD dataset or benchmark comparison** (Reviewer 1, Reviewer 2)  
   Generate synthetic curve ensembles to evaluate the MMD test’s Type I error rate and statistical power. Add a comparative experiment using a non‑EBSD dataset or a benchmark method.

8. [ ] **Report computational cost/runtime estimates for each pipeline stage** (Reviewer 1, Reviewer 4)  
   Provide runtime measurements or complexity estimates for preprocessing, cyclic Procrustes, dimensionality reduction, and hypothesis testing. Summarize these in a table.

9. [ ] **Demonstrate interpretability of shape features and discuss recent AI/varifold methods, optionally with comparative experiment** (Reviewer 4)  
   Show how extracted shape features correspond to physical differences and aid interpretation. Cite recent AI/varifold approaches and, if feasible, include a small comparative experiment.

10. [x] **Insert missing references [1]–[5]** (Reviewer 4)
    Add the cited works to the bibliography, ensuring correct formatting and cross‑referencing.

11. [ ] **Discuss separability assumption of undulation and scale; propose diagnostic for violations** (Reviewer 2)  
    Analyze whether undulation and scale can be assumed independent in real data. Propose a diagnostic test (e.g., correlation analysis) to detect violations.

12. [ ] **Add schematic figure contrasting nonlinear undulation vs. linear scale/rotation/shear** (Reviewer 2)  
    Create a clear schematic illustrating the distinction between undulation and scale/rotation/shear effects to aid reader understanding.

13. [ ] **Re‑structure manuscript: move detailed background to supplementary material, place core contributions earlier** (Reviewer 2)  
    Relocate extensive methodological background to a supplementary appendix. Reorder the main text so that the primary contributions appear in the early sections.

14. [ ] **Formalize statements of lemmas, theorems, and definitions; use definition environments for acronyms (CLO, PRRTI, SST, HS)** (Reviewer 3)  
    Rewrite lemmas, theorems, and definitions in a formal style with proper numbering. Use LaTeX definition environments for the listed acronyms.

15. [ ] **Introduce all acronyms on first use and provide clear definitions** (Reviewer 3)  
    Ensure each acronym (e.g., SST, HS) is defined at its first occurrence in the manuscript.

16. [ ] **Correct typographical errors and improve grammar throughout (e.g., “it sufficient” → “it is sufficient”)** (Reviewer 2, Reviewer 3)  
    Perform a thorough copy‑editing pass to fix typos, grammatical issues, and improve overall readability.
