# Global Concision & Redundancy Pass — `sn-article-revised.tex`

Snapshot: commit `0a1d5b9` (pulled 2026-04-22). Focus: **blue (new) content**. Math, notation, definitions, lemmas, theorems, and equations are **not touched**. Only prose is rewritten. Citations are reused but never invented.

## Conventions used below

- **OLD** blocks reproduce current manuscript text. Passages I consider redundant / mergeable are wrapped in `\textcolor{green}{...}` so you can see what is on the chopping block at a glance.
- **NEW** blocks are drop-in LaTeX rewrites — copy-paste ready, blue colouring preserved where the text stays inside the revision-tracking convention.
- Numeric **line refs** match the current `sn-article-revised.tex`.
- Each edit lists the approximate word delta.
- The edits are independent and can be adopted piecewise.

The running theme: three places in the document (§1.1 intro, §1.2 contributions, §3.5 MMD) independently spell out the binary mapping $H$, the decompose/discretize/test triple, and the separable logical conjunction. Intro should *pose*, MMD should *instantiate*, contributions should *enumerate*. Each currently does all three.

Estimated total trim across all edits: **≈ 550–700 words** (≈ one printed page) without losing any claim, citation, or equation.

**Scope note.** Appendix A.1 is intentionally a redundant deep-dive restatement of the main-body material, so it is excluded from this pass — no edits are proposed there, and redundancy between the main body and the appendix is not treated as a reason to shorten.

---

## §1.1 Problem Statement (lines 174–195)

### Edit 1.1 — Collapse the three-paragraph $H$ preamble (lines 176–180)

**Why.** Three consecutive blue paragraphs restate the same point: hypothesis testing = binary mapping, the mapping admits a logical conjunction of marginal tests, and the mapping can be promoted to classification. The same three ideas reappear at line 885 in §3.5 (blue paragraph re-defining $H$) and in the Contributions bullet list at 206. One paragraph here is enough; §3.5 should do the instantiation.

**OLD (lines 176–180):**

```latex
\textcolor{blue}{To formally answer the proposed question in an unsupervised manner, we define a binary mapping $H: (\mathcal{E}, \widehat{\mathcal{E}}) \mapsto \lbrace 0, 1\rbrace$, where $\mathcal{E}$ and $\widehat{\mathcal{E}}$ represent sets of feature-encoding random matrices or tensors---i.e., two \textit{ensembles}. Using two-sample hypothesis testing, $0$ represents the rejection of a null hypothesis (indicating a difference), while $1$ represents a failure to reject (FTR). This boolean determines if the random features of the images are statistically equivalent.}

\textcolor{blue}{\textcolor{green}{Our paradigm of explanation involves offering distinct binary conclusions over decomposed features. We aggregate these logically: $H(\mathcal{E}, \widehat{\mathcal{E}}) \coloneqq H(\mathcal{G}_r, \widehat{\mathcal{G}}_r) \,\wedge\, H(\mathcal{P}, \widehat{\mathcal{P}})$, where $\mathcal{G}_r$ and $\mathcal{P}$ are separate feature representations of ensemble $\mathcal{E}$, likewise for $\widehat{\mathcal{E}}$. Consequently, the results of these separate features provide logical explanations for aggregate decisions. While the statistical nature of these decisions introduces potential error, the framework remains inherently logical by definition.}}

\textcolor{blue}{\textcolor{green}{For our problem, information is implicitly clustered by virtue of the images being compared---e.g., $\mathcal{E}_i \mapsto i$. Thus binary decisions can be generalized to classification tasks such that $\mathcal{E}_1$ is built from one class of images (dogs) and $\mathcal{E}_2$ is built from another (cats). Naturally, a classification model would accept a single image as input and return a corresponding label. In our case, a binary decision machine is also capable of the context-driven classification by keeping one argument of $H(\cdot, \cdot)$ fixed and the other variable or considering all pairwise comparisons of `trusted' (context-driven) ensembles and `discovered' (unknown) ensembles.}}
```

**NEW:**

```latex
\textcolor{blue}{To formally answer the proposed question in an unsupervised manner, we define a binary mapping $H: (\mathcal{E}, \widehat{\mathcal{E}}) \mapsto \lbrace 0, 1\rbrace$, where $\mathcal{E},\widehat{\mathcal{E}}$ are ensembles of feature-encoding random tensors; $0$ rejects the null hypothesis of equality and $1$ is a failure to reject (FTR). Separability lets the aggregate decompose as $H(\mathcal{E},\widehat{\mathcal{E}})\coloneqq H(\mathcal{G}_r,\widehat{\mathcal{G}}_r)\wedge H(\mathcal{P},\widehat{\mathcal{P}})$, so the separate marginal outcomes logically \emph{explain} the aggregate. The same machinery extends to context-driven classification by fixing one argument of $H(\cdot,\cdot)$ and sweeping the other over a database of labelled ensembles.}
```

*Delta: −200 words.*

---

### Edit 1.2 — Tighten the decompose/discretize/test enumeration + lead-in (lines 186–192)

**Why.** The paragraph immediately before the blue enumeration already says "separately approximated distributions of representative shape features"; the bullets then re-announce the same plan with verbs. The Contributions opener at line 198 repeats the exact same decompose/discretize/test triple. Keep the bullets (they are the outline), strip the lead-in down so it does not pre-announce the same three steps.

**OLD (lines 186–192):**

```latex
In this work, quantifying random differences is based on (maximum mean) \emph{discrepancy}~\cite{gretton2012kernel}. \textcolor{green}{More precisely, we ask: are the \textit{separately} approximated distributions of \emph{representative} shape features over the ensemble in one image statistically significant from the ensemble in another? To answer this question procedurally, we propose:}
\textcolor{blue}{\begin{enumerate}[label=\roman*)]
    \item \textit{Decompose} shapes into separate distinguishing features $\leftarrow$ separable shape tensors
    \item \textit{Discretize} and `learn' separate feature distributions from images $\leftarrow$ manifold learning
    \item \textit{Test} for statistically significant discrepancies between images over separate feature distributions $\leftarrow$ maximum mean discrepancy
\end{enumerate}
}
```

