# Changes Applied to `sn-article-revised.tex`

Detailed log of all edits for revision items 1–5 (low-effort tasks).

---

## Item 1 — Insert missing references [1]–[5] (R4)

### Bibliography fixes
- **Removed 5 duplicate `\bibitem` entries** that had been inserted a second time with inconsistent formatting (kaltenmark2017, pierson2022, bauer2017sobolev, hartman2023varigrad, hartman2021supervised)
- **Reformatted all 5 new entries** to match sn-aps bibliography style (abbreviated first names, journal abbreviations, consistent DOI format)
- **Added missing co-author** P. Harms to `bauer2017sobolev`
- **Removed orphaned text fragment** ("Lynch, E.M., ..." dangling after `\bibitem{lynch2023}`)
- **Fixed malformed DOI** for Lynch 2023: `10://doi.org/10.4031/...` → `10.4031/MTSJ.57.3.1`

### In-text citation additions
- Added `\cite{bauer2017sobolev}` in Sec. 1.4 alongside existing Srivastava citation, where Sobolev metrics on curve spaces are discussed

---

## Item 2 — Correct typos, grammar, and word-choice errors (R2, R3)

### Typos
- "it sufficient" → "it is sufficient" (Sec. 1.4, after Eq. 5)
- "eigendecompsition" → "eigendecomposition" (Sec. 2.3)
- "apriori" → "*a priori*" (Sec. 3.2, italicized as Latin phrase)
- "nickle-manganese-cobalt" → "nickel-manganese-cobalt" (Sec. 4.2)

### Doubled words
- "weighted version of of" → "weighted version of" (Sec. 2, after Eq. 8)
- "by by taking" → "by taking" (Sec. 3.1)

### Grammar
- "These numerical experiment emphasizes" → "These numerical experiments emphasize" (Sec. 4, subject–verb agreement)
- "SST's" → "SSTs" (Sec. 2.1, no apostrophe for plural acronyms)

### Reference errors
- Missing `Figure~` prefix before `\ref{fig:eg_other_images}` (Sec. 1.1)
- `\eqref{fig:nystrom_eg}` → `\ref{fig:nystrom_eg}` (Sec. 3.1, `\eqref` is for equations only)
- Malformed DOI for Lynch 2023 (see Item 1 above)

---

## Item 3 — Introduce all acronyms on first use (R3)

- **SST** (Separable Shape Tensor): defined at first occurrence in Sec. 1.2 — added parenthetical "(SST)" after "separable shape tensor"
- **CLO** (Curve-Level Observation): wrapped in a `\begin{definition}...\end{definition}` environment in Sec. 2, providing a formal statement of the CLO definition
- **PRRTI** (Pre-Registered Random Template Invariance): wrapped in a `\begin{definition}...\end{definition}` environment in Sec. 2, providing a formal statement of the PRRTI definition
- **HS** (Hypothesis of Separability): verified already defined at first use in Sec. 2.1

---

## Item 4 — Formalize statements of lemmas, theorems, and definitions (R3)

### Lemma 1 (Sec. 2.2)
- Rewritten in "Let … Then …" style: "Let $c \in \mathcal{C}_d$ be a closed curve with quadrature weights $\{w_i\}_{i=1}^n$. Then the landmark representation …"

### Lemma 2 (Sec. 2.3)
- Rewritten with `\coloneqq` notation for definitions
- Formal statement now opens: "Let $\boldsymbol{X} \in \mathbb{R}^{n \times d}$ …"

### Lemma 3 (Sec. 3.1)
- Rewritten in formal "Let … Then …" style with explicit hypotheses

### Theorem 1 (Sec. 3.5)
- Rewritten with clearly separated hypotheses and conclusion
- Uses "Let … Suppose … Then …" structure

### Definition environments
- Added numbered `\begin{definition}...\end{definition}` blocks for CLO and PRRTI (see Item 3)

---

## Item 5 — Revise title, abstract, and hypothesis-testing terminology (R1, R2, R4)

### Title
- Changed from "Explainable Binary Classification via Separable Shape Tensors" to **"Explainable Imaging Discrepancies with Separable Shape Ensembles"**

### Abstract
- Revised to foreground the statistical comparison / hypothesis-testing contribution
- Added language framing hypothesis testing as a binary mapping from pairs of distributions into a binary conclusion
- Removed classification-centric framing

### Terminology update
- **Table 1** (Sec. 4): "Accept" → "FTR" (Fail To Reject) in all relevant cells — this is the statistically correct terminology for a hypothesis test that does not reject the null

### New paragraph: hypothesis testing vs. clustering (Sec. 4.1)
- Added a paragraph addressing R4's question of why not use clustering given the proposed distance
- Key argument: hypothesis testing provides a binary conclusion (reject/fail-to-reject) with statistical guarantees, while clustering aggregates similar features without a formal decision rule
- Noted that clustering remains a valid complementary approach for exploratory analysis of SSTs

### Conclusion
- Updated to reflect revised title and terminology (ensembles rather than classification)
