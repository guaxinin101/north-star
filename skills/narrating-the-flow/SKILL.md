---
name: narrating-the-flow
description: Use when describing how a system behaves over time — a flow end to end, the lifecycle of one entity, or the chain of domain events. The conceptual movement, not the wiring. Also when a flow, state machine or event doc is pressured to get technical and turn into service calls, an enum/status column, or Kafka topics and message schemas. Not for sequence diagrams of API calls, state columns, message contracts, BPMN, specs or ADRs.
---

# Narrating the Flow

## Overview

This skill owns the **flow** axis — how the system **behaves over time**: a **flow** end to end, the **lifecycle** of one entity, or the **chain of domain events**. It is the companion of structure: the same roles, now **in motion**. It works at the **conceptual level** (meaning over time), never the wiring — as living **design-as-context**.

**The engine is `superpowers:brainstorming`.** This skill adds the altitude (conceptual flow), the target shape, the notation, and the discipline.

## Where this sits — an axis, not a layer

```
NEED → CONCEPT → SOLUTION ─── altitude-stop ─── spec · ADR · code · schema · topics
                    │
                    ├─ structure (north-star:designing-by-altitude) — the static shape
                    └─ flow      ← THIS SKILL — the same shape in motion, over time
```

FLOW is an **axis within SOLUTION**, not a new layer. It **reads the structure (North Star / subsystem) above** and borrows the **ubiquitous language** (`north-star:modeling-the-domain`) for its situations and facts. Zoom is free — a whole-system narrative or one entity's lifecycle. Every doc instantiates the **meta-template** (`templates/meta-template.md`).

## The discipline that fails: stay at the conceptual flow

Baseline testing was unambiguous: asked to describe a flow, a lifecycle, or domain events, agents **descend into implementation in all three forms** — even under mild pressure. The flow doc must stay at the **conceptual movement**: roles, intentions, business situations, and facts of the domain over time — never the wiring that realizes them.

A flow describes **what happens and why, in what order**. *A role needs something from another role; an entity moves from one business situation to another because a domain fact occurred* = FLOW. *A service calls another service; a `status` column flips; a message lands on a topic* = you crossed into SOLUTION/spec.

| Rationalization | Reality |
|---|---|
| "The team will implement the state machine — make it concrete and ready to code" | The conceptual lifecycle (the business situations and what moves between them) is what they implement against. A state is a situation of meaning, not an `enum`; a transition is a domain happening, not a method `(state,event)->state` or a `status` column. Name the situation; the enum/columns/fields are the spec. |
| "The team is technical — detail the calls between the services" | A flow's boxes are **roles** and its arrows are **intentions** (who needs what from whom, and why), not services and method calls. `Inventory.hold(...)`, webhooks, sagas, TTLs and retries are wiring — an ADR/spec, not the flow. |
| "We'll use Kafka — list the topics and message schemas" | A domain event is a **business fact in the past** (what happened), not a Kafka message. Topics, partitions, envelopes, schemas and DLQs are the realization — point down to them; here name the fact and what it sets in motion. |

If you are naming a method, an endpoint, an infra service, a topic/queue, a field/type, a `status` column, or a messaging pattern, you have left this altitude.

## Which of the three — the boundary between them

Three forms answer "how it happens" from different angles. **One question per doc**; pick by the angle:

| Form | Answers | Notation |
|---|---|---|
| **Flow narrative** | how one end-to-end scenario unfolds across several roles (an interaction / journey) | `sequenceDiagram` (roles) or `flowchart` (process) |
| **State / lifecycle model** | the situations one entity passes through, and what moves it | `stateDiagram-v2` |
| **Domain event flow** | the chain of business facts that propagate and trigger reactions (often across contexts) | `flowchart` |

A single end-to-end scenario → narrative; one thing that changes situation over time → states; a chain of facts and their reactions → events.

## Form — structured prose with Mermaid

- In every diagram, **boxes are roles** and **arrows are intentions / happenings** (not calls, signatures or messages) — the altitude-stop applies to the drawing.
- **Flow narrative** → `sequenceDiagram` between roles (the messages are intentions — "reserves a room", "asks to confirm" — not `POST /reservations`), or a `flowchart` for a process.
- **State model** → `stateDiagram-v2`; states are business situations (*Reserved*, *No-show*), transitions are domain happenings (*guest cancels*), never methods or a `status` enum.
- **Event flow** → `flowchart` of facts in causal order (`Pedido feito --> Pagamento confirmado --> Entrega despachada`).
- **Never BPMN / executable process** — that is drawn to become runnable; it is below the altitude (toolkit §6 boundary).

## The shape

Each artifact is lean and instantiates the meta-template:

- **Flow narrative** — the roles, then the scenario as an ordered exchange of **intentions**, plus the main alternate paths (told as meaning, not error codes).
- **State / lifecycle model** — the **situations** one entity passes through and the **domain happenings** that move it; the invariants on the moves (e.g. a terminal situation has no exit).
- **Domain event flow** — the **facts** (past tense) in causal order, who raises each and who reacts — meaning, not message contracts.

## Every doc carries

Focus-question · status markers `[TARGET]/[DECIDED]/[FRONTIER]/[LEGACY]` · **reads the structure above** (North Star / subsystem) as input · the **altitude-stop**. See the meta-template.

## Where they live (convention)

- `docs/design/flow-<scenario>.md` (narrative) · `docs/design/<entity>-lifecycle.md` (states) · `docs/design/events-<process>.md` (events).
- Read alongside the North Star (structure) and the domain model (the situations and facts speak its ubiquitous language).

## Common mistakes (from baseline testing)

| Mistake | Fix |
|---|---|
| States as an `enum`/`status` column + entity fields/schema | States are business situations; the enum and columns are the spec. Name the situation and the domain happening that moves it. |
| A transition written as `(state, event) -> state` or a method/setter | That is the implementation; describe the **happening** that causes the move and the situation it lands in. |
| Narrative as calls between named services (`Inventory.hold(...)`, webhooks, sagas, TTLs) | Boxes are roles, arrows are intentions; the calls and infra patterns are an ADR/spec. |
| Events as Kafka topics with schemas/envelopes/partitions/DLQs | Events are domain facts in the past; topics/schemas are the realization — point down. |
| Mixing all three forms in one doc | One question per doc; pick narrative / states / events by the angle. |
| Drifting into BPMN / an executable process | Stop above it; that is built to run (an ADR/spec). |

## Example

`example-claim-lifecycle.md` (this directory) — a real, lean **state/lifecycle** model (the *Sinistro* of the insurance domain, in pt-BR), states as business situations and transitions as domain happenings — the same domain `modeling-the-domain` models as concepts, here in motion.
