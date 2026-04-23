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

[x] 6. **Undulation-vs-scale schematic figure.** (R1.1, R2.6, R4.1) [D] — done
   New Figure 3 (`fig:PL_SST` in §`subsec:geo_interp`) plots piecewise-linear polygons with identical generalized scales but increasing face count, alongside their orthonormal eigenfunctions, isolating undulation variation at fixed scale. Replies R1.1, R2.6, R4.1 updated to point at this figure.

[x] 7. **Remove or upgrade the pipeline-pseudocode placeholder.** (R4.4) [D] — done (upgrade path taken)
   `fig:placeholder` in §`subsec:mfld_learn` (line 810) is now a rendered pipeline diagram via `\input{pipeline_diagram}`. Additionally, a concise `algorithm` block (Algorithm~\ref{alg:pipeline}, `algo.tex`) has been added at the end of §`subsec:MMD` stating the full pipeline as pseudocode in manuscript notation with step-level section cross-references. Reply R4.4 updated.

[x] 8. **Clustering within an image.** (R4.2) [W] — done (declined)
   Red placeholder removed. A clustering demonstration could be included, but we have decided against adding it to keep the manuscript concise per reviewers' other requests. Reply R4.2 now states that clustering is a very natural application of the $(\boldsymbol{t},\boldsymbol{\ell})$ feature space but is deliberately not pursued in this work, flagging a dedicated clustering treatment as follow-on work.

[x] 9. **Type I / power assessment.** (R1.5, R2.3) — done (no simulation required)
   The decision-landscape framework is the effective empirical tool for this assessment and is already in the manuscript. Rationale: (i) Type I is controlled by construction at the permutation-test significance level (exact in finite samples under exchangeability), so it does not require empirical verification; (ii) what remains genuinely empirical for a novel pipeline is the stability of the end-to-end Bernoulli trial over representation choices $(r,n)$, which the decision landscapes in Figures~11, 12, and~15 together with the ambiguity metric (Eq.~(25)) quantify directly at fixed significance level. Reply R1.5 rewritten. An optional extension---per-example decision landscapes for each Appendix~B case---is offered in the reply but weighed against competing reviewer requests for concision and brevity.

[x] 10. **Per-stage runtime table.** (R1.6) [N] — done
    Table~\ref{tab:timing} in §`sec:experiments` (Subsection 4.3 ``Timings'') reports wall-clock seconds for cyclic Procrustes, SRQD (which subsumes arc-length reparameterization), tPCA, and $B=1000$-permutation pMMD across $N\in\{100,\dots,2000\}$. A summary row reports the empirical scaling exponent $\widehat{\eta}$ fit to $t(N)\approx C\,N^{\widehat{\eta}}$. The accompanying paragraph partitions the pipeline into embarrassingly-parallel stages versus the intrinsically-sequential tPCA reduction, quantifies the Numba parallel-JIT speedup that removes pMMD from the critical path, and cites an independent MATLAB R2024b run with SRQD via \texttt{parfor} as a $\sim 50\times$ demonstration of SRQD acceleration headroom. Reply R1.6 rewritten.

[x] 11. **Non-EBSD demonstration.** (R4.3) [W] — done
    Lithium-ion battery SEM study is now explicitly promoted as a primary experimental contribution in the §`sec:intro` Contributions \& Outline bullet (line 207) — the "non-EBSD" framing is visible from §1.2 rather than buried near the end of §`sec:experiments`. Speculative SUVI / MNIST / Kaltenmark promises have been trimmed from reply R4.3 and ported to `reviewer_responses.md` as shelved work.

## Reviewer coverage (remaining gaps)

None. All 24 reviewer comments are paired with a completed reply + edit or a reply-only response where no document edit is warranted. Items 1--11 above are all closed.
