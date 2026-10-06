# COURSE MAP — Homework 1

## Design target

Final capability ladder:

1. **Understand** — explain each primitive in plain language.
2. **Reconstruct** — derive the primitive from definitions without notes.
3. **Transfer** — use it in a new example not copied from lecture.
4. **Independent Homework** — solve the corresponding Homework 1 subproblem cold.

No homework solution formulas or numerical answers are stored here.

---

## Dependency graph

```text
M0 Randomized mechanism -> output distribution
 |
 v
M1 Privacy unit + adjacency
 |
 v
M2 DP definition as an event-wise comparison of output distributions
 |-----------------------------|
 v                             v
M3 Hypothesis testing          M4 DP closure properties
(MIA, FPR/TPR, LRT)            (post-processing, composition)
 |                             |
 |                             v
 |                         M10 repeated access/accounting preview
 |
 v
M5 Global sensitivity + norm geometry (l1/l2)
 |-----------------------------|
 v                             v
M6 Laplace mechanism           M7 Gaussian mechanism
 |                             |
 |                             v
 |                         M9 vector means + clipping + utility error
 |
 v
M8 Randomized response + unbiased estimation
 |
 v
M11 Central vs local threat model

M1 + M4 + M5 + M6 + M7
          |
          v
M12 Record-level vs user-level DP
(group privacy, contribution bounding, time-series vector queries)
          |
          v
M13 Closed-book Homework 1 rehearsal
```

---

## Modules and mastery gates

### M0 — Randomized mechanism -> output distribution
**Why first:** every expression such as P(A(D) in S), likelihood ratio, Laplace/Gaussian mechanism, and attacker test assumes this mental model.

Gate: given a tiny randomized algorithm, explain what is random, what is fixed, and write its output distribution for two fixed datasets.

### M1 — Privacy object / protected unit / adjacency
Topics:
- dataset vs record vs user contribution
- add/remove vs replacement adjacency
- symmetric vs non-symmetric adjacency
- why the same epsilon under different adjacency is not the same promise

Gate: for a new application, state the protected unit and construct a valid neighboring pair without being prompted.

### M2 — Formal DP definition
Topics:
- mechanism, range, event
- epsilon and delta roles
- why the guarantee quantifies over every adjacent pair and every event
- one-sided statement when adjacency is symmetric

Gate: reconstruct the definition and interpret every quantifier.

### M3 — Privacy as binary hypothesis testing
Topics:
- H0/H1, tests, FPR, TPR
- deterministic vs randomized tests
- likelihood ratio and Neyman–Pearson intuition
- DP privacy region

Gate: translate a mechanism + adjacent pair into a membership-inference test problem.

### M4 — Closure properties
Topics:
- post-processing
- simple composition
- sequential/adaptive composition
- conditioning on independent random seeds

Gate: prove a small closure statement directly from the DP definition.

### M5 — Global sensitivity + norm geometry
Topics:
- Delta_p f
- l1 vs l2 geometry
- triangle inequality
- ||x||1 <= sqrt(d)||x||2 and equality cases
- constructing tight examples

Gate: compute sensitivity from adjacency rather than memorized recipes.

### M6 — Laplace mechanism
Topics:
- multidimensional Laplace density
- why l1 sensitivity pairs with coordinatewise Laplace noise
- density-ratio proof
- variance / expected squared error

Gate: derive the privacy ratio bound without looking at the lecture proof.

### M7 — Gaussian mechanism
Topics:
- l2 sensitivity
- classical approximate-DP theorem and its epsilon restriction
- analytic Gaussian mechanism as the general fallback
- why Gaussian noise cannot satisfy finite pure DP

Gate: distinguish what the classical theorem proves from what Gaussian noise itself can do.

### M8 — Randomized response
Topics:
- truth/flip probabilities
- likelihood-ratio tightness
- debiasing
- expectation and exact variance

Gate: derive the unbiased estimator from E[Y|X], not from memorization.

### M9 — Vector means, clipping, and utility error
Topics:
- sensitivity of vector averages
- E||Z||_2^2 and RMS error
- fixed clipping threshold vs data-dependent calibration
- clipping bias vs noise variance

Gate: explain exactly why clipping bounds one person's influence.

### M10 — Repeated releases / accounting preview
Topics:
- repeated access to the same protected people
- simple composition
- why iterative algorithms look bad under naive accounting
- names only for now: advanced composition, RDP, GDP/privacy accounting

