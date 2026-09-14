# interface-craft

A Claude skill for designing product UI that looks like a real designer made it.

Most AI-generated interfaces fail in the same five ways. This skill names them,
imposes an order of operations that makes them hard to commit, and ends in a
checklist that can actually return "no."

It encodes the discipline behind Linear, Shopify Polaris, Flighty, and Apple's
HIG — not their colours, their **structure**.

## The core idea

When something needs to read as *more*, *worse*, or *different*, there's a
hierarchy of channels available. Use the highest one that can carry it:

| # | Channel | |
|---|---------|---|
| 1 | **Order** | The worst item goes first. Costs nothing, always legible. |
| 2 | **Grouping** | Sections and whitespace; a count in the header. |
| 3 | **Type weight & size** | The number that matters is big. Nothing else is. |
| 4 | **Glyph** | Linear's four-bar priority mark. Achromatic, tiny, learnable. |
| 5 | **Achromatic value** | muted → graphite → ink. Four steps before any hue. |
| 6 | **Hue** | Last. Smallest scale. One or two values, never a ramp of five. |

Most bad interfaces start at 6. Most good ones never get past 3.

Reach for colour first and you get rainbow category chips, orange→red severity
ramps, and hashed label hues — decoration that reads as decoration, because the
information was already available in a channel you skipped.

## What's in it

- **Five failure modes**, written to be self-diagnosed against
- **An order of operations** — job → inventory → hierarchy → build → verify → subtract
- **Reference anatomy** for Linear, Shopify, Flighty and Apple, with real
  structure and numbers, so "copy it" is checkable
- **Colour discipline**, including a calibration list of the looks that show up
  regardless of subject
- **Type, layout, motion and copy** rules
- **A completeness contract** — no decorative buttons, every state built
- **Verification by breaking the guard**, not by green checks
- **Codebase binding** — lift exact tokens from the repo rather than inventing a
  palette, and let a project's own `DESIGN.md` outrank the skill

## Install

**Claude Code — all your projects:**

```bash
git clone https://github.com/deanayoung3-droid/interface-craft.git ~/.claude/skills/interface-craft
```

**One project only:**

```bash
git clone https://github.com/deanayoung3-droid/interface-craft.git .claude/skills/interface-craft
```

Restart Claude Code, then invoke it with `/interface-craft`, or just ask for UI
work — the description is written so it triggers on its own.

**Claude.ai / Desktop:** upload `SKILL.md` as a custom skill.

## Project overrides

The skill defers to the repo. If a project has a `DESIGN.md`, `.claude/DESIGN.md`,
or a design section in `CLAUDE.md`, that outranks the skill wherever they
disagree — project rules are decisions someone already made and defended.

A project override is the right place for your tokens, your banned list, and the
specific things you've told Claude three times already.

## Licence

MIT
