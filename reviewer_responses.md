# Reviewer Responses

Responses to reviewer comments for "Explainable Binary Classification of Separable Shape Ensembles." Items reference the REVISIONS.md to-do list.

---

## Reviewer 1

### R1.1 — Notation and illustrations (Sections 2–3)
> While generally the presentation of concepts was clear and easy to understand, there are portions of these two sections that were cumbersome to read due to heavy notation and lack of illustrations.

**Response:** [Item 7] *(notation simplification and figures — pending)*

### R1.2 — Terminology ("classification" vs. hypothesis testing; Table 1 "Accept" → "FTR")
> I feel that the title and terminology used in the paper is a bit misleading. The authors are not performing classification, but rather a statistical comparison via a hypothesis testing procedure based on MMD.

**Response:** [Items 5, 6] We respectfully disagree that the terminology is misleading. Two-sample hypothesis testing defines a binary decision rule mapping pairs of distributions to {reject, fail to reject}—this *is* a binary classification at the distribution level, distinct from supervised classification over labeled instances. We have added a technical justification in Sections 1 and 3.5 clarifying this distinction and connecting the title to the formal framework. Table 1 terminology has been updated from "Accept" to "FTR" (Fail To Reject) per the reviewer's suggestion.

### R1.3 — Cyclic Procrustes: random template vs. Fréchet mean
> Why didn't the authors perform this registration with respect to the Frechet mean of the ensemble?

**Response:** [Item 13] The reviewer's suggestion of a Fréchet-mean-based template is well-motivated. We address this as follows:

1. **Why a random template works:** The cyclic Procrustes problem (Theorem 2) finds the *optimal* rotation and cyclic permutation aligning each curve to the template. For asymmetric templates, this alignment is unique. The decision landscape in Fig. 7 demonstrates stability of MMD decisions across quadrature nodes $n$, which implicitly tests archetype sensitivity since different $n$ yield different discrete representations of the random archetype. The key requirement is asymmetry, not optimality, of the template.
2. **Why we did not use the Fréchet mean:** Computing the Fréchet mean over cyclic-Procrustes-aligned curves is a chicken-and-egg problem—alignment requires a template, but the mean requires aligned data. An iterative scheme (align to current mean → recompute mean → repeat) is possible but:
   - Convergence is not guaranteed for the cyclic permutation component (discrete optimization),
   - Each iteration requires $O(N \cdot n)$ SVDs for the full ensemble,
   - The tangent-space Fréchet mean used *after* alignment (Sec. 3.4) is computed on the Grassmannian, which is a different object than a pre-alignment template in $\mathbb{R}^{n \times d}$.
3. **Sensitivity analysis:** We will add a brief sensitivity study comparing decisions under (a) the current random archetype, (b) a different random archetype, and (c) the Fréchet mean of aligned preshapes (one iteration). If decisions are consistent—as the decision landscapes suggest—this justifies the random template pragmatically.
4. **Computational trade-off:** The random template costs $O(N \cdot n)$ SVDs (one pass). An iterative Fréchet mean multiplies this by the number of iterations. For ensembles of $N \sim 10^3$–$10^4$ curves, this difference matters.

### R1.4 — Details of MMD-based hypothesis test (permutations, p-value, Procrustes within permutations)
> How was the p-value computed? ... how many permutations were used? ... how was the cyclic Procrustes procedure incorporated into the hypothesis test?

**Response:** [Item 10] We agree that the manuscript lacked procedural detail for the MMD test. The revised Sec. 3.5 will include the following:

1. **Test statistic:** The unbiased estimator of $\text{MMD}^2$ from Lemma 6 of Gretton et al. (2012), computed separately for undulation and scale coordinates.
2. **Kernel choice:** Gaussian RBF kernel $k(\mathbf{x}, \mathbf{y}) = \exp(-\|\mathbf{x} - \mathbf{y}\|^2 / 2\sigma^2)$, where $\sigma$ is the median pairwise Euclidean distance heuristic over a subset of normal coordinates (already stated in Sec. 4 but will be formalized earlier).
3. **Permutation procedure:** The null distribution of the test statistic is estimated by permutation. Under the null, the ensemble labels (image 1 vs. image 2) are exchangeable. For each permutation: (a) randomly reassign the $N + \hat{N}$ coordinate vectors to two groups of size $N$ and $\hat{N}$, (b) recompute $\widehat{\text{MMD}}^2$ on the permuted groups. This is repeated $B$ times (we use $B = 1000$).
4. **Cyclic Procrustes within permutations:** Critically, cyclic Procrustes registration is performed *once* against the archetype using the full aggregate ensemble *before* the permutation loop. The registration maps each curve to aligned coordinates $(\boldsymbol{t}_q, \boldsymbol{\ell}_q)$ in a common tangent frame. Permutations then shuffle these *pre-registered coordinates*, not the raw curves. This is valid because the archetype and Fréchet mean are computed from the pooled ensemble (both images together), so the registration is label-agnostic. Re-registering within each permutation would be computationally prohibitive and unnecessary given the pooled archetype.
5. **p-value:** $p = (1 + \sum_{b=1}^{B} \mathbf{1}[\widehat{\text{MMD}}^2_b \geq \widehat{\text{MMD}}^2_{\text{obs}}]) / (1 + B)$, where the +1 terms include the observed statistic in the count (conservative estimate). Reject at significance level $\alpha$ if $p \leq \alpha$.

### R1.5 — Simulations (Type I error and power)
> Could the authors carry out a study based on simulated curves/landmark configurations?

**Response:** [Item 14] *(numerical experiment — pending)*

### R1.6 — Computational cost
> The authors should provide an idea of the computational cost associated with the entire procedure.

**Response:** [Item 17] *(numerical experiment — pending)*

---

## Reviewer 2

### R2.1 — Separability assumption (undulation vs. scale independence)
> Is it reasonable to assume separability of undulation and scale in real data examples?

**Response:** [Item 9] The separability assumption (HS, Sec. 2.1) decomposes shape into undulation $[\widetilde{X}] \in Gr(d,n)$ and generalized scale $P \in S^d_{++}$ via the polar decomposition $T_n = \widetilde{X}P$. This decomposition is *algebraically exact*—every full-rank $T_n$ admits a unique polar factorization—so it is not an approximation or modeling assumption.

However, *statistical independence* of the resulting normal coordinates $(\boldsymbol{t}, \boldsymbol{\ell})$ is a stronger claim. In practice:

- **When separability is reasonable:** If shape variation is dominated by either scale (e.g., grain growth) or undulation (e.g., boundary roughness from processing), the cross-correlation between $\boldsymbol{t}$ and $\boldsymbol{\ell}$ coordinates will be small. The EBSD experiments exhibit this: the $(0 \wedge 1)$ case detects undulation differences with no scale discrepancy, and $(1 \wedge 0)$ detects scale differences with no undulation discrepancy.
- **When it may be violated:** Physical processes that simultaneously affect boundary roughness and grain size (e.g., recrystallization) could induce correlation. In such cases, the separate tests remain valid individually but the product interpretation (Truth Table 1) may miss joint effects.
- **Proposed diagnostic:** Compute the sample canonical correlation between $\{\boldsymbol{t}_q\}$ and $\{\boldsymbol{\ell}_q\}$ in the tangent spaces. If the leading canonical correlations are statistically significant (e.g., via Bartlett's test), this flags potential dependence. We can report these correlations for each EBSD experiment to demonstrate the diagnostic.
- **Ramifications:** When dependence is detected, the pMMD framework still applies—the product metric remains a valid metric—but the separate rejection decisions may not fully explain joint variation. In such cases, one could test the joint distribution directly rather than relying on the De Morgan decomposition.

### R2.2 — Terminology ("explainable binary classification")
> I'm not sure if "explainable binary classification" is the right terminology here.

**Response:** [Items 5, 6] See response to R1.2. We retain the title because hypothesis testing *is* a binary classification—it maps distribution pairs to a binary outcome. The "explainable" qualifier refers to the SST decomposition identifying *why* (undulation vs. scale) the discrepancy exists. A technical justification has been added to Sections 1 and 3.5.

### R2.3 — Statistical detail (non-parametric two-sample test procedure)
> There is little statistical detail, particularly in Section 3.

**Response:** [Item 10] See response to R1.4. The revised Sec. 3.5 will include the full permutation test algorithm: test statistic definition, kernel specification, permutation scheme, the role of pre-registration, and p-value formula.

### R2.4 — Multiple testing (joint product-MMD Type I error)
> This doesn't take into account multiple testing concerns... unless adjustments are made (e.g., Bonferroni corrections).

**Response:** [Item 11] The reviewer raises an important point. The De Morgan equivalence in Sec. 3.5 establishes that the *joint null* (both undulation and scale distributions are equal) is rejected if *either* marginal test rejects. When each marginal test is conducted at level $\alpha$, the joint Type I error rate under the intersection null is bounded by $2\alpha$ (union bound), not $\alpha$.

The response will address this as follows:

1. **Bonferroni correction:** The simplest remedy is to conduct each marginal test at level $\alpha/2$. Under the intersection null $H_0: (\rho_{\boldsymbol{t}} = \widehat{\rho}_{\boldsymbol{t}}) \wedge (\rho_{\boldsymbol{\ell}} = \widehat{\rho}_{\boldsymbol{\ell}})$, this guarantees the joint Type I error is at most $\alpha$. For our experiments at $\alpha = 0.01$, each marginal test would use $\alpha/2 = 0.005$.
2. **Practical impact:** With $B = 1000$ permutations, the minimum achievable p-value is $\approx 0.001$, so the Bonferroni correction from $0.01$ to $0.005$ does not change any of the reported decisions in Sec. 4 (all rejections have p-values well below $0.005$; all FTR cases have p-values well above $0.01$).
3. **Reconciliation with De Morgan:** The De Morgan equivalence is a *logical* identity relating the joint and marginal hypotheses. The multiple testing correction is a *statistical* adjustment to control the error rate when evaluating the logical conjunction empirically. Both are compatible: the De Morgan structure tells us *which* tests to run; Bonferroni tells us at *what level* to run them.
4. **Alternative: Holm–Bonferroni** could also be applied (slightly less conservative), but with only two tests the difference is negligible.

### R2.5 — Selecting r, n
> More discussion on selecting r, n, particularly within Section 4, would help.

**Response:** [Item 12] The revised manuscript will add guidelines in Sec. 4 (near the decision landscape discussion) covering:

1. **Quadrature nodes $n$:** The decision landscapes (Figs. 7–8) demonstrate remarkable stability over $n$, with consistent decisions across $n \in [100, 500]$. This stability follows from the spectral accuracy of the Fourier quadrature on smooth closed curves—once $n$ exceeds the effective bandwidth of the boundary, additional nodes contribute negligible information. A practical guideline: choose $n$ large enough that the landmark representation visually resolves boundary features (Fig. 1, right panel). For the EBSD data, $n = 500$ is well into the stable regime.
2. **Undulation dimensionality $r$:** This is the more consequential choice. The decision landscapes show:
   - For $r \leq 7$: empirical regularization suppresses fine-scale undulations, and the test fails to reject even when discrepancies exist (Fig. 7).
   - For $r \geq 8$: consistent rejection in the $(0 \wedge 1)$ case, with monotonically increasing MMD (Fig. 7).
   - The reviewer correctly notes that discrepancies may only appear at higher dimensions. This is exactly the $(0 \wedge 1)$ scenario: smoothing differences manifest in fine undulations captured at $r \geq 8$.
   - **Recommended criterion:** Choose $r$ to capture a cumulative variance threshold (e.g., 95% or 99%) from the tangent PCA spectrum, then verify stability by examining the decision landscape over a range of $r$ values. Ambiguity (defined in Sec. 4.1) provides a practical diagnostic—choose $r$ beyond the ambiguity peak.
3. **Interaction:** The decision landscape framework itself (Figs. 7–8) serves as the primary tool for understanding sensitivity. Given the computational efficiency of the method (seconds per evaluation), practitioners can and should sweep both parameters.

### R2.6 — Writing and organization (contributions buried, background too long)
> I could not distinguish which of these results were from existing work vs. new to this manuscript.

**Response:** [Items 7, 8] *(document restructuring — pending)*

### R2.7 — Illustration of undulation vs. scale
> A figure which describes nonlinear shape undulations vs. linear scale differences would be useful.

**Response:** [Item 7] *(figures — pending)*

### R2.8 — Typo: "it sufficient"
> Typo on page 6 after Eq. (5): "it sufficient" -> "it is sufficient"

**Response:** [Item 2] Fixed.

---

## Reviewer 3

### R3.1 — Formalize lemma/theorem statements
> Lemma 1, Lemma 3, and Theorem 1 could be presented more formally. Lemma 2 wording is awkward.

**Response:** [Item 4] Lemmas 1–3 and Theorem 1 have been rewritten in standard "Let … Then …" style. Lemma 2 now uses $\coloneqq$ notation.

### R3.2 — Acronyms: definition environments for CLO and PRRTI
> PRRTI and CLO have rigorous mathematical definitions and would benefit from being presented in a definition environment.

**Response:** [Item 3] CLO and PRRTI are now presented in numbered `\begin{definition}` environments. SST and HS acronyms are defined at first use.

### R3.3 — Acronyms not introduced on first use (SST, HS)
> The paper begins using acronyms such as SST and HS without introducing them.

**Response:** [Item 3] Fixed. SST is defined parenthetically at first occurrence in Sec. 1.2; HS was already defined but we verified consistency.

### R3.4 — Typos and grammar
> The paper contains several typos, difficult to parse sentences, and incorrect word choices.

**Response:** [Item 2] A full copy-editing pass has been completed. See CHANGES.md for the detailed log.

---

## Reviewer 4

### R4.1 — Presentation quality (overcomplicated, missing visualizations)
> The paper tends to overcomplicate concepts... authors never provide visualisations.

**Response:** [Items 7, 8] *(notation simplification, figures, and restructuring — pending)*

### R4.2 — Problem statement unclear; why not clustering?
> The problem that the paper is trying to solve is not easy to understand. I believe it is to group curves by similarity but then why not using clustering.

**Response:** [Items 5, 6] A paragraph has been added in Sec. 1.1 clarifying that hypothesis testing implies a classification (binary decision with statistical guarantees), whereas clustering aggregates without a formal decision rule. Clustering remains a valid complementary approach. A technical justification connecting hypothesis testing to binary classification is being added to Sections 1 and 3.5.

### R4.3 — Evaluation limited to EBSD
> The choice of evaluation, limited to EBSD feels restricted.

**Response:** [Item 15] *(numerical experiment — pending)*

### R4.4 — Pipeline algorithm figure
> An algorithm presenting the pipeline would be very helpful.

**Response:** [Item 7] *(pipeline algorithm figure — pending)*

### R4.5 — Interpretability claims not demonstrated; AI methods not cited or compared
> The author claims a lot in the introduction the "interpretability" of the method, but it's not used otherwise.

**Response:** [Item 16] We acknowledge that the interpretability claims could be better substantiated. The revision will address this on two fronts:

1. **Demonstrating interpretability:** The separable structure *is* the interpretability mechanism—the Truth Table (Table 1) decomposes a binary decision into *why*: undulation, scale, or both. This is already demonstrated in Sec. 4 (e.g., the $(0 \wedge 1)$ case identifies boundary smoothing as an undulation-only effect; the $(1 \wedge 0)$ case identifies grain size as a scale-only effect). We will make this connection more explicit by:
   - Adding a paragraph in Sec. 4 that walks through how a practitioner interprets each row of the Truth Table in physical terms for the EBSD examples,
   - Showing reconstructed shapes at different points in the learned feature space to visualize *what* undulation and scale variations look like (using the existing dimensionality reduction in Fig. 5).

2. **AI method citations and comparison:** The five references requested by R4 have been added (Item 1). A qualitative comparison will be included in Sec. 1.3 (Contributions) or a new Related Work subsection:
   - **Varifold methods** (Kaltenmark 2017, Bauer 2017): operate on unregistered curves but produce a single scalar distance without separable explanations.
   - **Deep learning on shapes** (Hartman 2023, Hartman 2021, Pierson 2022): require labeled training data and produce opaque latent features. Our method is unsupervised and produces interpretable features by construction.
   - A *quantitative* comparison (e.g., classification accuracy on a shared benchmark) is deferred to Item 15 (non-EBSD dataset) where a fair comparison is feasible.

### R4.6 — Missing/wrong references [1]–[5]
> Some references on the topic are ignored or wrong.

**Response:** [Item 1] All five references have been added with correct sn-aps formatting. Kaltenmark et al. (2017) replaces the incorrect varifold citation. Bauer et al. (2017) is cited in Sec. 1.4. See CHANGES.md for details.

### R4.7 — Conclusion: rejection
> I tend towards rejection: the paper is far from being ready for publications.

**Response:** We appreciate the candid feedback. The revisions address presentation quality (Items 2–4), missing references (Item 1), and the terminology/framing concerns (Items 5–6). Remaining items (experiments, comparisons, pipeline figure) are in progress.