Gate: recognize when several outputs are one composed release.

### M11 — Central vs local privacy threat models
Topics:
- trusted curator vs each individual perturbing before collection
- why equal epsilon need not imply equal utility
- what stronger adversary each model protects against

Gate: identify what raw information the analyst is allowed to see.

### M12 — Record-level vs user-level DP
Topics:
- group privacy
- approximate group privacy
- contribution bounding
- designing directly at user level vs converting record-level guarantees
- vector query sensitivity for time series

Gate: rewrite the same application under two privacy units and predict how sensitivity / guarantees change qualitatively.

### M13 — Independent Homework 1
Order:
1. cold solve one subpart at a time
2. classify any error: concept / notation / algebra / calculus / probability / strategy
3. patch only that missing primitive
4. redo from blank paper
5. final full timed reconstruction

---

## Homework mapping — what each subproblem tests

### Problem 1 — Properties of the DP definition
- **1(a):** adjacency symmetry + quantifiers in the DP definition.
- **1(b):** post-processing with extra independent randomness; conditioning / total probability.
- **1(c):** sequential composition; joint distributions and conditioning.
- **1(d):** translate DP events into attacker FPR/TPR constraints; complements and randomized tests.
- **1(e):** interpret a privacy-region inequality numerically and reject a misleading attacker metric.

Primary modules: M1–M4.

### Problem 2 — Basic mechanisms and misconceptions
- **2(a):** correct norm for Laplace calibration; norm inequality; tightness construction.
- **2(b):** tail behavior / likelihood ratios for Gaussian vs Laplace; pure vs approximate DP.
- **2(c):** likelihood-ratio attacker for randomized response; tightness of DP.
- **2(d):** exact expectation/variance of randomized response vs curator Laplace; central vs local privacy.

Primary modules: M3, M5–M8, M11.

### Problem 3 — Private feature mean / DP-SGD preview
- **3(a):** l1/l2 sensitivity of a bounded vector mean under replacement adjacency.
- **3(b):** Gaussian calibration + high-dimensional noise utility.
- **3(c):** Laplace calibration + high-dimensional utility comparison.
- **3(d):** why a data-dependent clipping bound is unsafe; fixed clipping and bias.
- **3(e):** repeated release + simple composition; recognize why later accounting tools matter.

Primary modules: M4–M7, M9–M10.

Important: this is only a DP-SGD preview. Full DP-SGD (per-example gradients, sampling amplification, accountant implementation) is not required to solve this homework.

### Problem 4 — Record-level vs user-level DP
- **4(a):** privacy unit changes sensitivity; unbounded influence; contribution bounding.
- **4(b):** pure-DP group privacy vs direct user-level mechanism design.
- **4(c):** approximate-DP group privacy and limits of generic conversions.
- **4(d):** one vector query vs incorrectly splitting budget across coordinates; user contribution caps.
- **4(e):** writing a complete privacy statement.

Primary modules: M1, M5–M7, M12.

---

## Prerequisites by urgency

### Must understand before solving any homework
- random variables, events, conditional probability
- mechanism as randomized map
- output distributions for fixed D
- privacy unit + adjacency
- DP definition and quantifiers
- l1/l2 norms and basic inequalities
- expectation and variance of independent sums

### Learn only when the corresponding problem approaches
- conditioning on an independent random seed
- joint distribution factorization / chain rule
- equality cases for norm inequalities
- density-ratio tail arguments
- exact Bernoulli variance
- E||Z||_2^2 for iid coordinates
- geometric-series algebra for approximate group privacy
- small-epsilon asymptotics / limits

### Explicitly defer for Homework 1
- full RDP theory and Renyi-divergence proofs
- GDP / f-DP derivations
- advanced composition proofs
- privacy amplification by subsampling
- full DP-SGD mechanics and privacy accountants
- exponential mechanism / Report Noisy Max / Gumbel-Max
- local sensitivity
- graph/node/edge DP

These are valuable later, but learning them now would dilute the dependency path for Homework 1.

---

## Source priority

1. **HW1.pdf** — defines the actual target.
2. **Ch1_v2** — main Lecture 1 reference; use this rather than v1 where they differ.
3. **Ch1_v1** — earlier near-duplicate, useful only for comparison.
4. **Ch2_v1** — later-framework preview; defer except for recognizing names of improved composition/accounting tools.
