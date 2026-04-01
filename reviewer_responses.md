# Reviewer Responses

Responses to reviewer comments for "Explainable Binary Classification of Separable Shape Ensembles." Items reference the REVISIONS.md to-do list.

---

## Reviewer 1

### R1.1 — Notation and illustrations (Sections 2–3)
> While generally the presentation of concepts was clear and easy to understand, there are portions of these two sections that were cumbersome to read due to heavy notation and lack of illustrations.

**Response:** [Item 7] *(pending)*

### R1.2 — Terminology ("classification" vs. hypothesis testing; Table 1 "Accept" → "FTR")
> I feel that the title and terminology used in the paper is a bit misleading. The authors are not performing classification, but rather a statistical comparison via a hypothesis testing procedure based on MMD.

**Response:** [Items 5, 6] We respectfully disagree that the terminology is misleading. Two-sample hypothesis testing defines a binary decision rule mapping pairs of distributions to {reject, fail to reject}—this *is* a binary classification at the distribution level, distinct from supervised classification over labeled instances. We have added a technical justification in Sections 1 and 3.5 clarifying this distinction and connecting the title to the formal framework. Table 1 terminology has been updated from "Accept" to "FTR" (Fail To Reject) per the reviewer's suggestion.

### R1.3 — Cyclic Procrustes: random template vs. Fréchet mean
> Why didn't the authors perform this registration with respect to the Frechet mean of the ensemble?

**Response:** [Item 13] *(pending)*

### R1.4 — Details of MMD-based hypothesis test (permutations, p-value, Procrustes within permutations)
> How was the p-value computed? ... how many permutations were used? ... how was the cyclic Procrustes procedure incorporated into the hypothesis test?

**Response:** [Item 10] *(pending)*

### R1.5 — Simulations (Type I error and power)
> Could the authors carry out a study based on simulated curves/landmark configurations?

**Response:** [Item 14] *(pending)*

### R1.6 — Computational cost
> The authors should provide an idea of the computational cost associated with the entire procedure.

**Response:** [Item 17] *(pending)*

---

## Reviewer 2

### R2.1 — Separability assumption (undulation vs. scale independence)
> Is it reasonable to assume separability of undulation and scale in real data examples?

**Response:** [Item 9] *(pending)*

### R2.2 — Terminology ("explainable binary classification")
> I'm not sure if "explainable binary classification" is the right terminology here.

**Response:** [Items 5, 6] See response to R1.2. We retain the title because hypothesis testing *is* a binary classification—it maps distribution pairs to a binary outcome. The "explainable" qualifier refers to the SST decomposition identifying *why* (undulation vs. scale) the discrepancy exists. A technical justification has been added to Sections 1 and 3.5.

### R2.3 — Statistical detail (non-parametric two-sample test procedure)
> There is little statistical detail, particularly in Section 3.

**Response:** [Item 10] *(pending)*

### R2.4 — Multiple testing (joint product-MMD Type I error)
> This doesn't take into account multiple testing concerns... unless adjustments are made (e.g., Bonferroni corrections).

**Response:** [Item 11] *(pending)*

### R2.5 — Selecting r, n
> More discussion on selecting r, n, particularly within Section 4, would help.

**Response:** [Item 12] *(pending)*

### R2.6 — Writing and organization (contributions buried, background too long)
> I could not distinguish which of these results were from existing work vs. new to this manuscript.

**Response:** [Items 7, 8] *(pending)*

### R2.7 — Illustration of undulation vs. scale
> A figure which describes nonlinear shape undulations vs. linear scale differences would be useful.

**Response:** [Item 7] *(pending)*

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

**Response:** [Items 7, 8] *(pending)*

### R4.2 — Problem statement unclear; why not clustering?
> The problem that the paper is trying to solve is not easy to understand. I believe it is to group curves by similarity but then why not using clustering.

**Response:** [Items 5, 6] A paragraph has been added in Sec. 1.1 clarifying that hypothesis testing implies a classification (binary decision with statistical guarantees), whereas clustering aggregates without a formal decision rule. Clustering remains a valid complementary approach. A technical justification connecting hypothesis testing to binary classification is being added to Sections 1 and 3.5.

### R4.3 — Evaluation limited to EBSD
> The choice of evaluation, limited to EBSD feels restricted.

**Response:** [Item 15] *(pending)*

### R4.4 — Pipeline algorithm figure
> An algorithm presenting the pipeline would be very helpful.

**Response:** [Item 7] *(pending)*

### R4.5 — Interpretability claims not demonstrated; AI methods not cited or compared
> The author claims a lot in the introduction the "interpretability" of the method, but it's not used otherwise.

**Response:** [Item 16] *(pending)*

### R4.6 — Missing/wrong references [1]–[5]
> Some references on the topic are ignored or wrong.

**Response:** [Item 1] All five references have been added with correct sn-aps formatting. Kaltenmark et al. (2017) replaces the incorrect varifold citation. Bauer et al. (2017) is cited in Sec. 1.4. See CHANGES.md for details.

### R4.7 — Conclusion: rejection
> I tend towards rejection: the paper is far from being ready for publications.

**Response:** We appreciate the candid feedback. The revisions address presentation quality (Items 2–4), missing references (Item 1), and the terminology/framing concerns (Items 5–6). Remaining items (experiments, comparisons, pipeline figure) are in progress.
