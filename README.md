# North Star — Design Skills for Claude Code

A growing toolkit of **design** skills for Claude Code — conceptual, *target-oriented*
design (the system you intend to build, and why), not as-is documentation.

> A **North Star** is the fixed point you navigate by. This toolkit helps you set and
> keep one for your software: the stable, tech-agnostic design vision the whole system
> points to.

## Skills

| Skill | What it does |
|---|---|
| [`framing-the-need`](skills/framing-the-need/SKILL.md) | Frame the **NEED** layer — the **problem before any form**: why the system exists, for whom, the **capabilities and outcomes** it must deliver, and the **system as a black box** at its boundary (vision/PR-FAQ, impact map, boundary capabilities). The top of the spine — read by CONCEPT and SOLUTION. Discipline: stay at the problem; never descend into modules, services, APIs or screens. One black-box `flowchart`. |
| [`modeling-the-domain`](skills/modeling-the-domain/SKILL.md) | Capture the **CONCEPT** layer — a domain's **ubiquitous language**, its concepts and relations, and the **invariants** that always hold — as living *design-as-context* the SOLUTION layer reads. Per bounded context, with a polysemy table for cross-context terms. Discipline: stay at the knowledge level, never schema or services. `classDiagram` (not `erDiagram`). |
| [`designing-by-altitude`](skills/designing-by-altitude/SKILL.md) | Formalize and maintain a system's conceptual **target** design **by altitude** (abstraction: NEED → CONCEPT → SOLUTION). Owns the **SOLUTION** layer — a **North Star** (whole system) and **subsystem designs** (one block + its contracts) — as living *design-as-context*, written as **structured prose with Mermaid diagrams**. Discipline: target, not as-is. Pairs with `superpowers:brainstorming`; stops above specs/ADRs. |
| [`narrating-the-flow`](skills/narrating-the-flow/SKILL.md) | Describe the **flow** axis — how the system behaves over **time**: a flow end to end, the **lifecycle** of one entity, or the **chain of domain events**. The companion of structure within SOLUTION (the same roles, in motion). Discipline: stay at the conceptual movement — never service calls, an enum/`status` column, or Kafka topics/schemas. `sequenceDiagram` / `stateDiagram-v2` / `flowchart` (boxes = roles, arrows = intentions/happenings). |

_More design skills will join this toolkit over time._

## Install

```text
/plugin marketplace add guaxinin101/north-star
/plugin install north-star@north-star
```

Skills are then invoked namespaced by the plugin: `/north-star:designing-by-altitude`.

## Develop locally (no publishing needed)

From this repo's root:

```text
claude --plugin-dir .
```

Then invoke `/north-star:designing-by-altitude`. Edit a `SKILL.md`, re-run, iterate.
To validate the structure before pushing:

```text
claude plugin validate .
```

## Layout

```text
north-star/
├── .claude-plugin/
│   ├── marketplace.json     # this repo as a marketplace (lists the plugin)
│   └── plugin.json          # the plugin manifest (name, version, license)
├── skills/                  # by altitude layer, plus the flow axis (each: SKILL.md + example)
│   ├── framing-the-need/        # NEED — the problem, before any form
│   ├── modeling-the-domain/     # CONCEPT — ubiquitous language + domain model
│   ├── designing-by-altitude/   # SOLUTION · structure — North Star + subsystem designs
│   └── narrating-the-flow/      # SOLUTION · flow — narrative, lifecycle, domain events
├── templates/
│   └── meta-template.md     # the common anatomy every skill instantiates
├── docs/design/toolkit.md   # the toolkit's own design, organized by altitude
├── README.md
└── LICENSE
```

## Conventions this toolkit assumes

- Design docs live in `docs/design/` of the consuming project: `north-star.md` (one,
  required) + `<block>.md` attachments.
- A `## Design` section in the project's `CLAUDE.md` points the agent to read the
  North Star first (design-as-context).

## License

[MIT](LICENSE) © 2026 gg
