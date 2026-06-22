---
name: mapping-the-journey
description: Use when mapping a user's experience over time — a customer journey or a service blueprint, outside-in. Covers the stages, what the user does, thinks and feels, the touchpoints, the pains and the moments that matter. Also when the map is pressured to get concrete and turn into UI screens, wireframes, a click-flow, or named systems and APIs. Not for screen designs, wireframes, the system's internal flow, named services, specs or ADRs.
---

# Mapping the Journey

## Overview

This skill owns the **experience** axis — a user's experience over time, **outside-in**: a **customer journey** (the stages, what the user does, thinks and **feels**, the touchpoints, the pains and the moments that matter) or a **service blueprint** (the same journey plus the layers that sustain it). It works at the level of **lived experience and meaning**, never UI screens or named systems — as living **design-as-context**.

**The engine is `superpowers:brainstorming`.** This skill adds the altitude (experience), the target shape, the notation, and the discipline.

## Where this sits — the experience axis (outside-in)

```
NEED  the problem + the user's experience that motivates it   ← the journey anchors here
  ↓
CONCEPT → SOLUTION ...
```

The journey is **user-centric** (outside-in): what the user lives. It is the **complement** of `north-star:narrating-the-flow`, which is **system-centric** (roles + intentions, inside-out). The journey **anchors in NEED** (the experience and pains inform the problem); a **service blueprint** extends it toward SOLUTION — the backstage that sustains the experience, as meaning, pointing to `narrating-the-flow`. Every doc instantiates the **meta-template** (`templates/meta-template.md`).

## The discipline that fails: stay in the experience

Baseline testing was consistent: the experience layers (stages, emotion, pains) already come through — but under pressure to be **concrete** ("we'll prototype in Figma", "name the backstage systems"), agents **descend into the UI** (screens, fields, components, a click-flow) and, in a blueprint, into **named systems** (OMS, ERP, PSP, the APIs).

A journey is **what the user lives, needs and feels**, and the **touchpoints as meaning**. *The patient looks for a way to book; anxiety while waiting; relief at "confirmed"* = journey. *A search screen with a card, a CPF field, OMS + an API* = you crossed into UI/SOLUTION.

| Rationalization | Reality |
|---|---|
| "The team wants the screens and the UI flow, ready to prototype in Figma" | A journey is the experience, not its UI. A touchpoint is a point of contact as meaning ("the patient looks for a way to book"), not a screen with a card and fields. Screens, wireframes and the click-flow are a UX/UI spec — point down. |
| "It's a blueprint — name the backstage systems (OMS, ERP, the PSP, the APIs)" | The backstage is the **roles and activities** that sustain the experience, as meaning; which systems realize them is SOLUTION/spec. Name "inspect the item at the warehouse", not "WMS + an API". |
| "Make it actionable — list the screens to design" | The actionable thing here is the experience and the **moments of truth** (the pains, the emotion, where it is won or lost). The screen list is the next step (UI design), not the journey. |

If you are naming a screen, a field, a component, a click-flow, Figma, or a concrete system/API, you have left the experience.

## Customer journey vs service blueprint

| Form | Answers |
|---|---|
| **Customer journey** | what the user lives across stages — does · thinks/feels · touchpoint · pain/opportunity · moment of truth (outside-in) |
| **Service blueprint** | the same journey + the layers that sustain it — **frontstage** (what the user sees) · *line of visibility* · **backstage** (the roles/activities behind it) · **support** — as meaning |

Use a journey to understand and align on the experience; a blueprint when you also need to show how the organization sustains it (without drawing the systems).

## Form — structured prose with a journey table

- The journey is mostly a **table by stage**: *stage · does · thinks/feels · touchpoint · pain/opportunity*, plus the **emotional curve** and the **moments of truth**. Optionally a Mermaid `journey` diagram for the emotional arc.
- **Touchpoints are points of contact as meaning** (channel + intention), not screens.
- A **blueprint** adds the three lines (interaction · visibility · internal interaction); **backstage = roles/activities**, never systems/APIs.
- **Never** screens, wireframes, fields, a click-flow or Figma; **never** named systems/APIs/stack — those are UX or SOLUTION specs.

## The shape

- **Customer journey** — persona + goal · the stages, each as does / thinks-feels / touchpoint / pain · the emotional curve · the **moments of truth** (where the experience is won or lost).
- **Service blueprint** — the journey's frontstage, then backstage roles/activities and support, separated by the lines — the meaning of how the experience is sustained, pointing to `narrating-the-flow` for the system's movement.

## Every doc carries

Focus-question · status markers `[TARGET]/[DECIDED]/[FRONTIER]/[LEGACY]` · **reads the NEED above** (the experience informs the problem) · the **altitude-stop**. See the meta-template.

## Where they live (convention)

- `docs/design/journey-<persona-or-scenario>.md` (journey) · `docs/design/blueprint-<service>.md` (blueprint).
- Reads the need (`framing-the-need`); a blueprint's backstage points to `narrating-the-flow` and the North Star.

## Common mistakes (from baseline testing)

| Mistake | Fix |
|---|---|
| "Screens / UI flow" per stage (cards, fields, a Figma flow) | A touchpoint is a point of contact as meaning; the screen is a UX/UI spec — point down. |
| Blueprint backstage as named systems (OMS, ERP, PSP, APIs) | Backstage = roles and activities (meaning); which system realizes them is SOLUTION/spec. |
| A "screens to design (MVP)" list | That is the next step (UI design), not the journey. |
| Losing the user's point of view (it becomes the system's flow) | The journey is outside-in — does / thinks / feels / touchpoint; the system's movement is `narrating-the-flow`. |
| No emotion / no moments of truth | The emotional curve and the moments that matter are the point; without them it is a flowchart. |
| Click-flow / wireframes | Stop at the experience; the wireframe is a UX spec. |

## Example

`example-journey-claim.md` (this directory) — a lean customer journey of the **segurado** filing a claim (insurance, in pt-BR): the experience (anxiety → uncertainty → relief/frustration), the outside-in complement of the system-centric `claim-lifecycle` in `narrating-the-flow`.
