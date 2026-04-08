# Development Notes - DriftCompass

## Current conceptual state

The current prototype is organized around four ideas:

1. **Structural binomial**
2. **Structural potential of the binomial**
3. **Observed turn-by-turn trajectory**
4. **Latent change through pressure**

These layers should not be collapsed back into each other.

---

## Main variables

### User

- `u0`: Rigidity
- `u1`: Openness
- `u2`: Loop
- `u3`: Energy

### Model

- `m0`: Validation
- `m1`: Friction
- `m2`: Metacognition
- `m3`: Precision

### Simulation state

- `turn`
- `hist`
- `engagement`
- `pressureU`
- `pressureM`
- `selE`, `selU`, `selM`
- `lastTurnE`, `lastTurnU`, `lastTurnM`

`sel*` represents the live selection for the in-progress turn.  
`lastTurn*` represents memory of the last committed turn.

---

## Base system formula

The compass still derives from a combination of user and model traits:

```txt
uA = (u1 - u0*0.8 - u2*0.6) * 0.45
mA = (m2*1.3 + m1*0.5 - m0*0.7) * 0.35
eA = (u3 - 5) * 0.1

y = clamp((uA + mA + eA) / 4, -1, 1)
x = clamp((u1-u0)/10 + (m2-m0)/10*0.5, -1, 1)
```

Interpretation:

- `y` = epistemic agency
- `x` = more convergent/divergent mode

---

## Cognitive inertia

Actions do not directly transform traits. They become accumulated pressure.

```txt
user_threshold  = 2 + floor(u0 / 3)
model_threshold = 2 + floor(m0 / 4)
```

When `|pressure[i]| >= threshold`, the slider advances one unit and pressure is reduced by the threshold amount.

Design consequence:

- one turn does not “fix” a loop
- a good correction can have structural epistemic value without producing immediate visible reconfiguration

---

## Exact preview

Preview is no longer approximate.

The key function is:

- `simulateTurnOutcome()`

It should remain the single source of truth for:

- agency preview
- engagement preview
- pressure preview
- consolidation when `Next turn` is pressed

Maintenance rule:

- never return to separate logic paths for preview and commit

---

## Last-turn memory

Explicit memory of the last committed turn was introduced:

- `lastTurnE`
- `lastTurnU`
- `lastTurnM`

Reason:

- `selE` and `selM` are reset after `advance()`
- patterns and interpretive text still need access to the committed turn context

This affects:

- `detectPattern()`
- `engNote()`
- loop logic in committed state

---

## Engagement

Engagement and epistemic agency are distinct variables and may diverge strongly.

Central example:

- high engagement
- low agency

This models conversational capture or addictive validation.

### Design rule

- **engagement value**: cumulative
- **structural engagement potential**: initial predisposition of the binomial

Do not confuse:

- the real accumulated engagement of the conversation
- the potential engagement of the binomial before turn 1

---

## Structural potential of the binomial

The “Binomial selection” header now shows a structural reading of the system before any turns are simulated.

It is not history.  
It is not an exact prediction of the full dialogue.  
It is an **initial structural reading**.

### Current implementation

It is computed from:

- base values of the active profiles
- `calcStateFromValues(u, m)` for agency potential
- a separate heuristic for engagement potential

Output:

- agency: `favorable / mixed / fragile`
- engagement: `high / mid / low`

### Note

This layer is useful, but more heuristic and less mechanical than turn preview.  
If recalibrated in v2, it should remain clearly distinct from real engagement.

---

## Initial hypothesis of the binomial

`sc_ctx` now covers all user-model combinations.

Current editorial rule:

- at `turn === 0`, the reading is presented as an **initial hypothesis**
- later, the same combination can be read as an observed or sustained dynamic

This avoids overly conclusive wording before turns exist.

---

## Copy constraints

Maintain these rules:

- do not anthropomorphize the model as if it “thinks” in the human sense
- do not present structural tendency as if it were instant change
- do not speak as if the tool diagnoses users
- prefer language of:
  - drift
  - tendency
  - pressure
  - predisposition
  - reorientation

Avoid phrases such as:

- “the user recovers agency” after a single turn
- “the model thinks”
- “the conversation proves” on turn 0

Prefer:

- “tends to restore agency”
- “pushes the system toward”
- “supports more reflective evaluation”
- “initial hypothesis”

---

## Interaction likelihood

Action buttons now display:

- `prob: high`
- `prob: mid`
- `prob: low`

These are not hard restrictions.

They make visible the most probable interaction path given the current binomial state.

### Current implementation

- `scoreUserAction(i)`
- `scoreModelAction(i)`
- `likelihoodClass(score)`
- `likelihoodText(score)`

### Criterion

This is a pedagogical heuristic, not a statistical probability.

It should not be presented as empirical prediction.  
It should be preserved as a structural compatibility cue.

---

## Emergent patterns

Current patterns:

- `confirmation_spiral`
- `certainty_loop`
- `passive_drift`
- `active_resistance`
- `missed_opportunity`
- `active_exploration`
- `cocreation`
- `slow_shift`
- `cognitive_threshold`

They remain second-order descriptors: they describe the system, not the identity of the user.

### Interesting v2 concept still pending

- `captured_metacognition`

Idea:

- metacognitive user
- sycophantic model
- reflection is used to reinforce the loop rather than break it

This should not be implemented hastily if the boundaries are not clear, because it can introduce substantial ambiguity.

---

## Recently confirmed decisions

### Confirmed as correct

- Preview must match consolidation exactly.
- Epistemic impact may be latent rather than immediate.
- Engagement and agency may diverge strongly.
- The binomial should have a prior structural reading.
- Actions may remain available while still showing compatibility/likelihood.

### Deferred for this version

- Expanding the action repertoire aggressively
- Splitting actions like “change frame” into positive/negative subtypes
- Hard-blocking actions except in very justified edge cases

---

## Maintenance risks

### 1. Growth without discipline

The biggest risk is conceptual, not technical:

- too many actions
- too many patterns
- mixing structure, preview, and history

That would break the current clarity.

### 2. Reintroducing preview/commit incoherence

If `pickM()`, `advance()`, or `calcSys()` are changed without also updating `simulateTurnOutcome()`, the old bug can return.

### 3. Over-strong copy

The simulator gets stronger when it talks in terms of tendencies rather than determinate claims.

---

## Suggested v2 order

If v2 is opened, the sensible order is:

1. calibrate weights and thresholds
2. revisit structural binomial potential
3. expand the interaction repertoire
4. add more explainability of the rules
5. run user testing

Do not invert that order.
