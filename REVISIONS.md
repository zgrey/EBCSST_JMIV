# Revision To-Do List

Remaining gaps to close before resubmission. All 24 reviewer comments have a committed reply in `reviewer_response.tex`; the items below are the document edits and experiments those replies still depend on. Types: **D** = document edit, **W** = written-only adjustment, **N** = numerical experiment. Place new prose in blue; log any small fixes in `CHANGES.md`.

## Remaining items

[x] 1. **MMD permutation-test procedure.** (R1.4, R2.3) [D] — done
   Blue-text block in §`subsec:MMD` (lines ~910–916) now specifies biased $\widehat{\mathrm{MMD}}^2$ estimator, Gaussian RBF with median-distance bandwidth, $B=1000$ sample permutations on pre-registered $(\boldsymbol{t}_q,\boldsymbol{\ell}_q)$, and explicitly distinguishes row-level cyclic Procrustes permutation (run once pre-loop against pooled archetype) from sample-label permutation. Reply R1.4 rewritten.

[x] 2. **Bonferroni multiple-testing paragraph.** (R2.4) [D] — done
   Blue text in §`subsec:MMD` at line 882: each marginal at $\alpha/2$, joint Type I bounded by $\alpha$, no reported decisions change because $p\ll 0.005$ or $p\gg 0.01$. Includes De Morgan (logical) vs Bonferroni (statistical) compatibility note. Reply R2.4 rewritten.

[x] 3. **Guidelines for $r$ and $n$.** (R2.5) [D] — done
   Blue text in §`sec:experiments` at line 972 (decision-landscape subsection) covers $n\in[100,500]$ from Nyström spectral convergence, and recommends ambiguity-metric–based selection of $r$ beyond the ambiguity peak rather than raw cumulative-variance thresholding. Reply R2.5 rewritten.

[x] 4. **Prior-vs-new contributions delineation.** (R2.6) [D] — done
   `[prior]`/`[new]` bulleted list in §`sec:intro` at lines 200–208 labels inherited vs new contributions with section cross-references. Reply R2.6 already reflected this.

[x] 5. **Notation paragraph (square brackets, reused shorthand).** (R1.1, R4.1) [D] — done
   Blue text at lines 227 and 229 clarifies quotient-topology notation $\mathcal{A}/\mathcal{B}$, square-bracket equivalence-class convention $[\cdot]$ (e.g.\ $\mathcal{K}_{\mathcal{T}}[\boldsymbol{c}]$), inner-product vs dot-product conventions, and the `vectors are tall' convention. The curve space $\mathcal{C}_d$ is explicitly defined at `eq:reg_Hilbert_space` in §`subsec:preshapes`. R4.1 reply updated to mention the notation expansion.

[x] 6. **Undulation-vs-scale schematic figure.** (R1.1, R2.6, R4.1) [D]
   Add a visualization: curves differing only in $\boldsymbol{t}$ (undulation on $\mathrm{Gr}(d,n)$). See updated fig. 3. Replies R1.1, R2.6, R4.1 all retain "in preparation" language.

[x] 7. **Remove or upgrade the pipeline-pseudocode placeholder.** (R4.4) [D] — done (upgrade path taken)
   `fig:placeholder` in §`subsec:mfld_learn` (line 810) is now a rendered pipeline diagram via `\input{pipeline_diagram}`. Additionally, a concise `algorithm` block (Algorithm~\ref{alg:pipeline}, `algo.tex`) has been added at the end of §`subsec:MMD` stating the full pipeline as pseudocode in manuscript notation with step-level section cross-references. Reply R4.4 updated.

[ ] 8. **Clustering within an image — decline or short demo.** (R4.2) [W, optional D]
   PLACEHOLDER at line 1036 (optional) still present at end of §`sec:experiments` ``Segmentation Efficacy''. Reply R4.2 still forward-references a prepared clustering-within-an-image demo. Minimal-effort path: delete line 1036 placeholder and trim the forward-reference from reply R4.2.

NF [ ] 9. **Type I / power simulated-curve study.** (R1.5, R2.3) [N]
   Synthetic ensembles with controlled $(\boldsymbol{t},\boldsymbol{\ell})$ differences; sweep effect size; report empirical Type I at the null and power on the alternative. One table plus one small figure panel in §`sec:experiments`. Current reply R1.5 cites decision-landscape stability as partial evidence; the table closes the gap.

ZG [ ] 10. **Per-stage runtime table.** (R1.6) [N]
    Wall-clock timings on a standard laptop for interpolation/arc-length reparametrization, SRQD, cyclic Procrustes, tangent PCA, and $B=1000$ permutation MMD. One small table in §`sec:experiments`. Mirrors reply R1.6.

[x] 11. **Non-EBSD demonstration.** (R4.3) [W] — done
    Lithium-ion battery SEM study is now explicitly promoted as a primary experimental contribution in the §`sec:intro` Contributions \& Outline bullet (line 207) — the "non-EBSD" framing is visible from §1.2 rather than buried near the end of §`sec:experiments`. Speculative SUVI / MNIST / Kaltenmark promises have been trimmed from reply R4.3 and ported to `reviewer_responses.md` as shelved work.

## Reviewer coverage (remaining gaps)

| Reviewer | Comments with gaps | Items |
|----------|--------------------|-------|
| R1 | R1.1, R1.5, R1.6 | 6, 9, 10 |
| R2 | R2.6 | 6 |
| R3 | none — all R3 comments fully answered by existing edits and replies | — |
| R4 | R4.1, R4.2 | 6, 8 |

Every reviewer comment is paired with either (a) a reply + completed edit, (b) a reply + a to-do item above, or (c) a reply only where no document edit is warranted.