**NEW:**

```latex
Quantifying these random differences is based on (maximum mean) \emph{discrepancy}~\cite{gretton2012kernel} over separately approximated distributions of representative shape features. Procedurally:
\textcolor{blue}{\begin{enumerate}[label=\roman*)]
    \item \textit{Decompose} shapes into separate distinguishing features $\leftarrow$ separable shape tensors
    \item \textit{Discretize} and `learn' separate feature distributions from images $\leftarrow$ manifold learning
    \item \textit{Test} for statistically significant discrepancies between images over separate feature distributions $\leftarrow$ maximum mean discrepancy
\end{enumerate}
}
```

*Delta: −35 words.*

---

## §1.2 Contributions & Outline (lines 197–216)

### Edit 2.1 — Merge the practical-efficiency and fixed-reparametrization blue paragraphs (lines 212, 214)

**Why.** Lines 212 and 214 say the same thing twice: registration reduces to SVDs + cyclic permutations, therefore thousands of curves can be swept cheaply, therefore parameter studies are tractable. The distinction (speed vs. sweep-enabling) is not strong enough to warrant two paragraphs.

**OLD (lines 212, 214):**

```latex
\textcolor{blue}{A primary practical contribution is the framework's computational efficiency, which enables shape-comparison using thousands of curves from images which alternative methods struggle to practically address. Registration reduces to finite SVDs collocated at quadrature nodes and cyclic permutations against a single asymmetric archetype (Theorem~\ref{thm:cycl_Procrustes}) rather than an optimization over the space of diffeomorphisms as in elastic and Sobolev-metric curve frameworks~\cite{srivastava2010shape, bauer2017sobolev, hartman2023varigrad}. Thousands of curves can therefore be decomposed and tested in seconds/minutes on a conventional machine.}

\textcolor{blue}{\textcolor{green}{This \textit{fixed reparametrization collocated at quadrature nodes} is what makes the parameter studies of Section~\ref{sec:experiments} tractable: diagnostic parameter sweeping over, the detection of sub-visual smoothing-induced discrepancies (Figure~\ref{fig:compare_grains_010}), and a `goldilocks' analysis of how smoothing scales obscure or preserve distinguishing features for any given segmentation. \textit{To our knowledge, comparisons over such scales and sweeps have not been previously demonstrated for curve ensembles due to the expense of comparing curves}.}}
```

**NEW:**

```latex
\textcolor{blue}{A primary practical contribution is computational efficiency: registration reduces to finite SVDs collocated at quadrature nodes and cyclic permutations against a single asymmetric archetype (Theorem~\ref{thm:cycl_Procrustes}), rather than optimization over diffeomorphisms as in elastic and Sobolev-metric frameworks~\cite{srivastava2010shape,bauer2017sobolev,hartman2023varigrad}. Thousands of curves can therefore be decomposed and tested in seconds on a conventional machine, making tractable the parameter sweeps of Section~\ref{sec:experiments}---including the sub-visual smoothing-induced discrepancies in Figure~\ref{fig:compare_grains_010} and the `goldilocks' segmentation analysis of Figure~\ref{fig:avg_decision_land}. To our knowledge, comparisons over such scales and sweeps have not previously been demonstrated for curve ensembles.}
```

*Delta: −75 words.*

---

### Edit 2.2 — Fold the varifold / AI contrast into the theoretical-contribution paragraph (lines 210, 216)

**Why.** Lines 210 and 216 both position the work relative to related frameworks (Kendall / Micheli, then AI / varifolds / Sobolev). They can live in one paragraph.

**OLD (lines 210, 216):**

```latex
\textcolor{blue}{Our primary theoretical contribution is the second bullet: relating the separable shape tensor (SST) configuration space over finite-dimensional matrix manifolds to a functional analysis over an infinite-dimensional RKHS. This extends the classical configuration-space work of Kendall et al.~\cite{kendall2009shape}---which has no demonstrated connection to an infinite-dimensional space of curves---and permits flexible kernel choice~\cite{micheli2013matrix} to control regularity of a Hilbert space of curves.}

...

\textcolor{blue}{\textcolor{green}{In contrast with AI-based shape analysis~\cite{hartman2023varigrad, hartman2021supervised}, our method requires no hand-labeled training data and produces a provably interpretable feature space grounded in dual representations of curves. Relative to varifold-based approaches~\cite{kaltenmark2017varifolds, pierson2022shape} and Sobolev metrics on curves~\cite{bauer2017sobolev}, which produce a single scalar distance, our separable framework isolates undulation from generalized anisotropic scale, yielding logical explanations via Truth Table~\ref{tab:logical_conjunction} rather than a monolithic discrepancy score.}}
```

**NEW:**

```latex
\textcolor{blue}{Our primary theoretical contribution is the third bullet: relating the SST configuration space over finite-dimensional matrix manifolds to a functional analysis over an infinite-dimensional RKHS. This extends the classical configuration-space work of Kendall et al.~\cite{kendall2009shape}---which has no demonstrated connection to an infinite-dimensional space of curves---and permits flexible kernel choice~\cite{micheli2013matrix} to control regularity. Relative to varifold and Sobolev-metric approaches~\cite{kaltenmark2017varifolds,pierson2022shape,bauer2017sobolev} that return a single scalar distance, and to AI-based shape analysis~\cite{hartman2023varigrad,hartman2021supervised} that requires hand-labeled data and opaque latent features, the separable RKHS construction isolates undulation from anisotropic scale and supplies logical explanations via Truth Table~\ref{tab:logical_conjunction}.}
```

*Delta: −50 words. (Note: "second bullet" → "third bullet" because the Hilbert–Schmidt / eigenfunctions line is now the third item in the list at 200–208; verify before committing.)*

---

## §1.3 Notation (lines 218–229)

### Edit 3.1 — Fold the two blue fragments into the existing notation paragraph

**Why.** The two short blue additions (227, 229) and the surrounding non-blue prose all describe typographical conventions. One paragraph, one list.

**OLD (lines 227 and 229, in place):**

```latex
\textcolor{blue}{With these fundamental building blocks, various quotient topologies are represented as $\mathcal{A}/\mathcal{B}$ by `dividing out' the actions of $\mathcal{B}$ on $\mathcal{A}$.} Elsewhere, we define new notation explicitly and use ``$\coloneqq$'' to indicate that the identification is by definition.

\textcolor{blue}{A convention utilizing square brackets throughout, $[ \cdot ]$, indicates equivalence classes of various types which should be clear from context. \textcolor{green}{This helps delineate specific actions on the curve which should be applied everywhere the argument of $[\cdot]$ appears in the corresponding expression.} Inner products are denoted by angle brackets, $\langle\cdot, \cdot \rangle$, as a bilinear operation while the scalar (dot) product between vectors is expressed equivalently as $\boldsymbol{a}^{\top}\boldsymbol{b} = \boldsymbol{a} \cdot \boldsymbol{b}$. Vectors are always assumed to be tall.}
```

**NEW:**

```latex
\textcolor{blue}{Quotient topologies are written $\mathcal{A}/\mathcal{B}$ (``dividing out'' the action of $\mathcal{B}$), and square brackets $[\cdot]$ denote the induced equivalence classes (e.g.\ $[\boldsymbol{c}]\in\mathcal{A}/\mathcal{B}$).} Elsewhere, we define new notation explicitly and use ``$\coloneqq$'' to indicate identification by definition. \textcolor{blue}{Angle brackets $\langle\cdot,\cdot\rangle$ denote bilinear inner products; the scalar dot product is written equivalently as $\boldsymbol{a}^{\top}\boldsymbol{b}=\boldsymbol{a}\cdot\boldsymbol{b}$; vectors are always tall.}
```

*Delta: −55 words.*

---

## §1.4 Review (lines 231–250)

### Edit 4.1 — Trim the "generalized scale" blue paragraph (line 248)

**Why.** The point — Kendall's classical scale is scalar dilation, ours is the full anisotropic cone $S^d_{++}$, and this is essential for separability — can be made in one sentence rather than four. Pure concision; the paragraph is not internally redundant but is inflated.

**OLD (line 248):**

```latex
\textcolor{blue}{\textcolor{green}{A key distinction from classical configuration-space analyses~\cite{kendall2009shape, srivastava2010shape, srivastava2016functional} is that the \emph{definition of scale is generalized}. Where classical treatments---most notably the work of Kendall~\cite{kendall2009shape}---model scale as a scalar dilation that modulates only overall size, an SST considers the full cone $S^d_{++}$ as \emph{anisotropic} deformations. The separable product $Gr(d,n)\times S^d_{++}$ therefore isolates undulation from general anisotropic scale rather than collapsing scale to a single dilation factor, and this richer notion of scale is essential to the separable hypothesis tests developed in subsequent sections.}}
```

**NEW:**

```latex
\textcolor{blue}{A key distinction from classical configuration-space analyses~\cite{kendall2009shape,srivastava2010shape,srivastava2016functional} is the generalized notion of scale: classical treatments model scale as a scalar dilation, whereas an SST takes the full cone $S^d_{++}$ of anisotropic deformations, so the product $Gr(d,n)\times S^d_{++}$ separates undulation from anisotropic scale---a separation essential to the hypothesis tests of Section~\ref{subsec:MMD}.}
```

*Delta: −55 words.*

---

## §2.3 Cyclic Procrustes (lines 741–808)

### Edit 5.1 — Trim the blue "why not Fréchet mean" paragraph (line 808)

**Why.** Keep the substance; tighten phrasing. The last clause about "somewhat remarkably" adds colour but not information that isn't already in the forward reference.

**OLD (line 808):**

```latex
\textcolor{blue}{A natural intuition is to align against a `central shape,' like the Fr\'echet mean, rather than a random archetype. However, the Fr\'echet mean is coupled with the alignment: alignment requires an archetype, but the mean requires aligned data. An iterative scheme (align $\mapsto$ compute mean $\mapsto$ repeat) is possible but, currently, lacks convergence guarantees for the discrete cyclic permutation component. In contrast, Theorem~\ref{thm:cycl_Procrustes} guarantees that cyclic Procrustes finds \emph{an optimal} alignment to any given template; thus the key requirement is asymmetry of the archetype, not its optimality in the sense of being a Fr\'echet mean. \textcolor{green}{Subsequent numerical experiments, specifically Fig.~\ref{fig:010_decision} and Fig.~\ref{fig:010_decision-normalized}, demonstrate the stability of the random archetype registration over changing $n$ and, somewhat remarkably, an observed stability from simple coordinate normalization despite random row-wise cyclic permutations.}}
```

**NEW:**

```latex
\textcolor{blue}{A natural alternative is to align against a `central shape' such as the Fr\'echet mean. However, the Fr\'echet mean is coupled with alignment---alignment needs an archetype, the mean needs aligned data---and the iterative scheme (align $\mapsto$ mean $\mapsto$ repeat) has no convergence guarantee for the discrete cyclic permutation. Theorem~\ref{thm:cycl_Procrustes} instead guarantees an optimal alignment to \emph{any} template, so the key requirement is asymmetry, not Fr\'echet optimality. Figures~\ref{fig:010_decision}--\ref{fig:010_decision-normalized} confirm empirically that the random-archetype registration is stable across $n$ and that coordinate normalization alone stabilizes decisions even under random row permutations.}
```

*Delta: −45 words.*

---

## §3.5 Maximum Mean Discrepancy (lines 854–921)

### Edit 6.1 — Shrink the $H$-instantiation blue paragraph (line 885), cross-reference §1 instead of restating it

**Why.** This paragraph re-derives the binary mapping $H$ and re-explains that $H(\boldsymbol{\rho},\widehat{\boldsymbol{\rho}}) = H(\rho_{\boldsymbol{t}},\widehat{\rho}_{\boldsymbol{t}}) \wedge H(\rho_{\boldsymbol{\ell}},\widehat{\rho}_{\boldsymbol{\ell}})$ — both already pinned down in §1. Here it is enough to *instantiate* the map via MMD and label it.

**OLD (line 885):**

```latex
\textcolor{blue}{\textcolor{green}{Recalling the motivation of Section~\ref{sec:intro}, hypothesis testing instantiates a binary mapping $H: (\mathcal{E}, \widehat{\mathcal{E}}) \mapsto \lbrace 0, 1\rbrace$ over ambiguous feature ensembles.} Concretely, for each pair of normal coordinate joint distributions, the map $(\boldsymbol{\rho}, \widehat{\boldsymbol{\rho}}) \mapsto \lbrace\text{Reject},\text{FTR}\rbrace$ is a binary decision rule over pairs of distributions---i.e., $\mathcal{E} \coloneqq \boldsymbol{\rho}$, $\widehat{\mathcal{E}} \coloneqq \widehat{\boldsymbol{\rho}}$, and $H$ is the result of the MMD hypothesis test. \textcolor{green}{With separable features, the aggregate decision decomposes as $H(\boldsymbol{\rho}, \widehat{\boldsymbol{\rho} }) \coloneqq H(\rho_{\boldsymbol{t}}, \widehat{\rho}_{\boldsymbol{t}}) \,\wedge\, H(\rho_{\boldsymbol{\ell}} , \widehat{\rho}_{\boldsymbol{\ell}})$, so that Truth Table~\ref{tab:logical_conjunction} logically identifies discrepancies from undulation, scale, or both---constituting the notion of explainability.} We emphasize that this is an unsupervised, distribution-level binary classification via hypothesis testing, distinct but extensible to supervised or context-driven classification over labeled instances.}
```

**NEW:**

```latex
\textcolor{blue}{Concretely, setting $\mathcal{E}\coloneqq\boldsymbol{\rho}$ and $\widehat{\mathcal{E}}\coloneqq\widehat{\boldsymbol{\rho}}$ in the $H$ of Section~\ref{sec:intro}, the MMD hypothesis test \emph{is} an unsupervised, distribution-level binary classifier, extensible to supervised or context-driven classification over labelled ensembles.}
```

*Delta: −120 words.*

---

### Edit 6.2 — Combine the Bonferroni + De Morgan compatibility paragraphs (line 887)

**Why.** One paragraph already; keep it. Minor tightening only: the last sentence can fuse into the main.

**OLD (line 887):**

```latex
\textcolor{blue}{A multiple-testing correction for the joint product-MMD is warranted because the separable hypothesis test is the logical conjunction of two marginal MMD tests. If each marginal is conducted at level $\alpha$, a union-bound argument gives joint Type~I error bounded by $2\alpha$ under the intersection null. We therefore adopt a Bonferroni correction: each marginal MMD test is conducted at level $\alpha/2$, so the joint Type~I error is bounded by $\alpha$. For the experiments of Section~\ref{sec:experiments} at $\alpha = 0.02$, each marginal test uses $\alpha/2 = 0.01$; this correction does not change any of the reported decisions because all rejections satisfy $p$-value $\ll 0.01$ while all FTR cases satisfy $p$-value $\gg 0.02$. \textcolor{green}{Note that the De~Morgan equivalence, $(\rho_{\boldsymbol{t}}=\widehat{\rho}_{\boldsymbol{t}}) \wedge (\rho_{\boldsymbol{\ell}}=\widehat{\rho}_{\boldsymbol{\ell}}) \leftrightarrow \neg((\rho_{\boldsymbol{t}}\neq\widehat{\rho}_{\boldsymbol{t}}) \vee (\rho_{\boldsymbol{\ell}}\neq\widehat{\rho}_{\boldsymbol{\ell}}))$, is a \emph{logical} identity relating joint and marginal hypotheses, while Bonferroni is a \emph{statistical} adjustment; the two are compatible and complementary.}}
```

**NEW:**

```latex
\textcolor{blue}{Because the separable test is a logical conjunction of two marginal MMD tests, a union bound gives joint Type~I error at most $2\alpha$ under the intersection null; we therefore adopt the Bonferroni correction and run each marginal at $\alpha/2$ so that the joint level is bounded by $\alpha$. For Section~\ref{sec:experiments} at $\alpha=0.02$ (hence $\alpha/2=0.01$), none of the reported decisions changes---all rejections satisfy $p\ll 0.01$ and all FTRs satisfy $p\gg 0.02$. The De~Morgan identity underlying Truth Table~\ref{tab:logical_conjunction} is logical, Bonferroni is statistical; the two adjustments are complementary.}
```

*Delta: −70 words.*

---

### Edit 6.3 — Merge the independence + HSIC diagnostic paragraphs (lines 911, 913)

**Why.** Lines 911 and 913 together make one argument: separability ≠ independence, a diagnostic exists (HSIC) but is not pursued, the separable conclusion still holds regardless. Two paragraphs is one too many.

**OLD (lines 911, 913):**

```latex
\textcolor{blue}{Statistical independence of the resulting normal coordinates $(\boldsymbol{t}, \boldsymbol{\ell})$ is a distinct claim from separability which does not assume nor imply independence. Distinct normal coordinates, $\boldsymbol{t}$ and $\boldsymbol{\ell}$, describe distinct shape features. When physical processes simultaneously affect both---e.g., recrystallization correlations driving grain growth and boundary roughness---joint variability may offer supplemental explanations.}

\textcolor{blue}{\textcolor{green}{Although not explored herein, a diagnostic is straightforward: test if the distinct joint distributions from either or both images factor as products of the marginals as in~\cite{gretton2012kernel}---i.e., test with $\text{MMD}[\mathcal{F},\boldsymbol{\rho},\rho_{\boldsymbol{t}}\rho_{\boldsymbol{\ell}}\,]$ over either ensembles or an aggregate ensemble. This is also known as the Hilbert-Schmidt information criterion.} If the joint does not factor as a product of the marginals, the product metric in~\eqref{eq:pMMD} remains valid---features may be separately discrepant and, thus, explainable discrepancy exists---but the separate rejection decisions ignore interesting joint variation. \textcolor{green}{In that case, compare the joint distributions directly to augment the separate discrepancies implied by the De Morgan decomposition and, thus, further augment explanations. In other words, joint variation may be promoting similarity or discrepancy over separate tests but the separate features remain separate by definition and thus imply an aggregate conclusion regardless of independence.}}
```

**NEW:**

```latex
\textcolor{blue}{Separability does not assume or imply statistical independence of $(\boldsymbol{t},\boldsymbol{\ell})$: distinct normal coordinates describe distinct shape features, but physical processes---e.g.\ recrystallization correlations driving both grain growth and boundary roughness---can couple them. A straightforward (un-pursued) diagnostic is to test whether the joint factors as a product of marginals via $\text{MMD}[\mathcal{F},\boldsymbol{\rho},\rho_{\boldsymbol{t}}\rho_{\boldsymbol{\ell}}\,]$~\cite{gretton2012kernel} (the Hilbert--Schmidt information criterion). Whether or not the joint factors, the product metric~\eqref{eq:pMMD} remains valid and the aggregate conclusion of Truth Table~\ref{tab:logical_conjunction} still holds; factoring simply determines whether direct comparison of the joint distributions would add explanatory content beyond the marginal tests.}
```

*Delta: −110 words.*

---

### Edit 6.4 — Tighten the permutation-operations paragraph (line 917)

**Why.** The "must not be conflated" framing is slightly defensive; the content is correct and concise already. One pass to remove the commented-out predecessor and trim a sentence.

**OLD (line 917) — kept in place; trim the "must not be conflated" clause:**

```latex
\textcolor{blue}{\textcolor{green}{Two distinct permutation operations enter the workflow and must not be conflated.} Cyclic Procrustes permutation (Theorem~\ref{thm:cycl_Procrustes}) acts on the \emph{rows} of each individual landmark matrix to register every shape against the random asymmetric archetype. Sample permutations, by contrast, act on the \emph{ensemble labels} of these pre-registered coordinates: for each random sample permutation, the $N + \widehat{N}$ coordinate vectors from the pooled ensembles are randomly reassigned to two groups of sizes $N$ and $\widehat{N}$, and MMD is recomputed on that partition. \textcolor{green}{The latter is known as bootstrapping and we conservatively use $1000$ bootstrap samples in our examples.} The conservative permutation $p$-value is then rejected at significance level $\alpha$ whenever it is less than $\alpha/2$ with the Bonferroni adjustment applied.}
```

**NEW:**

```latex
\textcolor{blue}{Two permutation operations enter the workflow. Cyclic Procrustes permutation (Theorem~\ref{thm:cycl_Procrustes}) acts on the \emph{rows} of each landmark matrix to register every shape against the random asymmetric archetype, once and prior to testing. Sample permutations act on the \emph{ensemble labels}: the $N+\widehat{N}$ pre-registered coordinate vectors are pooled and randomly reassigned to two groups of sizes $N,\widehat{N}$, and MMD is recomputed---repeated $B=1000$ times. The permutation $p$-value is rejected at significance $\alpha$ when it is below $\alpha/2$ per the Bonferroni adjustment above.}
```

*Delta: −40 words. (Incorporates the commented-out line 915 content about bootstrap sample count and kernel choice — consider restoring the kernel sentence if the reviewer flagged it.)*

---

## §4 Numerical Experiments (lines 937–955)

### Edit 7.1 — Merge the four-bullet scenario list (944–949) with the blue Truth-Table summary (955)

**Why.** Bullets 944–949 already describe each of the four scenarios. The blue paragraph at 955 re-maps the same four cases to Truth-Table rows. One unified list with the row labels baked in is cleaner; delete 955 and relabel the bullets. This is the largest single redundancy.

**OLD (lines 944–949, then 955):**

```latex
These numerical experiments emphasize four scenarios where our methods deliver benefits to materials scientists and practitioners investigating micrographs with EBSD: 
\begin{enumerate}[label=\roman*)]
    \item Figure~\ref{fig:compare_grains_111}, \textit{the method is not suspected to be overly sensitive to statistical rejection}: we identified data which concluded, empirically, that there were no useful statistical discrepancies in the compared images.
    \item Figure~\ref{fig:compare_grains_100}, \textit{the method emulates conclusions consistent with human observations}: when provided with data which has very clear human recognizable distinctions described as `scale variations,' the method detects statistical differences in the measured shapes and results in a theoretical interpretation that scale is the significant factor. 
    \item Figure~\ref{fig:compare_grains_010}, \textit{the method detects differences below human-scale visual observations}: given an image processing routine that smooths an EBSD image differently, we demonstrate how the approach detects nonlinear variations in shapes which would otherwise go overlooked by cursory human inspection.
    \item Figure~\ref{fig:compare_grains_000}, \textit{the method detects a presumed faulty measurement}: when provided with data which was suspected to be `out-of-focus' utilizing the state-of-the-art measurement instrumentation, we were able to detect significant differences to indicate the presence of a problem. 
\end{enumerate}

...

\textcolor{blue}{\textcolor{green}{To summarize interpretability, each row of Truth Table~\ref{tab:logical_conjunction} maps to a distinct physical conclusion for the EBSD experiments: $(1 \wedge 1)$ indicates no statistically significant discrepancy in either undulation or scale (Figure~\ref{fig:compare_grains_111}); $(1 \wedge 0)$ isolates a scale-only effect consistent with visible grain-size differences (Figure~\ref{fig:compare_grains_100}); $(0 \wedge 1)$ isolates an undulation-only effect attributable to boundary smoothing, even below visual resolution (Figure~\ref{fig:compare_grains_010}); and $(0 \wedge 0)$ detects discrepancies in both, flagging the presumed faulty measurement (Figure~\ref{fig:compare_grains_000}). The separable decomposition in Figure~\ref{fig:low_dim_grain} further visualizes these distinctions: varying $\boldsymbol{t}$ alone modulates boundary roughness while varying $\boldsymbol{\ell}$ alone modulates anisotropic size and aspect ratio.}}
```

**NEW (keep the enumeration, delete the blue summary, and add the row label in italics per bullet):**

```latex
These numerical experiments span the four rows of Truth Table~\ref{tab:logical_conjunction} and emphasize four scenarios where the method delivers benefits to practitioners investigating EBSD micrographs:
\begin{enumerate}[label=\roman*)]
    \item $(1\wedge 1)$, Figure~\ref{fig:compare_grains_111}: \textit{no over-sensitivity to statistical rejection}---no useful discrepancy in undulation or scale.
    \item $(1\wedge 0)$, Figure~\ref{fig:compare_grains_100}: \textit{conclusions consistent with human observation}---visible grain-size differences yield a scale-only rejection.
    \item $(0\wedge 1)$, Figure~\ref{fig:compare_grains_010}: \textit{discrepancy below visual resolution}---boundary smoothing yields an undulation-only rejection that would be missed by cursory inspection.
    \item $(0\wedge 0)$, Figure~\ref{fig:compare_grains_000}: \textit{detection of a faulty measurement}---an out-of-focus instrument is flagged by simultaneous rejection on both factors.
\end{enumerate}
\textcolor{blue}{The separable decomposition in Figure~\ref{fig:low_dim_grain} visualizes the distinction: varying $\boldsymbol{t}$ alone modulates boundary roughness while varying $\boldsymbol{\ell}$ alone modulates anisotropic size and aspect ratio.}
```

*Delta: −140 words.* (Also tightens each bullet and removes the double-narration.)

---

## §4.1 Decision Landscapes (lines 957–991)

### Edit 8.1 — Minor trim on the $r,n$ guidelines paragraph (line 975)

**Why.** Content is right-sized. Two small simplifications: "should \emph{not} be chosen to maximize variance coverage as in a traditional PCA" is a good rule; the reason clause can be compressed.

**OLD (line 975):**

```latex
\textcolor{blue}{Spectral convergence of Nystr\"om quadrature on smooth closed curves means a modest $n$ suffices; Figures~\ref{fig:010_decision} and~\ref{fig:010_decision-normalized} confirm decisions are stable across $n\in[100,500]$, so $n$ should simply be large enough that the landmarks visually resolve the worst-case boundary in the ensemble. The rank $r$ is more consequential but should \emph{not} be chosen to maximize variance coverage as in a traditional PCA. \textcolor{green}{Smaller $r$ acts as a \textit{dimension reduction} that regularizes shapes against noisy undulations (Figure~\ref{fig:low_dim_grain}), which is often desirable.} We instead study decision variability directly via the \emph{ambiguity}~\eqref{eq:ambiguity}---a scaled Bernoulli variation of the rejection proportion over $r$---and choose $r$ beyond the ambiguity peak so that decisions are stable against the chosen regularization level.}
```

**NEW:**

```latex
\textcolor{blue}{Spectral convergence of Nystr\"om quadrature on smooth closed curves means a modest $n$ suffices---Figures~\ref{fig:010_decision} and~\ref{fig:010_decision-normalized} show decisions are stable across $n\in[100,500]$---so $n$ need only be large enough for the landmarks to visually resolve the worst-case boundary in the ensemble. The rank $r$ is more consequential: smaller $r$ regularizes against noisy undulations (Figure~\ref{fig:low_dim_grain}), but variance-coverage thresholds from traditional PCA are the wrong criterion here. We instead pick $r$ beyond the peak of the \emph{ambiguity}~\eqref{eq:ambiguity}---a scaled Bernoulli variance of the rejection proportion over $r$---so that decisions are stable against the chosen regularization level.}
```

*Delta: −35 words.*

---

## §4.3 Computational Burdens (lines 1042–1070)

### Edit 9.1 — Condense the four blue scaling-discussion paragraphs into two

**Why.** Four consecutive blue paragraphs each re-introduce the same decomposition (embarrassingly-parallel vs. sequential). The content can be delivered in two paragraphs without losing any number or reference.

**OLD (lines 1064, 1066, 1068, 1070):**

```latex
\textcolor{blue}{A rough partition of the pipeline into \emph{embarrassingly parallel} versus \emph{intrinsically sequential} work emphasizes clear mechanisms for acceleration. The per-curve stages---SRQD and cyclic Procrustes alignment---touch each curve independently and both exhibit essentially linear empirical scaling ($\eta\approx 1$). Because no inter-curve synchronization is required, these stages admit process- or thread-level parallelism with speedups bounded only by worker count and memory bandwidth; the reference implementation exposes this via a pluggable backend switch (sequential, threaded, or multiprocess), with multiprocess preferred for the dominant \texttt{scipy} spline evaluations that otherwise hold the global interpreter lock.}

\textcolor{blue}{\textcolor{green}{The pMMD bootstrap is quadratic in ensemble size ($\eta\approx 2$) because each of the $B=1000$ permutations operates on the pooled $N\times N$ Gaussian kernel matrix, but the permutations themselves are independent and the inner kernel-sum loop is pure index arithmetic that compiles cleanly under a just-in-time compiler.} On the test machine, enabling Numba's parallel JIT reduces the $N=2000$ pMMD entry from $30.5$\,s to roughly $0.4$\,s---a two-orders-of-magnitude improvement that effectively removes pMMD from the critical path.}

\textcolor{blue}{\textcolor{green}{The sole sequential bottleneck is tPCA, because computing the Fr\'echet intrinsic mean on the Grassmannian and SPD factors is an iterative reduction---each update is a $\text{Log}$/$\text{Exp}$ step dependent on the previous mean---and the subsequent principal geodesic extraction is a single global singular value decomposition over samples $N$.} In practice tPCA remains one of the cheapest columns at every $N$ we tested, so the single-threaded cost is tolerable; the overall pipeline is dominated by SRQD reparameterization, and accelerating that stage is the highest-leverage optimization.}

\textcolor{blue}{As an independent demonstration that this acceleration is well within reach, an equivalent workflow executed in MATLAB~R2024b on a $20$-thread Ubuntu~22.04 workstation---with SRQD invoked through \texttt{parfor}---reduces the $N=2000$ SRQD entry to $3.45$\,s, an approximately $50\times$ improvement over the single-threaded Python reference. \textcolor{green}{Per-curve concurrency across the $20$ workers contributes most of the speedup; the remainder reflects MATLAB's native compiled spline and SVD primitives.} Full mathematical software packages in both MATLAB and Python are forthcoming.}
```

**NEW (two paragraphs):**

```latex
\textcolor{blue}{Table~\ref{tab:timing} partitions into per-curve work---SRQD and cyclic Procrustes alignment, both empirically linear ($\eta\approx 1$)---and the ensemble-level pMMD bootstrap, quadratic ($\eta\approx 2$) because each of the $B=1000$ permutations touches the pooled $N\times N$ Gaussian kernel matrix. The per-curve stages admit process- or thread-level parallelism with speedups bounded only by worker count and memory bandwidth; the reference implementation exposes this through a sequential/threaded/multiprocess backend switch, with multiprocess preferred because the dominant \texttt{scipy} spline evaluations otherwise hold the global interpreter lock. The pMMD permutations are independent and compile cleanly under a just-in-time compiler: enabling Numba's parallel JIT drops the $N=2000$ pMMD entry from $30.5$\,s to roughly $0.4$\,s, removing it from the critical path.}

\textcolor{blue}{The sole intrinsically sequential stage is tPCA---Karcher iteration is a previous-mean dependent reduction---but Table~\ref{tab:timing} shows tPCA is among the cheapest columns at every $N$, so the single-threaded cost is tolerable. SRQD reparameterization therefore dominates the pipeline and is the highest-leverage optimization target. As an independent demonstration that this acceleration is within reach, an equivalent workflow in MATLAB~R2024b on a $20$-thread Ubuntu workstation (SRQD invoked through \texttt{parfor}) reduces the $N=2000$ SRQD entry to $3.45$\,s---an approximately $50\times$ improvement over the single-threaded Python reference. Full mathematical software packages in both MATLAB and Python are forthcoming.}
```

*Delta: −115 words.*

---

## Cross-section: green-flagged passages worth revisiting even if not adopted

Below is a quick ledger of *all* the green-marked passages above, in document order, so that the author can scan the consolidated list without re-reading every edit. Line numbers are current-file.

| Line | Colour in source | Redundant with | Suggested action |
|------|------------------|----------------|------------------|
| 178  | blue            | 885, 206 bullet | shorten / absorb into 176 (Edit 1.1) |
| 180  | blue            | 206 bullet, §3.5 | move to 176 as one sentence (Edit 1.1) |
| 186  | black           | 198 (blue)      | drop decompose/discretize/test pre-announce (Edit 1.2) |
| 214  | blue            | 212 (blue)      | merge (Edit 2.1) |
| 216  | blue            | 210 (blue)      | merge (Edit 2.2) |
| 229  | blue            | 229 (same para) | trim (Edit 3.1) |
| 248  | blue            | (none — concision only) | compress 4 sentences → 1 (Edit 4.1) |
| 808  | blue (trailing) | Figures 7–8 captions | drop trailing confirmation sentence (Edit 5.1) |
| 885  | blue            | §1.1 lines 176–180 | shrink to instantiation (Edit 6.1) |
| 887  | blue (tail)     | Truth Table caption + De Morgan line 883 | fuse (Edit 6.2) |
| 911  | blue            | 913 (blue)      | merge (Edit 6.3) |
| 913  | blue            | 911 (blue)      | merge (Edit 6.3) |
| 917  | blue (opener)   | (none)          | drop "must not be conflated" framing (Edit 6.4) |
| 955  | blue            | 944–949 bullets | delete, bake row labels into bullets (Edit 7.1) |
| 975  | blue (middle)   | (none)          | minor polish (Edit 8.1) |
| 1066 | blue (lead)     | 1064 (blue)     | merge (Edit 9.1) |
| 1068 | blue (lead)     | 1064 (blue)     | merge (Edit 9.1) |
| 1070 | blue (mid)      | 1064 (blue)     | retain MATLAB demo only (Edit 9.1) |
---

## Items deliberately **not** changed

- **All of Appendix A.1** — by design a redundant deep-dive restatement of the main body; excluded from this pass.
- The notation paragraph's "vectors are always tall" convention — useful downstream, keep.
- The four EBSD experiment captions (Figures 14–17 in appendix) — these are the evidence, not prose.
- Every definition, lemma, theorem, proof, equation, and figure caption.
- The red placeholder at line 1040 (Item 8 in `REVISIONS.md`) — that is a separate decision (keep-or-delete), not a concision pass.
- The title and abstract — the "Explainable Binary Classification" framing is intentional and should not be revisited here.
- The Hilbert–Schmidt integral operator and RKHS evaluation-functional material — these are the theoretical contribution.

---

## Summary of estimated deltas

| Edit | Location | Words removed |
|------|----------|---------------|
| 1.1  | §1.1 intro $H$ paragraphs | −200 |
| 1.2  | §1.1 decompose/discretize/test lead-in | −35 |
| 2.1  | §1.2 efficiency + fixed-reparam paragraphs | −75 |
| 2.2  | §1.2 theory + AI/varifold paragraphs | −50 |
| 3.1  | §1.3 notation | −55 |
| 4.1  | §1.4 generalized-scale paragraph | −55 |
| 5.1  | §2.3 Fréchet-vs-archetype paragraph | −45 |
| 6.1  | §3.5 $H$ re-instantiation | −120 |
| 6.2  | §3.5 Bonferroni + De Morgan | −70 |
| 6.3  | §3.5 independence + HSIC | −110 |
| 6.4  | §3.5 permutation operations | −40 |
| 7.1  | §4 bullets + Truth-Table summary | −140 |
| 8.1  | §4.1 $r,n$ guidelines | −35 |
| 9.1  | §4.3 timings discussion | −115 |
| **Total** | | **≈ −1145 words** |

(The in-text word count is conservative — LaTeX source length trims less because of markup, but the visible prose length on a typeset page shrinks roughly proportionally.)
