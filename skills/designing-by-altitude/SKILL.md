---
name: designing-by-altitude
description: Use when formalizing or evolving the conceptual TARGET design of a software system or one major block — the intended shape above specs, ADRs and implementation, kept as living design-as-context. Also when a system already exists and you are tempted to document the as-is, or a pragmatic team wants a doc that reflects the real running system. Not for specs, plans, feature slices, or ADRs.
---

# Designing by Altitude

## Overview

Conceptual design has an **altitude** — how far a document sits from the *problem* versus the *technology*. This skill owns the **target** design (where the system is going, never the as-is) at the altitude of **shape**: blocks, roles, and the contracts between them — as living **design-as-context** read at the start of every session.

**The engine is `superpowers:brainstorming`** — it drives the conversation that fills the doc. This skill adds what it lacks: the **altitude**, the **target shape**, the **notation**, and **where the doc lives**.

## The altitude spine

Design is organized by altitude (abstraction), top to bottom:

```
NEED      the problem, before any form     (why, for whom, capabilities)
  ↓ reads
CONCEPT   the mental model of the domain   (ubiquitous language, concepts)
  ↓ reads
SOLUTION  the conceptual form, tech-neutral   ← THIS SKILL (axis: structure)
═══ altitude-stop ═══
[out]     spec · ADR · schema/API · technology · numbers
```

This skill owns the **SOLUTION** layer. It **reads NEED and CONCEPT as input** and distills them; it stops at the altitude-stop. Higher layers get their own skills; until then the North Star distills them inline.

**Zoom is not altitude.** Inside SOLUTION there are two zooms:

| | North Star | Subsystem design |
|---|---|---|
| Zoom | whole system | one block |
| Answers | "where are we going, and why?" | "what is this block's role, and what contracts does it expose?" |
| File | `docs/design/north-star.md` (exactly one) | `docs/design/<name>.md` (N) |

A subsystem is not *lower altitude* than the North Star — it is *smaller in scope*.

## The discipline that fails without this skill: TARGET, not as-is

Baseline testing showed agents already stop at the conceptual altitude and stay lean. The discipline that **does** break: when a system **already exists** and the team is **pragmatic**, agents document the **as-is**.

**Design is the target.** Even with a running system, draw where it is *going*. The existing system is **input and `[LEGACY]`** you cite — never the body of the doc.

| Rationalization | Reality |
|---|---|
| "Pragmatic means documenting the real system" | A target doc that mirrors the as-is rots with the code. The as-is is `[LEGACY]` you point to, not the design. |
| "The team wants what's real, not academic" | The most useful real thing is the *target* every decision steers toward. Mark the as-is only to say what is superseded. |
| "There's a prototype — let's mirror it" | The prototype is as-is. Where it contradicts the target, the target wins; where it's right, that's an ADR, not inertia. |

If you are describing what exists, that is **documentation**, not design — out of scope.

## Form — structured prose with Mermaid diagrams

Agents don't reach for these by default; apply them deliberately. Every doc instantiates the **meta-template** (`templates/meta-template.md`): a header (`Altitude · Axis · Status · Focus-question`) plus seven sections.

- **Prose** carries the soul — purpose, principles, contracts-as-meaning, alternatives, risks, the altitude-stop.
- **Mermaid** carries skeleton and movement, only in the **body of the axis**: structure → `flowchart` + `subgraph`; flow → `sequenceDiagram` / `flowchart`; state → `stateDiagram-v2`.
- In diagrams, **boxes are roles** (not services/classes) and **arrows are intentions** (not calls/signatures) — the altitude-stop applies to the drawing too.

## North Star — the shape

Lean enough to read at the start of every session. It **distills the NEED above** (purpose, principles, the strategic turn) and draws the form:

1. **Purpose + inviolable principles** — what the system is; the rules every decision respects.
2. **Strategy / the turn** — the core bet and why; roads not taken.
3. **Blocks and how they fit** — a **Mermaid** diagram of blocks + contracts (roles, not tech).
4. **Risks / open decisions.**
5. **Decision & legacy map** — pointers to ADRs and subsystem docs; what this supersedes.

## Subsystem design — the shape

**Read the North Star first.** Name the block; stay consistent with it. 1. **Role** · 2. **Internal shape** (Mermaid) · 3. **Contracts exposed** (meaning and protocol, not signatures) · 4. **Alternatives + trade-offs** · 5. **Limitations / open questions**.

## Every doc carries

- **Focus-question** at the top — the single question it answers (two questions → two docs).
- **Status markers:** `[TARGET]` (wanted, unbuilt) · `[DECIDED]` (firmed in an ADR) · `[FRONTIER]` (a bet in research) · `[LEGACY]` (exists, being superseded).
- **Reads the altitude above as input** — SOLUTION reads CONCEPT + NEED; a subsystem reads the North Star.
- **Altitude-stop** — the hard line: describe roles and contracts-as-meaning; the moment you reach for a field, signature, schema, wire format, concrete technology, or a latency/throughput number, you have left this altitude. Leave a pointer (ADR/spec), not the detail.

## Where they live (required)

1. `docs/design/north-star.md` — exactly one, required, the top of the tree.
2. `docs/design/<name>.md` — subsystem attachments (add one when a block earns its own doc).
3. A `## Design` section in the project root **`CLAUDE.md`** — ordering the agent to read the North Star first (design-as-context).

## Common mistakes (from baseline testing)

| Mistake | Fix |
|---|---|
| Documenting the as-is because the team is "pragmatic" | Draw the target; the as-is is `[LEGACY]` you cite. |
| ASCII/prose only, no diagrams | The body of the axis is Mermaid; boxes = roles, arrows = intentions. |
| Mixing altitudes in one doc without naming them | This doc is SOLUTION; distill NEED/CONCEPT at the top, point down for the rest. |
| Diagram drifts into signatures/schema/tech | Stop at the altitude-stop; that detail is an ADR/spec. |
| Decisions stated without the alternatives | Show the roads not taken, and why. |
| Doc too long to read as context | Keep it lean; push detail down. |

## Example

`example-north-star.md` (this directory) — a real, lean North Star (the WTO project, in pt-BR).
