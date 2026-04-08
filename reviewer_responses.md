# Reviewer Responses

Responses to reviewer comments for "Explainable Binary Classification of Separable Shape Ensembles." Items reference the REVISIONS.md to-do list.

Note that large additions/modifications are color-coded blue while small changes are documented in CHANGES.md

---

## Reviewer 1

### R1.1 — Notation and illustrations (Sections 2–3)
> While generally the presentation of concepts was clear and easy to understand, there are portions of these two sections that were cumbersome to read due to heavy notation and lack of illustrations.

**Response:** [Item 13] *(notation simplification and figures — pending; TikZ pipeline diagram in progress)*

### R1.2 — Terminology ("classification" vs. hypothesis testing; Table 1 "Accept" → "FTR")
> I feel that the title and terminology used in the paper is a bit misleading. The authors are not performing classification, but rather a statistical comparison via a hypothesis testing procedure based on MMD.

**Response:** [Items 5, 6] We respectfully disagree that the terminology is misleading. Two-sample hypothesis testing defines a binary decision rule mapping pairs of distributions to {reject, fail to reject}—this is a binary classification/mapping for determining if two distributions are the same or not albeit distinct from supervised classification over labeled instances. Technical justifications have been added in Sec. 1.1 (blue text defining the binary mapping $d: (\mathcal{E}_1, \mathcal{E}_2) \mapsto \{0,1\}$ and its separable decomposition) and in Sec. 3.5 (blue text connecting pMMD to this binary mapping and distinguishing from supervised learning). Table 1 terminology has been updated from "Accept" to "FTR" (Fail To Reject) per the reviewer's suggestion.

### R1.3 — Cyclic Procrustes: random template vs. Fréchet mean
> Why didn't the authors perform this registration with respect to the Frechet mean of the ensemble?

**Response:** [Item 9] The reviewer's suggestion of a Fréchet-mean-based template is well-motivated. A justification has been added in Sec. 3.3 (blue text) addressing this directly:

1. **Why a random template works:** Theorem 2 guarantees that cyclic Procrustes finds the *optimal* rotation and cyclic permutation aligning each curve to the template. The key requirement is asymmetry, not optimality, of the template. The decision landscape stability over $n$ in Fig. 7 provides empirical evidence—since different $n$ yield different discrete representations of the same random archetype, consistent decisions across $n$ implicitly test archetype sensitivity.
2. **Why we did not use the Fréchet mean:** Computing the Fréchet mean over cyclic-Procrustes-aligned curves is a chicken-and-egg problem—alignment requires a template, but the mean requires aligned data. An iterative scheme is possible but lacks convergence guarantees for the discrete cyclic permutation component, and each iteration requires re-solving $N$ SVDs across $n$ quadrature nodes---rapidly becoming expensive for large ensembles.

### R1.4 — Details of MMD-based hypothesis test (permutations, p-value, Procrustes within permutations)
> How was the p-value computed? ... how many permutations were used? ... how was the cyclic Procrustes procedure incorporated into the hypothesis test?

**Response:** [Item 11] We agree that the manuscript lacked procedural detail for the MMD test. The revised Sec. 3.5 will include the following: *(pending)*

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

**Response:** [Item 14] *(runtime table — pending)*

---

## Reviewer 2

### R2.1 — Separability assumption (undulation vs. scale independence)
> Is it reasonable to assume separability of undulation and scale in real data examples?

**Response:** [Item 7] A concise discussion has been added in Sec. 2.1 (blue text). The polar decomposition $T_n = \widetilde{X}P$ is algebraically exact—every full-rank $T_n$ admits a unique factorization—so separability is not an approximation. However, *statistical independence* of the resulting normal coordinates $(\boldsymbol{t}, \boldsymbol{\ell})$ is a stronger claim. In practice, separability is reasonable when shape variation is dominated by either scale (e.g., grain growth) or undulation (e.g., boundary roughness from processing), as our EBSD experiments illustrate. When physical processes simultaneously affect both (e.g., recrystallization), cross-correlation may arise. We propose a straightforward diagnostic: compute the sample canonical correlation between $\{\boldsymbol{t}_q\}$ and $\{\boldsymbol{\ell}_q\}$ and test significance via Bartlett's test. If dependence is detected, the product metric remains valid but the separate rejection decisions may not fully explain joint variation; one could test the joint distribution directly rather than relying on the De Morgan decomposition.

