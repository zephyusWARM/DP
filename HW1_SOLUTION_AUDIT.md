# HW1 Solution Booklet Audit — 2026-10-08

Status: **NEEDS CORRECTION BEFORE BEING TREATED AS A VERIFIED ANSWER KEY**

Scope: `DP_HW1_A4_大字超級詳解.pdf` (31-page A4 booklet generated 2026-10-07), checked against uploaded `HW1` and `Ch1_v2` / `Ch2_v1` lecture notes.

This audit changes **solution reference quality**, NOT student mastery. Never advance `LEARNING_STATE.md` based on having a solution booklet.

## Confirmed mathematical correction — P1(e)

For FPR=1e-3 and delta=1e-5, **both** inequalities from P1(d) constrain the maximum TPR:

- TPR <= e^eps * FPR + delta
- 1-FPR <= e^eps*(1-TPR)+delta implies TPR <= 1-(1-FPR-delta)/e^eps.

Thus max allowed by these privacy-region constraints is

`min(1, e^eps*FPR+delta, 1-(1-FPR-delta)/e^eps)`.

- eps=8: **0.9996648761886**, NOT 1 (booklet pages 3 and 9 are incorrect).
- eps=1: **0.002728281828**, previous value was correct.

This was the most important factual error. Do not use the old booklet as an answer key until corrected.

## P3(e) — distinguish the question's epsilon-only request from a stronger total (epsilon,delta) target

Homework asks for a *total epsilon = 0.5* over T=100 days, and the factor by which sigma grows relative to (b).

- If per-day delta stays 1e-5 as in (b), epsilon_t=0.005, sigma_t = **100** times baseline, RMS ≈ **19.3792**. Total delta from basic composition is **1e-3**.
- If one additionally requires total (epsilon,delta)=(0.5,1e-5), use delta_t=1e-7 and the classical Gaussian formula gives sigma factor ≈ **117.9998**, RMS ≈ **22.8674**.

The booklet puts the stricter interpretation first. A corrected teaching solution should state the natural epsilon-only reading first, then separate the total-delta-preserving calculation as an explicit additional requirement.

## P4(c) — same noise distribution vs same released random variable

Route A releases `f(D)+Z`, where f counts uncapped total posts.
Route B releases `f_50(D)+Z`, where each user's count is capped at 50.

The noise sigma matches (≈61.0636), and for a target user contributing exactly 50 posts, the neighboring pair has the same center separation (50). Nevertheless, **the two released random variables need not have the same distribution** if other users exceed 50 posts.

Example: target user has 50 posts and another user 200 posts.
- Route A output has center 250.
- Route B output has center 100.

Both use same N(0,sigma²) noise, but their means differ. Their relevant adjacent-pair privacy experiment is equivalent **up to translation**, not literally identical as output random variables. The homework wording itself is potentially overbroad; qualify rather than repeat it literally.

Analytic Gaussian sanity check for eps=5, Delta=50 and sigma=61.06361322 yields analytic delta ≈7.3197e-10 <=1e-8 (as allowed by homework).

## P4(b) — what “strictly better” means

Route B's fixed user-level epsilon=5 guarantee is better **uniformly over unbounded user post counts**. Route A gives group-privacy epsilon=k*0.1 to a user with k posts: k=200 gives epsilon=20, but k<50 yields a smaller individual bound than 5. Avoid unqualified “better for every user” claims.

## Printed-math/layout audit

The 31-page PDF has A4 page geometry and no text blocks beyond page bounds in a structural check, but that is NOT full print-quality verification.

Observed:
- At least some equations contain untypeset literal source characters: `e^{ε₁}`, `P_{D′}`, underscores/carets/braces.
- Page 7 has malformed text near the statement of the map `D -> A_2(D,y)`, plus raw mathematical markup.
- Page 16 places the green “core answer” heading at the bottom, with its text on page 17.
- Page 28 is almost blank because one answer paragraph spilled onto a new page.
- Across the 31-page PDF extraction: 74 literal carets, 82 braces, 125 underscores. Not all are errors, but formulas require real typography, not raw markup.
- The 31-page label “super detailed” overstates the extent of prerequisite-first exposition for a beginner: there are few concept diagrams and several proofs jump quickly into symbols.

Priority fix: regenerate with proper mathematical equation rendering, keep answer callouts with their paragraph, and run page-by-page visual checks.

## Quality gates for a corrected v2

1. Solve every HW item independently; compare with all inequalities and edge cases.
2. Cross-check theorem hypotheses (epsilon validity, adjacency, privacy unit).
3. Numerically recompute all claimed constants.
4. Reconstruct the output of each route on a small counterexample dataset.
5. Render mathematical formulas as equations rather than escaped plain text.
6. Inspect all pages for malformed symbols, orphaned callouts, wasted blank pages, and legibility.
7. Present a student-learning version separately from the concise hand-in solution. The goal is independent mastery, not uncritical copy/paste.

Do not describe the old booklet as fully verified or print-ready.
