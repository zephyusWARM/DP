# AI Privacy / Differential Privacy — Learning State

> AI handoff: read `TUTORING_PROTOCOL.md` first, then use this file for the current mastery checkpoint.

Last updated: 2026-10-07

## North Star

The goal is to solve **all of Homework 1 independently from a blank page**, while stating the correct privacy unit / protected unit and adjacency for every DP claim.

The target is not answer recognition. The target is:

1. Understand
2. Reconstruct
3. Transfer
4. Independent Homework

## Checkpoint Policy

This repository is a persistent checkpoint store, not a turn-by-turn transcript.

- Do **not** commit every explanation, drill, correction, or chat turn.
- Update only when a real mastery stage changes, a dependency is cleared, or a durable DP takeaway changes.
- Chat remains the working space; GitHub records stable milestones.
- Homework solutions should not be stored prematurely.

## Current Position

### Course / homework model
- Homework 1 defines the immediate target.
- `Ch1_v2` is the main Lecture 1 reference.
- `Ch1_v1` is an earlier near-duplicate.
- Lecture 2 is deferred except when Homework 1 explicitly asks to name later accounting tools.

### Current module
**M4 — Post-processing + composition**

Why this comes first:
Before `P(A(D) in S)`, likelihood ratios, Laplace/Gaussian mechanisms, or membership inference can mean anything, the learner must have a clean mental model that for fixed `D`, a randomized mechanism `A(D)` is still a random output with a distribution.

### Homework status
**Problem 1(a) conceptually cleared. Problem 1(b) active.**

Tonight's target: finish Problems 1 and 2 by 23:00 using just-in-time prerequisites.

## Current Gate

To clear M0, the learner must be able to do this **closed-book**:

- distinguish what is fixed from what is random in a tiny randomized algorithm;
- explain why a fixed dataset `D` does not imply a deterministic output;
- describe the output distribution of `A(D)`;
- interpret an event such as `A(D) in S` without treating it as notation to memorize.

## Milestone Visual Policy

At genuine mastery milestones, generate a standalone celebratory teaching image in the learner's preferred visual style.

Planned major visual milestones:
- after M2: first complete DP mental model;
- after M5: adjacency -> sensitivity geometry;
- after M9: mechanisms + clipping / utility;
- after M12: complete privacy-unit / user-level mental model;
- after M13: independent Homework 1 completion.

The art is a mastery reward, not an automatic output after every lesson.

<!-- tracker:begin -->
asof: 2026-10-07
goal: independently solve HW1 from a blank page with correct privacy unit and adjacency
M0 | cleared | 2 | Closed-book check passed: fixed D, mechanism randomness, output distribution, and event probability are distinguished correctly.
M1 | cleared | 3 | Transfer check passed: privacy unit, adjacency, symmetry, and a non-symmetric counterexample are understood.
M2 | current | 2 | Can reconstruct the event-wise DP inequality and explain the role of symmetry/quantification.
M3 | locked | 0 | Membership inference, FPR/TPR, likelihood-ratio attacker.
M4 | current | 0 | Problem 1(b) randomized post-processing is now active.
M5 | locked | 0 | Global sensitivity + l1/l2 geometry.
M6 | locked | 0 | Laplace mechanism.
M7 | locked | 0 | Gaussian mechanism.
M8 | locked | 0 | Randomized response + unbiased estimation.
M9 | locked | 0 | Vector means + clipping + utility error.
M10 | locked | 0 | Repeated releases / accounting preview.
M11 | locked | 0 | Central vs local threat models.
M12 | locked | 0 | Record-level vs user-level DP + group privacy + contribution bounding.
M13 | locked | 0 | Independent Homework 1 rehearsal.
check: M0 | done | Explain what is fixed and what is random when D is fixed but A is randomized.
check: M0 | done | Construct the output distribution of a tiny randomized mechanism.
check: M0 | done | Interpret P(A(D) in S) in plain language.
takeaway: course | Every DP claim is meaningless until the privacy unit and adjacency are specified.
takeaway: course | Homework is gated by prerequisites; do not reveal target formulas before the learner can reconstruct them.
takeaway: M0 | For fixed D, the probability comes from the mechanism's internal randomness; the realized output is sampled according to the output distribution induced by that fixed D.
check: P1a | done | One-sided suffices under symmetric adjacency; understands why the reverse direction comes from reapplying the definition to the swapped adjacent pair.
check: P1b | todo | Prove randomized post-processing by conditioning on an independent random seed R.
takeaway: M1 | Symmetry does not algebraically reverse an inequality; it makes the swapped ordered pair adjacent, so the definition applies again.
<!-- tracker:end -->