### R2.2 — Terminology ("explainable binary classification")
> I'm not sure if "explainable binary classification" is the right terminology here.

**Response:** [Items 5, 6] See response to R1.2. We retain the title because hypothesis testing *is* a binary classification—it maps distribution pairs to a binary outcome. The "explainable" qualifier refers to the SST decomposition identifying *why* (undulation vs. scale) the discrepancy exists. Technical justifications have been added in Sec. 1.1 and Sec. 3.5 (blue text).

### R2.3 — Statistical detail (non-parametric two-sample test procedure)
> There is little statistical detail, particularly in Section 3.

**Response:** [Item 11] See response to R1.4. The revised Sec. 3.5 will include the full permutation test algorithm: test statistic definition, kernel specification, permutation scheme, the role of pre-registration, and p-value formula. *(pending)*

### R2.4 — Multiple testing (joint product-MMD Type I error)
> This doesn't take into account multiple testing concerns... unless adjustments are made (e.g., Bonferroni corrections).

**Response:** [Item 11] The reviewer raises an important point. This will be addressed as part of the MMD procedure detail: *(pending)*

1. **Bonferroni correction:** The simplest remedy is to conduct each marginal test at level $\alpha/2$. Under the intersection null, this guarantees the joint Type I error is at most $\alpha$. For our experiments at $\alpha = 0.01$, each marginal test would use $\alpha/2 = 0.005$.
2. **Practical impact:** With $B = 1000$ permutations, the minimum achievable p-value is $\approx 0.001$, so the Bonferroni correction from $0.01$ to $0.005$ does not change any of the reported decisions in Sec. 4 (all rejections have p-values well below $0.005$; all FTR cases have p-values well above $0.01$).
3. **Reconciliation with De Morgan:** The De Morgan equivalence is a *logical* identity relating the joint and marginal hypotheses. The multiple testing correction is a *statistical* adjustment to control the error rate when evaluating the logical conjunction empirically. Both are compatible: the De Morgan structure tells us *which* tests to run; Bonferroni tells us at *what level* to run them.

### R2.5 — Selecting r, n
> More discussion on selecting r, n, particularly within Section 4, would help.

**Response:** [Item 12] *(guidelines — pending)*

### R2.6 — Writing and organization (contributions buried, background too long)
> I could not distinguish which of these results were from existing work vs. new to this manuscript.

**Response:** [Items 10, 13] We have begun clarifying the contributions section to delineate results specific to this manuscript versus previous work applied to aerodynamic bodies. We also acknowledge that many modern papers are written with concise descriptions and massive supplementary materials. However, we think this practice breaks with respected classical presentations which weave the formalisms into the narrative. Our opinion is that these formalisms should be critiqued, in detail, as part of the narrative and included in the main body of a contribution to a mathematical journal to promote more transparency and reproducibility---far too much is lost or ignored in supplementary materials. This is a failure of some researchers who "hide the details" in overly complicated supplementary materials as opposed to our attempt at being simultaneously precise and concise. *(Further restructuring and concision edits pending.)*

### R2.7 — Illustration of undulation vs. scale
> A figure which describes nonlinear shape undulations vs. linear scale differences would be useful.

**Response:** [Item 13] *(figures — pending)*

### R2.8 — Typo: "it sufficient"
> Typo on page 6 after Eq. (5): "it sufficient" -> "it is sufficient"

**Response:** [Item 2] Fixed. See CHANGES.md for the full list of corrections.

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

**Response:** [Item 3] Fixed. SST is defined parenthetically at first occurrence in Sec. 1.2; HS is defined in Lemma 2.

### R3.4 — Typos and grammar
> The paper contains several typos, difficult to parse sentences, and incorrect word choices.

