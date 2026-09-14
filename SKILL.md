---
name: interface-craft
description: Design and build product UI that looks like a real designer made it — app screens, dashboards, flows, redesigns, components. Use before writing any JSX/CSS for a user-facing screen, and before producing mockups or design directions. Encodes the discipline behind Linear, Shopify, Flighty, and Apple: workflow before layout, meaning encoded by rank and type before colour, and every control actually wired.
---

# Interface craft

Most AI-generated UI fails the same way, and it is not a matter of taste. It is
five specific, diagnosable mistakes. This skill names them, gives you an order
of operations that makes them hard to commit, and gives you checks that can
actually return "no."

If you read only one section, read **Failure modes** and **The encoding
hierarchy**. Those two carry most of the value.

---

## 1. Failure modes

Before designing, and again before handing over, check yourself against these.
Name which ones you were at risk of and what you did instead.

### F1 — Designing a screen instead of a workflow

The pass starts at "what does this page look like" and never asks "what is this
person doing, and what do they do next." When the job is undefined you show
everything you have, which is exactly why the result feels cluttered and
over-informative.

Flighty's main screen is essentially one number: when does the plane land. It is
not minimal because minimal is fashionable — it is minimal because it knows its
job. Every other fact on that screen is subordinate to the number, visibly.

**Fix:** you may not open an editor until you can complete this sentence:
*"On this screen, a person is ______, and the next thing they do is ______."*

### F2 — Copying the chrome, inventing the substance

Given a reference, the instinct is to reproduce the frame — the top bar height,
the sidebar width, the radii — and then fill the body with invented density. The
copying budget goes to the wrapper, which is the easy part and the part nobody
looks at.

The design *is* the row, the card, the empty state, the space between groups,
the way a number sits next to its label. Copy those.

**Fix:** when a reference is supplied, write down its row anatomy before you
build — height, what's at each end, what appears on hover, what's omitted. If
you cannot describe the row, you have not looked at the reference.

### F3 — Encoding meaning in hue

The reflex: something means more/worse/different, so reach for colour. This is
where rainbow category chips, orange→red severity ramps, and six-hue string
hashes come from. It reads as decoration because it *is* decoration — the
information was already available in a channel you skipped.

See **The encoding hierarchy** below. This is the highest-leverage rule here.

### F4 — Decoration that survives by inertia

A gradient, a resting glow, a coloured icon chip beside a page title, a status
dot next to a word that already says the status. Each was added for a reason
that has since expired, and each pass preserves it because removing things feels
like losing work.

**Fix:** every pass removes at least one element. Name it in the handover.

### F5 — Shipping the shape of a feature

A button that renders and does nothing. A tab strip over a single view. A `+`
pinned at `opacity-0` with nothing to reveal it. A filter that doesn't filter.

An inert control is **worse than a missing one** — it teaches people the product
is broken, and they stop trusting the controls that do work.

**Fix:** if it can't do the thing, it doesn't go in. See **Completeness**.

---

## 2. Order of operations

The ordering is the point. Skipping to step 4 is how F1 happens.

**1. State the job.** One sentence, both blanks filled (F1). Write it in the
handover so it can be argued with.

**2. Inventory and cut.** List every element you intend to show. For each, name
the decision it supports. Anything supporting no decision comes out.

A screen shows **one primary thing, up to three supporting facts, and one
action.** Exceeding that needs a reason you can say out loud. "The user might
want it" is not a reason — everything might be wanted; that's why it's a design
problem.

**3. Assign hierarchy.** Decide what is loudest. Exactly one element per screen
gets to be loud. Then decide what each remaining element is encoded by, working
down the hierarchy in §3 — not by reaching for a colour.

**4. Build, completely.** §7.

**5. Verify by breaking it.** §8.

