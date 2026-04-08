# DriftCompass - Changelog

## v0.6.0 - 2026-04-07

### Interface reorganized around the binomial

- The top section moves from “Detailed configuration” to **Binomial selection**.
- The visible header now shows:
  - `User + Model`
  - active selection
  - **structural potential of the binomial**
- When collapsed, the structural summary and active selection remain visible.
- The initial hypothesis and detailed configuration move inside the expandable body.

### Structural potential of the binomial

- Adds an initial structural reading separated from the real accumulated state.
- Two indicators are shown:
  - potential agency
  - potential engagement
- Introduces qualitative labels:
  - agency: `favorable / mixed / fragile`
  - engagement: `high / mid / low`

### Exact turn preview

- Preview and consolidation are unified through `simulateTurnOutcome()`.
- Selecting the model response previews exactly the state that will be committed when the turn advances.
- Preview now includes:
  - agency
  - engagement
  - expected pressure
  - system state

### Last-turn memory

- Adds:
  - `lastTurnE`
  - `lastTurnU`
  - `lastTurnM`
- Patterns and engagement interpretation no longer depend only on ephemeral selections reset after `advance()`.

### Binomial contexts

- Missing combinations in `sc_ctx` are completed for ES and EN.
- On turn 0, contexts are presented as **initial hypotheses**.
- Combinations no longer fall through to silence.

### Copy and system tone

- Text is revised to reduce overly conclusive wording.
- Insights shift toward:
  - structural tendency
  - drift
  - epistemic pressure
- Anthropomorphic wording is reduced in sensitive cases.

### Visual interaction likelihood

- Adds a lightweight compatibility/likelihood indicator to user and model actions:
  - `prob: high`
  - `prob: mid`
  - `prob: low`
- Uses subtle border/opacity reinforcement.
- Does not block actions; it reveals the most probable path through the system.

### Cleanup and polish

- Fixes mojibake in the main HTML.
- Improves alignment in the binomial summary header.
- Normalizes visual reading between structural summary and active simulation.

---

## v0.5.0 - 2026-04-04

### Expanded log and scenario separators

- `log-panel` uses space more effectively.
- Adds scenario separators to the log:
  - initial scenario
  - binomial change
- Removes the previous short cap on log entries.

---

## v0.4.0 - 2026-04-04

### Combinable scenarios

- Introduces independent user and model profiles.
- Selection becomes additive rather than based on fixed scenario presets.
- Adds dynamic context by active combination.
- Reworks interface sections and top banner.

### Epistemic agency as Y axis

- The Y axis explicitly becomes epistemic agency.
- Labels and insights are rewritten around that question.

---

## v0.3.0 - 2026-04-04

### Cognitive inertia

- Actions stop moving sliders directly.
- Independent pressure buffers are introduced for user and model.
- Thresholds are tied to rigidity and validation.
- Pressure bars appear in the interface.

### Turn preview

- Model response selection shows a ghost point and dashed line.
- Probable state is visualized before confirmation.

### Engagement modulated by user openness

- Open user + useful friction can raise engagement.
- User in loop + friction can lower engagement.
- Low energy dampens effects in both directions.

---

## v0.2.0 - 2026-04-03

### Epistemic premise type

- Adds mandatory step 0.
- Introduces four premise types:
  - factual true
  - factual false
  - opinion
  - unfalsifiable
- The epistemic matrix modulates agency, engagement, and insight.

### Guided sequential flow

- Orders simulation into steps 0 → 1 → 2 → turn.
- Each step unlocks the next.

---

## v0.1.0 - 2026-04-03

### Initial phase 1

- Two-agent simulator with independent sliders.
- Compass with accumulated trajectory.
- Cross-feedback between model actions and user state.
- Initial fixed scenarios.
- Contextual insights.
- Hot ES/EN language switching.