**Response:** [Item 2] A full copy-editing pass has been completed. See CHANGES.md for the detailed log. We have also made efforts to simplify the discussion and be more concise where possible.

---

## Reviewer 4

### R4.1 — Presentation quality (overcomplicated, missing visualizations)
> The paper tends to overcomplicate concepts... authors never provide visualisations.

**Response:** [Items 10, 13] *(notation simplification, figures, and restructuring — pending; TikZ pipeline diagram in progress)*

### R4.2 — Problem statement unclear; why not clustering?
> The problem that the paper is trying to solve is not easy to understand. I believe it is to group curves by similarity but then why not using clustering.

**Response:** [Items 5, 6] Blue text has been added in Sec. 1.1 clarifying that hypothesis testing implies a classification (binary decision with statistical guarantees) between *distributions encoding shape*, whereas clustering simply aggregates without a formal decision rule. However, clustering remains a valid complementary approach and we include examples to emphasize how clustering over our proposed features within a single image may be helpful for generalizing decision making. A formal justification connecting hypothesis testing to binary classification has been added to Sec. 1.1 and Sec. 3.5 (blue text). The problem we are attempting to solve is also very clearly stated in the section titled "Problem Statement":

*Are the curves/shapes in one image, up to rigid motions, the same or different from that of another and, if they are different, are differences due to linear deformations (generalized scale variations) or nonlinear deformations (undulations)?*

### R4.3 — Evaluation limited to EBSD
> The choice of evaluation, limited to EBSD feels restricted.

**Response:** [Item 15] Our evaluations are not limited to EBSD. We have an explicit example detailed in Sec. 4.2 which can be applied to any gray-scale image. We are also preparing additional examples (pending coauthor review): a SUVI sun image clustering example demonstrating clustering over proposed features within a single image, and an MNIST pairwise digit classification example demonstrating a supervised classification task.

### R4.4 — Pipeline algorithm figure
> An algorithm presenting the pipeline would be very helpful.

**Response:** [Item 13] *(pipeline algorithm figure — pending; TikZ diagram in progress)*

### R4.5 — Interpretability claims not demonstrated; AI methods not cited or compared
> The author claims a lot in the introduction the "interpretability" of the method, but it's not used otherwise.

**Response:** [Item 8] The revisions address this on two fronts:

1. **Demonstrating interpretability:** Blue text has been added in Sec. 4 walking through how each row of the Truth Table maps to a distinct physical conclusion for the EBSD experiments: $(1 \wedge 1)$ = no discrepancy, $(1 \wedge 0)$ = scale-only effect (grain size), $(0 \wedge 1)$ = undulation-only effect (boundary smoothing), $(0 \wedge 0)$ = both. The dimensionality reduction in Fig. 5 further visualizes these distinctions: varying $\boldsymbol{t}$ alone modulates boundary roughness while varying $\boldsymbol{\ell}$ alone modulates anisotropic size.

2. **AI/varifold method comparison:** Blue text has been added in Sec. 1.3 providing a qualitative comparison. Varifold methods (Kaltenmark 2017, Bauer 2017) bypass registration but produce a single scalar distance without separable explanations. Deep learning approaches (Hartman 2023, Hartman 2021, Pierson 2022) require labeled training data and produce opaque latent features. Our method is unsupervised and produces interpretable features by construction. All five requested references have been added (Item 1).

### R4.6 — Missing/wrong references [1]–[5]
> Some references on the topic are ignored or wrong.

**Response:** [Item 1] All five references have been added with correct sn-aps formatting. Kaltenmark et al. (2017) replaces the incorrect varifold citation. Bauer et al. (2017) is cited in Sec. 1.4. See CHANGES.md for details.

### R4.7 — Conclusion: rejection
> I tend towards rejection: the paper is far from being ready for publications.

**Response:** We appreciate the candid feedback. The revisions address presentation quality (Items 2–4), missing references (Item 1), terminology and framing concerns (Items 5–6), the separability assumption (Item 7), interpretability demonstration and AI/varifold comparison (Item 8), and the random archetype justification (Item 9). Further improvements to notation, figures, and additional experiments are in progress (Items 10–15).