**6. Subtract one thing.** Take out one element. If the screen isn't worse,
it stays out. (Coco Chanel's mirror rule, and it works on interfaces.)

---

## 3. The encoding hierarchy

When something needs to read as *more*, *worse*, *newer*, or *different*, use
the highest channel on this list that can carry it. Do not skip down.

| # | Channel | Example |
|---|---------|---------|
| 1 | **Order** | The worst item is at the top. Costs nothing, always legible. |
| 2 | **Grouping / whitespace** | Sections with space between them; a count in the group header. |
| 3 | **Type weight & size** | The number that matters is 32px/600; everything else is 13px/400. |
| 4 | **Glyph or shape** | Linear's four-bar priority mark. Achromatic, learnable, tiny. |
| 5 | **Achromatic value** | muted grey → graphite → ink. Four legible steps before any hue. |
| 6 | **Hue** | Last. Smallest scale. One or two values, never a ramp of five. |

Most bad interfaces start at 6. Most good ones never get past 3.

**Concretely:** a severity scale should be *rank* (worst first) + *weight* (the
top item's number is heavier) + at most **one** red on the genuinely urgent
bucket. Not five oranges.

**The corollary that matters:** if you find yourself needing five colours for
five levels, you are encoding in the wrong channel. Go back to order.

### When hue IS the right answer

- **Continuous data at large scale** — a heatmap, a chart series, a field
  visualisation. Here hue *is* the data, it occupies real area, and there's no
  text fighting it. Use a perceptually ordered, monochromatic-to-light ramp.
- **A single semantic state at small scale** — one red for destructive, one
  green for success. Two hues. Not a palette.
- **Brand identity in one place** — the logo, the primary action. Not the tenth
  place.

Critically: **a data-visualisation ramp and a severity scale are different jobs
and must never share tokens.** Using one ramp for both is a common and
expensive bug — it forces the viz ramp's mid-tones to serve as *text colours*,
which they are never legible as.

---

## 4. Reference anatomy

"Make it look like X" is not satisfied by adopting X's colours. Here is what
these products actually do, structurally. When asked to copy one, copy this —
and go look at real screenshots for the specific screen, because this is a
summary, not a substitute.

### Linear — density without noise
- Top bar ~40px: a **breadcrumb** (`workspace / section`) at the left, two quiet
  icon buttons at the right. **No centred search field** — that is Notion's and
  GitHub's idiom, and adding one makes a product read as not-Linear before any
  content renders. Search is a magnifier in the sidebar header.
- Rows ~32–36px, full-bleed, separated by nothing or a hairline. Hover reveals
  controls; nothing reserves space for them.
- Status = a 12px ring glyph. Priority = a four-bar glyph. Both achromatic or
  near it. Labels are neutral chips, not hashed hues.
- Group headers: name, count, a hover-revealed `…` and `+`. No coloured band.
- Palette: achromatic + exactly one accent. Title size does **not** change
  between a list page and a detail page.
- No coloured icon badge beside a page title. Anywhere. Not one.

### Shopify Polaris — numbers and cards
- Dark top bar (~56px) spanning full width, with search in the middle of it.
- **One grey ground** (`#f1f1f1`) shared by rail and canvas; white cards *float
  on* it. (Linear instead puts white content *inside* a bordered panel. This is
  the single biggest structural difference between the two languages.)
- Cards are the unit of layout: ~12px radius, soft shadow, real internal padding.
- Status = a **filled pill**: pale ground, very dark ink of the same hue
  (`#cdfee1` on `#0c5132`). The contrast lives in the **ink**, which is why
  these stay legible where a mid-tone fill would not.
- Index tables with a filter bar, column headers, and per-row actions.
- **Cost of this language:** pills bucket a continuous value into 3–4 states.
  If precision matters, you lose it.

### Flighty — one number, earned
- The single most important value dominates the screen at display size.
- Everything else is typographically subordinate and visibly so.
- Colour appears for exactly one thing (delay state), at small scale.
- Motion is used to explain change, not to announce arrival.

### Apple HIG — restraint as structure
- A defined type ramp used consistently; hierarchy from weight and size first.
- Semantic colour, sparingly; colour never the sole carrier of meaning
  (accessibility, and it also just reads better).
- Generous hit targets (44pt), generous margins, content-first.
- Depth comes from layering and material, not from borders on everything.

---

## 5. Colour

### Calibration — the AI-default looks

These three appear regardless of subject, which is what makes them defaults
rather than choices. If the brief doesn't explicitly ask for one, don't produce
one:

1. Warm cream (`#F4F1EA`) + high-contrast serif display + terracotta accent.
2. Near-black + a single acid-green or vermilion accent.
3. Broadsheet: hairline rules, zero radius, dense newspaper columns.

Also on this list, specifically for product UI:
- **Orange→red severity ramps on a white dashboard.** The most templated choice
  in the entire analytics category.
- **Gradients on surfaces** — cards, headers, page backgrounds, section bands.
- **Purple→blue "AI" gradients.** Instantly dates the product to its cohort.
- **Glassmorphism** applied to everything rather than to one layer.

### Rules

- **Two hues maximum on a screen at once**, not counting greys. One is usually
  better: an action colour, and a single semantic red when something is wrong.
- **Grounds are achromatic** (neutral or warm-neutral). If the grounds are tinted
  and the data is tinted, the data stops reading as data.
- **Never derive colour from a string hash.** That is the rainbow-chip generator.
- **Contrast lives in the ink**, not the fill. A pale ground with dark ink of
  the same hue stays legible; a mid-tone fill with white text rarely does.
- **Check text contrast as text**, not as decoration. A `#f8ae55` on white is
  about 2:1 and unreadable as a numeral — a real and frequent token bug.
- **No resting glows.** A permanent `box-shadow` halo on a button is
  marketing-CTA anatomy. Rings appear on `:focus-visible`, doing keyboard work.
- **Dark mode is not an inversion.** Redefine tokens only; preserve the
  *relationships* (if the rail is a step darker than the canvas in light, keep
  that relationship, which may mean surfaces get *lighter* than the ground).
  Define the full palette on bare `:root`; never give a colour its only
  definition inside a media query.

---

## 6. Type, layout, motion, words

### Type
- **One family** unless there's a stated reason for two. A second family is a
  design decision, not a default.
- **One title size for the whole product.** Products commonly drift to three;
  Linear does not change its title scale between a list and an entity. Pick one
  and enforce it.
- A tight scale: display / title / body / secondary / label. Five steps, used
  consistently, beats twelve used loosely.
- Tracking tightens as size grows (`-0.02em` on a 20px+ title; `0` on body).
  Tracking opens up in at most one place (an eyebrow), if at all.
- **Tabular numerals on anything that changes.** Values must not jitter between
  renders. This is a one-line fix people forget and it reads as amateurish.

### Layout
- **Space carries more meaning than rules do.** Reach for whitespace before a
  border; most dividers in a first draft can be deleted.
- Radii: consistent and few. Controls one value, cards another. Not five.
- Align to a real grid. Don't round token values to the 4/8px grid *after* lifting
  them from a design system — lift the exact value.
- Responsive is not optional: verify at 375px. Wide content (tables, charts,
  code) scrolls inside its own container; the page body never scrolls sideways.

### Motion
- Motion explains change: where something came from, what just happened.
- One orchestrated moment beats scattered effects. Scattered micro-animations
  are a strong AI-generated tell.
- 150–260ms for UI transitions, with an ease-out curve. Longer feels sluggish.
- Respect `prefers-reduced-motion`.
- **Careful with fill modes:** `animation-fill-mode: both` holding
  `transform: none` still computes to `matrix(1,0,0,1,0,0)`, which creates a
  containing block and silently breaks any `position: fixed` descendant. Use
  `backwards` for enter animations. (This costs a day every time.)

### Words
Copy is design material, not decoration.
- Name things by what a person controls, never by how the system is built.
- Active voice, sentence case: **"Save changes,"** not "Submit."
- An action keeps its name through the whole flow: the button that says
  "Publish" produces a toast that says "Published."
- Errors say what happened and how to fix it. They don't apologise and they are
  never vague.
- An empty state is an invitation to act, not a shrug.
- Each element does exactly one job — a label labels, an example demonstrates,
  nothing quietly does double duty.

---

## 7. Completeness

"Built" means all of this, or it isn't built:

- **Every control is wired to a real action.** No decorative buttons, no tab
  strips over one view, no filters that don't filter, no hover-reveal on an
  element with nothing to reveal.
- **Every state exists:** loading, empty, error, exactly one item, many items,
  very long text, and the overflow/truncation behaviour for each.
- **Keyboard reachable**, with a visible focus ring. Tab through it yourself.
- **The unhappy path is designed**, not just the demo path.
- If something genuinely can't be wired yet, it is **marked inert and
  `aria-hidden`**, or it is left out. Copy the shape, never the lie.

---

## 8. Verification

A green check is not verification. Three rules:

1. **Run the real path**, with real data, in a browser. Not a type-check.
2. **Break the guard on purpose.** Trigger the error, submit the empty form,
   pass the malformed input, resize to 375px, load with 200 rows. If you never
   saw it fail, you don't know the guard runs.
3. **Check the computed value, not the declaration.** What you wrote and what
   the browser resolved are different things, and the gap is where the bugs are.

Take a screenshot and look at it. A picture is worth a thousand tokens, and
you will catch things in the image that you cannot catch in the markup.

---

## 9. Binding to an existing codebase

**Default behaviour inside a repo: match the existing app exactly, without being
asked.** A user should never have to say "use our design system first."

Before drawing anything:

1. **Find the tokens** — `tokens.css`, `theme.*`, `variables.css`, a Tailwind
   theme block, `design-system/`, `ui/`, Storybook, brand fonts in `assets/`.
2. **Find the nearest existing screens** to what's being asked for.
3. **Lift exact values** from the real component source: colours, type ramp,
   weights, line-heights, spacing, radii, borders, control heights, icon sizes.
   Follow tokens to their resolved values. **Never round, never invent a hex.**
4. **Reproduce standard components' anatomy and states as they exist.** New UI
   *extends* that vocabulary — same tokens, same density, same components.
5. **Say in one line what you matched**, e.g. "matching `packages/ui` — Söhne,
   6px radii, slate/indigo tokens, 32px controls."

Only when a genuine search finds no app and no design system do you design a
palette from scratch — and say that you looked.

### Project overrides

If the repo has a `DESIGN.md`, `.claude/DESIGN.md`, or a design section in
`CLAUDE.md`, **it outranks this skill** wherever they disagree. Project rules
are decisions someone already made and defended; this file is the default.

Read it before designing. Honour standing bans (a specific colour, a specific
element) even when they contradict a general principle here — and if a project
rule looks like a mistake, say so in one sentence and follow it anyway.

---

## 10. Pre-handover checklist

Every item must be answerable. A "no" is a blocker, not a note.

**Job**
- [ ] Can I state the screen's job in one sentence, both blanks filled?
- [ ] Is exactly one element the loudest thing on screen?
- [ ] Did I cut everything that supports no decision?

**Encoding**
- [ ] Is meaning carried by order/grouping/type before hue?
- [ ] Two hues max, greys aside? No hue ramp standing in for rank?
- [ ] No string-hashed colours? No colour as the *sole* carrier of meaning?

**Craft**
- [ ] One type family, one title size, tabular numerals on changing values?
- [ ] Consistent radii, space doing the work that borders were doing?
- [ ] No surface gradients, no resting glows, no decorative icon chips, no dots
      restating a word that's already there?

**Completeness**
- [ ] Every control wired, or marked inert and hidden from assistive tech?
- [ ] Loading, empty, error, one, many, and long-text states all built?
- [ ] Keyboard reachable with a visible focus ring?

**Proof**
- [ ] Ran it, looked at it, and tried to break it?
- [ ] Verified at 375px?
- [ ] Checked computed values where behaviour depends on them?

**Restraint**
- [ ] Did I remove one thing?
- [ ] If a reference was supplied — did I copy the row and the card, or did I
      copy the frame and reinterpret the contents?
