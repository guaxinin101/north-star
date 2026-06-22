# North Star — Design Skills for Claude Code

A growing toolkit of **design** skills for Claude Code — conceptual, *target-oriented*
design (the system you intend to build, and why), not as-is documentation.

> A **North Star** is the fixed point you navigate by. This toolkit helps you set and
> keep one for your software: the stable, tech-agnostic design vision the whole system
> points to.

## Skills

| Skill | What it does |
|---|---|
| [`designing-by-altitude`](skills/designing-by-altitude/SKILL.md) | Formalize and maintain a system's conceptual design **by altitude** — a **North Star** (whole system, tech-agnostic, stable) and **subsystem designs** (one block + its contracts) — as living *design-as-context*. Pairs with `superpowers:brainstorming` as the engine; stops above specs/ADRs. |

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
├── skills/
│   └── designing-by-altitude/
│       ├── SKILL.md
│       └── example-north-star.md   # a real, lean North Star (WTO, in Portuguese)
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
