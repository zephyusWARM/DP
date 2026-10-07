# Interactive Learning Page Protocol

Last updated: 2026-10-07

This file records the preferred architecture for building interactive teaching webpages in this repository.

The reference pattern comes from the user's single-file HTML total-probability marble experiment. The goal is to preserve the **teaching architecture**, not merely copy its visual styling.

## 1. Core design principle

Interactive pages should make an abstract concept physically manipulable.

Use this separation:

```
concept / probability model
        ↓ decides
simulation state / branch
        ↓ rendered by
physics / geometry
        ↓ displayed by
UI / canvas / text / controls
```

A useful mental model is:

> **Probability decides the branch; physics makes the branch visible.**

The page should let the learner see the theoretical quantity and the empirical simulation at the same time.

## 2. Default file structure

Prefer a self-contained single HTML file when practical.

### A. `<style>`
Responsibilities:
- CSS design tokens
- typography
- light / dark themes
- responsive layout
- focus states
- reduced-motion behavior

Preferred visual language:
- Apple-like minimalism
- Traditional Chinese
- one main accent color
- generous spacing
- no unnecessary gradients / decorative colors
- mobile layout must not scroll horizontally

### B. Semantic HTML
Prefer a simple two-column desktop structure:
- left: one main interactive stage, usually `<canvas>`
- right: controls, theory, measured result, explanation

On small screens, collapse to one column.

A page should have **one primary interaction**, not many unrelated widgets.

### C. Pure simulation / model script
Use a function such as:

```js
function createSim() { ... }
```

This layer:
- owns simulation state;
- owns probability parameters;
- owns physics / geometry if needed;
- owns counts and empirical outcomes;
- does **not** access the DOM.

This makes the conceptual model reusable and keeps UI refactors from breaking the model.

### D. UI / renderer script
This layer:
- creates / obtains the simulation;
- draws the canvas;
- binds sliders, buttons, pointer events;
- updates formulas and explanatory text;
- shows empirical counts;
- manages light/dark mode;
- respects `prefers-reduced-motion`;
- handles responsive sizing.

The UI is a view/controller layer, not the source of mathematical truth.

## 3. Probability ↔ physics bridge

When a physical simulation is used, separate two responsibilities.

### Probability layer
At meaningful branch points, sample the mathematical event.

Example:

```js
const branch = Math.random() < p;
```

For total probability:
- first switch samples `R`;
- second switch samples `E` conditional on the chosen value of `R`.

### Physics layer
After the branch is sampled:
- give the object the corresponding direction / velocity / target;
- let the physical engine animate that decision;
- count the outcome only after it reaches its terminal region.

The physics should **visualize the sampled event**, not redefine the probability model.

## 4. Theory and experiment must coexist

A strong teaching page should show both:

### Theory
The exact mathematical quantity, e.g.

```
P(E) = p q0 + (1-p) q1
```

### Experiment
The empirical estimate:

```
P_hat(E) = (# observed E) / (# trials)
```

The learner should be able to watch the empirical quantity approach the theoretical one as sample size grows.

This is more educational than showing only animation or only a formula.

## 5. Multiple representations, one concept

Use a second representation only when it explains the same concept from another angle.

Good example:
- marble simulation = repeated trials;
- formula = exact probability;
- seesaw = weighted average.

For the seesaw metaphor:
- horizontal position = `P(E | R=r)`;
- weight / mass = `P(R=r)`;
- balance point = `P(E)`.

The representation must have a precise mathematical mapping. Avoid decorative metaphors with no exact correspondence.

## 6. Interaction rules

Prefer:
- sliders for probability parameters;
- direct manipulation on the main canvas when natural;
- pointer events so mouse / touch / pen share one implementation;
- one-click presets for important examples;
- a short challenge mode that hides the answer;
- immediate feedback based on common misconceptions.

Do not add interaction merely because it is possible.

Every interaction should answer a teaching question.

## 7. Accessibility and robustness

Required defaults:
- semantic labels / ARIA where useful;
- visible keyboard focus;
- `prefers-reduced-motion`;
- responsive canvas sizing;
- cap device pixel ratio when appropriate;
- no horizontal overflow on mobile;
- dark and light themes;
- controls large enough for touch;
- text remains readable without relying on color alone.

## 8. Rendering / simulation implementation pattern

For physics-heavy pages:
- use a fixed simulation timestep;
- cap velocity to avoid tunneling;
- separate collision functions;
- use spatial partitioning when object count grows;
- let settled objects sleep;
- decouple simulation coordinates from CSS pixels;
- render according to device-pixel ratio.

Animation quality matters only insofar as it improves comprehension.

## 9. Teaching-copy pattern

The page should follow the same pedagogical ladder as the course:

1. one-sentence purpose;
2. manipulate the phenomenon;
3. show the exact formula;
4. compare theory with measurement;
5. explain why the formula has that structure;
6. offer one small retrieval / prediction challenge;
7. reconnect to the actual homework or theorem.

Avoid dropping the full proof on screen before intuition exists.

## 10. DP-specific page ideas

This architecture can be reused later for:

### Randomized post-processing
- random seed `R` chooses a deterministic map;
- freeze `R=r`;
- compare each conditional branch;
- average back over `r`.

### Sensitivity
- drag one protected unit in / out;
- show the induced query-output displacement;
- display the worst adjacent jump.

### Laplace / Gaussian mechanisms
- fixed query output;
- repeatedly sample noise;
- show two neighboring output distributions;
- display empirical likelihood / event probabilities.

### Record-level vs user-level DP
- toggle the privacy unit;
- visually change which records move together;
- show how the adjacency graph changes.

## 11. Quality bar

A page is successful only if:
- the interaction makes the concept easier to explain afterward;
- the simulation and formula agree;
- the learner can state what every visual element means mathematically;
- layout works from narrow mobile to desktop;
- no console errors;
- no horizontal overflow;
- dark/light modes both work.

A beautiful page that does not sharpen the mental model is not a successful teaching page.

## 12. Source-of-truth rule

Interactive pages are teaching views.

They must not become a second learning-state database.

For learner progress:
- `LEARNING_STATE.md` remains canonical.
- `COURSE_MAP.md` remains the curriculum / dependency source.
- interactive pages may read those files, but should not silently invent mastery state.
