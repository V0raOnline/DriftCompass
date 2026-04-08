# DriftCompass

**Epistemic agency simulator in human-AI interaction**

Bilingual ES/EN · No backend · No dependencies · Single HTML file

---

## Core question

> Does the user leave this conversation more able to think for themselves, or less?

DriftCompass visualizes how the interaction between a user profile and a model profile affects two distinct dimensions:

- **Epistemic agency**: the capacity to evaluate, revise, and maintain independent judgment.
- **Engagement**: the degree of conversational pull, attachment, or continuity.

The core thesis is that **fixing only the model's output is not enough**. The dynamic depends on the whole system: user, model, content type, and accumulated inertia.

---

## What the current version includes

### Binomial selection

The top section is no longer framed as “detailed configuration”, but as **Binomial selection**:

- active selection `User + Model`
- **structural potential of the binomial**
  - potential agency
  - potential engagement
- **initial hypothesis** for the selected combination
- detailed editing through profiles and sliders

When the panel is collapsed, only these remain visible:

- the active selection
- the structural potential of the binomial

### Structural potential of the binomial

Before the turn-based simulation starts, DriftCompass shows an initial structural reading of the selected binomial.

This is not an observed result and not real accumulated engagement. It is a **structural predisposition of the system**:

- agency: `favorable / mixed / fragile`
- engagement: `high / mid / low`

This makes it possible to distinguish clearly between:

- **structural potential**
- **observed turn-by-turn trajectory**

### Guided simulation

Each turn keeps the same three-step flow:

1. **Premise type**
2. **User says**
3. **Model responds**

Selecting the model response triggers an **exact preview** of the state that will be committed when `Next turn` is pressed.

### Exact preview

Preview and consolidation now share the same transition function.

That means choosing a model response previews:

- agency shift
- probable system state
- expected engagement for the turn
- expected pressure after the interaction

`Next turn` does not introduce a second hidden result. It only confirms the already-previewed state, records it in history, and advances the turn.

### Cognitive inertia

Actions do not transform sliders directly. They accumulate **pressure**.

A trait only shifts when pressure crosses a threshold:

```txt
user_threshold  = 2 + floor(rigidity / 3)
model_threshold = 2 + floor(validation / 4)
```

This models slow, latent change:

- a rigid user does not change in one turn
- a factual correction does not, by itself, break a validation loop

### Binomial contexts

All user-model combinations now have their own contextual reading.

On turn 0 they are shown as **initial hypotheses**, not as already-observed diagnoses.

Once turns accumulate, the contextual reading coexists with:

- the compass state
- turn-level insights
- emergent patterns

### Interaction likelihood

User and model action buttons now display a lightweight likelihood cue:

- `prob: high`
- `prob: mid`
- `prob: low`

This does not block actions. It makes visible which interaction path is more probable given the current profile.

That strengthens the pedagogical role of the sliders: they affect the space of behavior, not only the final outcome.

---

## Conceptual model

### Y axis: epistemic agency

- **↑ Growing agency**: the user gains capacity to evaluate and revise.
- **→ Neutral**: the conversation does not substantially change their epistemic agency.
- **↓ Agency loss**: the user leaves more dependent, more biased, or with a worse mental model.

The ideal is not the center. It is sustained upward drift, or at least neutrality.

### Engagement

Engagement and epistemic agency are distinct variables and can diverge.

There may be:

- high engagement with low agency
- low engagement with high agency
- joint growth
- joint deterioration

The most important case for DriftCompass is:

- **high engagement**
- **low agency**

That models conversations that are highly absorbing while still epistemically degrading.

---

## How it works

### User profiles

- Validation loop
- Open user
- Low energy
- High rigidity
- Metacognitive

### Model profiles

- Sycophant
- Corrects only
- With metacognition
- Adaptive friction
- Neutral model

### Adjustable variables

User:

- Rigidity
- Openness
- Loop
- Energy

Model:

- Validation
- Friction
- Metacognition
- Precision

### Premise type

- Factual true
- Factual false
- Opinion
- Unfalsifiable

Premise type modulates the epistemic effect of the model response.

---

## Patterns and system reading

DriftCompass detects emergent patterns after several turns, such as:

- confirmation spiral
- certainty loop
- passive drift
- active resistance
- missed opportunity
- active exploration
- co-creation
- slow shift
- cognitive threshold

These patterns describe **system behavior**, not user identity.

---

## Project status

This version already includes:

- reordered binomial selection section
- structural potential of the binomial
- exact preview-to-commit logic
- last-turn memory for patterns and engagement
- complete contexts for all combinations
- softer and less anthropomorphic copy
- visual likelihood indicator for interaction options

It remains a heuristic simulator, not an empirically validated model.

---

## Explicit limits

- It does not diagnose.
- It does not evaluate real people.
- It is not a clinical psychology tool.
- It does not attribute human-style thinking to the model.
- The weights are heuristic and pedagogical.
- It shows direction and structure of dynamics, not exact measurement of the world.

---

## Reasonable roadmap

### v1 closed

- stabilize copy
- refine visual calibration
- document rules and assumptions

### v2

- richer interaction repertoire
- stronger contextual sensitivity by binomial
- calibration and user testing
- semi-automatic or real conversation analysis

---

## Structure

```txt
/
├── DriftCompass.html
├── README.md
├── README_EN.md
├── NOTAS_DEV.md
├── NOTAS_DEV_EN.md
├── CHANGELOG.md
├── CHANGELOG_EN.md

```

No build step. No server required. Open `DriftCompass.html` in a browser or publish through GitHub Pages.

---

## Credits

Developed by [V0ra](https://v0raonline.substack.com) as part of the Codexsfera project.

*This simulator does not diagnose, evaluate, or judge. It shows a dynamic.*
