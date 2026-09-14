<div align="center">

# interface-craft

**A Claude skill for building product UI that looks like a real designer made it.**

Most generated interfaces fail in the same five ways.<br/>
This names them, makes them hard to commit, and checks for them before handover.

<sub>

[![License: MIT](https://img.shields.io/badge/License-MIT-1a1a1c.svg?style=flat-square)](LICENSE)
[![Claude Skill](https://img.shields.io/badge/Claude-Skill-4285f4.svg?style=flat-square)](https://docs.claude.com/en/docs/claude-code/skills)
[![Works anywhere](https://img.shields.io/badge/Code%20·%20Desktop%20·%20Web-5c5c66.svg?style=flat-square)](#install)

</sub>

</div>

---

## The problem

Ask a model for a dashboard and you get a dashboard. It renders, it's
responsive, the code is clean — and it looks generated. Ask why and you get
vague answers about taste.

It isn't taste. It's five specific, diagnosable mistakes, and the biggest one is
this: **reaching for colour to encode meaning.**

Something means *worse*, so it gets a red chip. Something means *different*, so
it gets a hue derived from its label. Something means *more*, so it gets a
five-step ramp. The result reads as decoration, because it is — the information
was already available in a channel that got skipped.

## The core idea

When something needs to read as *more*, *worse*, or *different*, there's a
hierarchy of channels available. **Use the highest one that can carry it.**

| | Channel | What it looks like |
|:--|:--|:--|
| **1** | **Order** | The worst item goes first. Costs nothing, never ambiguous. |
| **2** | **Grouping** | Sections with real space between them; a count in the header. |
| **3** | **Type weight & size** | The number that matters is big. Nothing else is. |
| **4** | **Glyph** | A small four-bar mark for priority. Achromatic, learned once. |
| **5** | **Achromatic value** | muted → graphite → ink. Four legible steps before any hue. |
| **6** | **Hue** | Last. Smallest scale. One or two values — never a ramp of five. |

> **Most bad interfaces start at 6. Most good ones never get past 3.**

## What that changes

A severity list, encoded at level 6 — hue first:

```
● Critical   Checkout button below the fold     ▓▓▓▓▓
● High       Signup form asks 11 fields         ▓▓▓▓░
● Medium     Hero copy doesn't say what we do   ▓▓░░░
● Low        Footer links are 11px              ▓░░░░
```

Four coloured pills, a legend to learn, and a decorative bar repeating what the
pill already said. The pale amber is about 2:1 on white — unreadable the moment
someone reuses it for a numeral.

The same list, encoded at levels 1–3, with one hue held in reserve:

```
Checkout button below the fold                    87
Signup form asks 11 fields                        64
Hero copy doesn't say what we do                  41
Footer links are 11px                             22
```

Sorted worst-first, so rank carries severity for free. The top figure is
heavier and larger, so the eye lands there first. **One** red, on `87` alone,
because that's the only one that's actually urgent. No legend. And the real
numbers survive — `64` and `41` read differently, where a badge would have
bucketed both to "medium."

Same information. Less ink, no legend, more precision.

## The five failure modes

The skill is built around these, written so they can be self-diagnosed.

| | Failure | The tell |
|:--|:--|:--|
| **F1** | **Designing a screen, not a workflow** | Starts at "what does this look like," never "what does this person do next." With no job defined, there's no principle for excluding anything — which is the real source of clutter. |
| **F2** | **Copying the chrome, inventing the substance** | The bar height and radii get reproduced exactly; the body gets filled with invented density. But the design *is* the row, the card, the empty state, the space between groups. |
| **F3** | **Encoding meaning in hue** | Rainbow category chips, five-step severity ramps, hash-a-string-to-a-colour. See above. |
| **F4** | **Decoration surviving by inertia** | A gradient, a resting glow, a dot next to a word that already says the status. Each added for a reason that expired; each preserved because removing feels like losing work. |
| **F5** | **Shipping the shape of a feature** | A button that renders and does nothing. An inert control is *worse* than a missing one — one dead button costs the credibility of the whole toolbar. |

## What's in the skill

| Section | |
|:--|:--|
| **Failure modes** | The five above, with fixes phrased as preconditions rather than advice |
| **Order of operations** | job → inventory → hierarchy → build → verify → **subtract one thing** |
| **The encoding hierarchy** | Including when hue genuinely *is* right, and why a data-viz ramp and a severity scale must never share tokens |
| **Patterns that hold up** | Chrome, rows, surfaces, badges — structural, with real numbers |
| **Colour** | A calibration list of the looks that appear regardless of subject, plus contrast and dark-mode rules |
| **Type, layout, motion, words** | One title size. Tabular numerals. Copy as design material. |
| **Completeness** | Every control wired; loading, empty, error, one, many, long-text all built |
| **Verification** | Break the guard on purpose. Check the computed value, not the declaration. |
| **Codebase binding** | Lift exact tokens from the repo rather than inventing a palette |
| **Checklist** | Ten-ish items, each of which can return "no" |

## Install

**Claude Code — every project:**

```bash
git clone https://github.com/deanayoung3-droid/interface-craft.git ~/.claude/skills/interface-craft
```

**Claude Code — one project:**

```bash
git clone https://github.com/deanayoung3-droid/interface-craft.git .claude/skills/interface-craft
```

**Claude.ai or Claude Desktop:** upload `SKILL.md` as a custom skill.

Restart Claude Code afterwards. Invoke it with `/interface-craft`, or just ask
for UI work — the description is written to trigger on its own.

## Using it

It's most useful *before* code exists. Good openers:

```
/interface-craft redesign the settings page
/interface-craft this list looks cluttered, fix the hierarchy
/interface-craft build the empty and error states for the inbox
```

It will push back in ways that are the point, not friction: asking what the
screen's job is before drawing it, cutting elements that support no decision,
refusing to build a control it can't wire, and removing one thing before
handing over.

## Project overrides

The skill defers to the repo. If a project has a `DESIGN.md`, a
`.claude/DESIGN.md`, or a design section in `CLAUDE.md`, **that outranks the
skill wherever they disagree** — project rules are decisions someone already
made and defended.

This is where your tokens, your banned colours, and the things you've already
said three times belong:

```markdown
# Design rules

## Standing bans
- No status dots. A dot beside a word that already says the status is
  the same value twice, in a form you have to learn.
- No orange anywhere. It's a lifted brand colour and it reads as generic.

## Tokens — resolved values, never invent a hex
--ink #1a1a1c   --graphite #5c5c66   --muted #8a8a94
--action #4285f4   (actions and links only)
```

Keeping them in the repo means they survive a new session, a new machine, and
whoever picks up the work next.

## Why this exists

It was written after four redesigns of the same app were rejected for the same
reasons, none of which anyone could name at the time. Each pass restyled instead
of rebuilding, reached for colour instead of hierarchy, and shipped controls that
didn't do anything.

Writing the rules down was the fix. Nothing durable held them, so every session
re-derived them from scratch and drifted back to the same defaults.

## Licence

MIT — see [LICENSE](LICENSE). Use it, fork it, change it.
