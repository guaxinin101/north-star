---
name: designing-by-altitude
description: Use when formalizing or evolving the conceptual design of a software system — the intended target or vision, not the as-is — for the whole system (a North Star) or for one major block (a subsystem design). Triggers include starting a project's architecture, adding a major component, rethinking the system's shape above the spec/implementation level, or keeping a living architecture vision as session context. Not for specs, plans, feature slices, ADRs, or documenting what already exists.
---

# Designing by Altitude

## Overview

Conceptual design lives at **fixed altitudes**. This skill owns exactly **two artifacts**, both describing the **target** (where the system is going), never the as-is:

- **North Star** — the whole system, conceptual, tech-agnostic, stable.
- **Subsystem design** — one block: its role and the contracts it exposes.

Everything **below** them — stack/API/deploy decisions, feature slices, implementation — is *not* this skill. Those are ADRs and the `superpowers` spec → plan → code flow.

**The engine is `superpowers:brainstorming`.** It drives the conversation that fills any of these docs; this skill adds what it lacks — the *altitude*, the *target shape* of each doc, and *where it lives*.

- **When open questions remain that only your human partner can settle** → gather with `superpowers:brainstorming` (one question at a time, verification echo) before drafting.
- **When the input is already specified** → state your premises explicitly at the top of the doc and draft. Don't stage a ritual interview over settled facts.

## When to use / not

- **Use:** the system's overall conceptual shape, or one block's role + contracts, **above** the spec.
- **Not:** a feature/slice → `superpowers:brainstorming` → spec. A stack/tech decision → an **ADR**. Describing something that already exists → that's *documentation*, not design.

## The two altitudes

| | North Star | Subsystem design |
|---|---|---|
| **Scope** | whole system | one block |
| **Answers** | "where are we going, and why?" | "what is this block's role, and what contracts does it expose?" |
| **Tech** | agnostic | near-agnostic (structural roles, not APIs) |
| **File** | `docs/design/north-star.md` (exactly one) | `docs/design/<name>.md` (N of them) |
| **Stops before** | naming stacks/schemas | field-level APIs, schemas, latency numbers |

## Where they live (convention — required)

1. `docs/design/north-star.md` — **exactly one**, **required**, the top of the tree.
2. `docs/design/<name>.md` — subsystem designs, **attachments** (add one when a block earns its own doc).
3. A `## Design` section in the project root **`CLAUDE.md`** — **required** — short, ordering the agent to read `docs/design/north-star.md` first (design-as-context). It lists the attachments but does not restate them.

## North Star — the shape

Lean enough to be read at the start of every session. Ordered parts:

1. **Purpose + inviolable principles** — what the system is; the rules every decision must respect.
2. **Strategy / the turn** — the core bet and *why*; alternatives weighed, roads not taken.
3. **Blocks and how they fit** — a diagram of the blocks + the contracts (the arrows) between them. Roles, not tech.
4. **Risks / open decisions** — what you now own; what is still unproven.
5. **Decision & legacy map** — pointers to ADRs and to the subsystem docs; what this supersedes.

## Subsystem design — the shape

**Read the North Star first** — it is the input; name the block you are zooming into and stay consistent with it. Ordered parts:

1. **Role** — what this block is responsible for inside the North Star.
2. **Internal shape** — the conceptual pieces inside and how they relate (no implementation).
3. **Contracts exposed** — what flows in/out, as *meaning and protocol*, not signatures.
4. **Alternatives + trade-offs** — the structural choices weighed.
5. **Limitations / open questions.**

**Altitude stop — the hard line.** Describe roles, responsibilities, and contracts-as-meaning. The moment you reach for a **struct field, a function signature, a wire format, a database schema, a concrete technology, or a latency/throughput number**, you have left this altitude. That detail belongs to an **ADR** (if it's a decision) or a **spec** (`superpowers`, if it's a slice). Leave a pointer, not the detail.

## Every doc carries

- **Status markers:** `[TARGET]` (wanted, not built) · `[DECIDED]` (firmed in an ADR) · `[FRONTIER]` (a bet still in research) · `[LEGACY]` (exists, being superseded).
- **Alternatives with trade-offs**, not only the chosen path.
- A **Limitations / Risks** section.
- It **reads the one above as input** — subsystem ← North Star; the North Star reads nothing, it is the top.

## Maintaining (create / update)

- **New system** → write `north-star.md` + the `CLAUDE.md` section.
- **New major block** → add `docs/design/<name>.md`; link it from the North Star's blocks section.
- **A decision lands (ADR) or reality shifts** → revise the affected doc deliberately and flip its status markers. The North Star is a *living point*, not a frozen relic — you don't append, you re-settle it.

## Common mistakes (from baseline testing)

| Mistake | Fix |
|---|---|
| Doc too long to read as context | Keep it lean; push detail down to ADR/spec. |
| Subsystem doc drifts into API fields, schemas, latencies | Below this altitude → ADR/spec. State the contract's *meaning*. |
| Decisions stated without the alternatives | Show the roads not taken, and why. |
| Subsystem written without reading the North Star | Read it first; name and cite the block. |
| Writing the as-is | Design is the *target*. If it already exists, it's documentation — out of scope. |

## Example

`example-north-star.md` (this skill's directory) is a real, lean North Star — the author's WTO project, in Portuguese. It is the canonical shape for altitude 1: ~5 sections, a block diagram, status markers, alternatives, risks, a decision/legacy map, and zero stack choices.
