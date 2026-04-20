# Revision To-Do List

Remaining gaps to close before resubmission. All 24 reviewer comments have a committed reply in `reviewer_response.tex`; the items below are the document edits and experiments those replies still depend on. Types: **D** = document edit, **W** = written-only adjustment, **N** = numerical experiment. Place new prose in blue; log any small fixes in `CHANGES.md`.

## Remaining items

[ ] 1. **MMD permutation-test procedure.** (R1.4, R2.3) [D]
   Replace placeholder at line ~911 in §`subsec:MMD` with a blue-text block: Gaussian RBF with median-distance bandwidth, $B=1000$ label permutations on pre-registered $(\boldsymbol{t}_q,\boldsymbol{\ell}_q)$, and $p=(1+\#\{b:\widehat{\mathrm{MMD}}^2_b\geq\widehat{\mathrm{MMD}}^2_{\mathrm{obs}}\})/(1+B)$. State that cyclic Procrustes is run once on the pooled aggregate before the permutation loop. Mirrors reply R1.4.

[ ] 2. **Bonferroni multiple-testing paragraph.** (R2.4) [D]
   Append ~5 blue-text lines in §`subsec:MMD` immediately after item 1: each marginal test at $\alpha/2$, joint Type I bounded by $\alpha$, no reported decisions change because $p\ll 0.005$ or $p\gg 0.01$. Note De Morgan is a logical identity while Bonferroni is the statistical adjustment — compatible, not redundant. Mirrors reply R2.4.

[ ] 3. **Guidelines for $r$ and $n$.** (R2.5) [D]
   Blue-text paragraph in §`sec:experiments` near the decision-landscape discussion (around `fig:010_decision`): $n\in[100,500]$ from Nyström spectral convergence (`fig:nystrom_eg`), $r$ via 95–99\% cumulative-variance threshold then verified against the decision landscape and the ambiguity metric, pick beyond the ambiguity peak. Mirrors reply R2.5.

[ ] 4. **Prior-vs-new contributions delineation.** (R2.6) [D]
   Replace placeholder at line 198 (§`sec:intro` contributions list) with ~5 blue-text bullets labeling inherited vs new: inherited from `\cite{grey2023sst}` =  SST polar decomposition and separate tangent PCA (not repeated for concision); new here = CLO, PRRTI eigenfunctions, quadrature rule interpretation with Nystrom, cyclic Procrustes against a random asymmetric archetype, pMMD hypothesis test with De-Morgan/Bonferroni logic, decision-landscape diagnostic. Mirrors reply R2.6.

[ ] 5. **Notation paragraph (square brackets, reused shorthand).** (R1.1, R4.1) [D]
   Replace placeholder at line 226 with one paragraph clarifying the square-bracket operator convention (e.g. $\mathcal{K}_{\mathcal{T}}[\boldsymbol{c}]$), cross-referencing the explicit $\mathcal{C}_d$ definition at `eq:reg_Hilbert_space`, and listing heavily-reused symbols. Directly answers R4.1's complaint that the notation paragraph "contains barely any notation."

[ ] 6. **Undulation-vs-scale schematic figure.** (R1.1, R2.6, R4.1) [D]
   Add a two-panel TikZ schematic — left: curves differing only in $\boldsymbol{t}$ (undulation on $\mathrm{Gr}(d,n)$); right: curves differing only in $\boldsymbol{\ell}$ (linear deformation on $S^d_{++}$). Place at the line 237 placeholder in §`subsec:mfld_learn`; this and item 5 together resolve and remove that placeholder. Referenced by replies R1.1, R2.6, R4.1.

[ ] 7. **Remove or upgrade the pipeline-pseudocode placeholder.** (R4.4) [D]
   `fig:placeholder` in §`subsec:mfld_learn` already satisfies R4.4's algorithm request. Minimal-effort: delete the line 941 placeholder and trim the "pseudocode in preparation" sentence from reply R4.4. Upgrade path: replace with a 6–8 line `algorithm` block. Recommend delete.

[ ] 8. **Clustering within an image — decline or short demo.** (R4.2) [W, optional D]
   R4.2 asked why not clustering; reply R4.2 already argues hypothesis testing is a decision rule with guarantees while forward-pointing to a clustering-within-an-image demo at line 1066. Minimal-effort: delete the line 1066 placeholder and remove the forward-reference from reply R4.2 (keep the principled distinction). Optional upgrade covered by item 11.

NF [ ] 9. **Type I / power simulated-curve study.** (R1.5, R2.3) [N]
   Synthetic ensembles with controlled $(\boldsymbol{t},\boldsymbol{\ell})$ differences; sweep effect size; report empirical Type I at the null and power on the alternative. One table plus one small figure panel in §`sec:experiments`. Current reply R1.5 cites decision-landscape stability as partial evidence; the table closes the gap.

ZG [ ] 10. **Per-stage runtime table.** (R1.6) [N]
    Wall-clock timings on a standard laptop for interpolation/arc-length reparametrization, SRQD, cyclic Procrustes, tangent PCA, and $B=1000$ permutation MMD. One small table in §`sec:experiments`. Mirrors reply R1.6.

[ ] 11. ** Non-EBSD demonstration.** (R4.3) [W]
    Reply R4.3 already points to the SEM/NMC battery example in §`sec:experiments` as a non-EBSD case. Minimal-effort: promote that example with a single blue-text sentence at the top of §`sec:experiments` emphasizing it is non-EBSD, and trim the speculative SUVI/MNIST promises from reply R4.3. Higher-effort (pending coauthor review): add a SUVI morphology clustering sub-experiment that also discharges item 8.

## Reviewer coverage (remaining gaps)

| Reviewer | Comments with gaps | Items |
|----------|--------------------|-------|
| R1 | R1.1, R1.4, R1.5, R1.6 | 1, 5, 6, 9, 10 |
| R2 | R2.3, R2.4, R2.5, R2.6 | 1, 2, 3, 4, 6 |
| R3 | none — all R3 comments fully answered by existing edits and replies | — |
| R4 | R4.1, R4.2, R4.3, R4.4 | 5, 6, 7, 8, 11 |

Every reviewer comment is paired with either (a) a reply + completed edit, (b) a reply + a to-do item above, or (c) a reply only where no document edit is warranted (R3 items, R1.2, R1.3, R2.1, R2.2, R2.7, R4.5, R4.6).
