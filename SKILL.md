---
name: interface-craft
description: Design and build product UI that looks like a real designer made it — app screens, dashboards, flows, redesigns, components. Use before writing any JSX/CSS for a user-facing screen, and before producing mockups or design directions. Encodes workflow before layout, meaning encoded by rank and type before colour, patterns that hold up at scale, and a completeness contract where every control is actually wired.
---

# Interface craft

Most generated UI fails the same way, and it is not a matter of taste. It is
five specific, diagnosable mistakes. This skill names them, imposes an order of
operations that makes them hard to commit, and ends in a checklist that can
actually return "no."

If you read only two sections, read **Failure modes** and **The encoding
hierarchy**. Those carry most of the value.

---

## 1. Failure modes

Check yourself against these before designing, and again before handing over.
Name which ones you were at risk of and what you did instead.

### F1 — Designing a screen instead of a workflow

The pass starts at "what does this page look like" and never asks "what is this
person doing, and what do they do next." When the job is undefined you show
everything you have. That is the actual source of clutter — not too many
elements, but no principle for excluding any.

The strongest screens in any category are built around a single question the
person came to answer. Everything else on the screen is visibly subordinate to
it. That subordination is the design.

**Fix:** you may not open an editor until you can complete this sentence:
*"On this screen, a person is ______, and the next thing they do is ______."*

Both blanks. If the second one is empty, you are building a report, not a
screen, and it will read as one.

### F2 — Copying the chrome, inventing the substance

Given a reference, the instinct is to reproduce the frame — bar height, sidebar
width, radii, shadows — and then fill the body with invented density. The
copying budget goes to the wrapper, which is the easy part and the part nobody
actually looks at.

The design *is* the row, the card, the empty state, the space between groups,
the way a number sits next to its label, what appears on hover. Those carry the
feel. The frame is a rectangle.

**Fix:** when a reference is supplied, write down its **row anatomy** before
building — height, what sits at each end, what appears on hover, what is
deliberately absent. If you cannot describe the row, you have not looked.

### F3 — Encoding meaning in hue

The reflex: something means more, worse, or different, so reach for colour.
This is where rainbow category chips, five-step severity ramps, and
hash-a-string-to-a-hue come from.

It reads as decoration because it *is* decoration. The information was already
available in a channel that was skipped. See §3 — this is the highest-leverage
rule in this document.

### F4 — Decoration that survives by inertia

A gradient, a resting glow, a coloured icon chip beside a page title, a status
dot next to a word that already states the status. Each was added for a reason
that has since expired, and each pass preserves it, because removing things
feels like losing work rather than doing work.

**Fix:** every pass removes at least one element. Name it in the handover.

### F5 — Shipping the shape of a feature

A button that renders and does nothing. A tab strip over a single view. A `+`
pinned at `opacity-0` with nothing to reveal it. A filter that doesn't filter.
A sort header that doesn't sort.

An inert control is **worse than a missing one.** It teaches people the product
is broken, and then they stop trusting the controls that do work. One dead
button costs you the credibility of the whole toolbar.

**Fix:** if it can't do the thing, it doesn't go in. See §7.

---

## 2. Order of operations

The ordering is the point. Skipping to step 4 is exactly how F1 happens.

**1. State the job.** One sentence, both blanks filled. Put it in the handover
so it can be argued with.

**2. Inventory and cut.** List every element you intend to show. For each, name
the decision it supports. Anything supporting no decision comes out.

Budget: **one primary thing, up to three supporting facts, one action.**
Exceeding it needs a reason you can say out loud. "Someone might want it" is
not a reason — everything might be wanted, which is precisely why this is a
design problem and not an inventory problem.

**3. Assign hierarchy.** Decide what is loudest. Exactly one element per screen
gets to be loud. Then, for everything else, work *down* the hierarchy in §3
rather than reaching for a colour.

**4. Build it completely.** §7.

**5. Verify by breaking it.** §8.

**6. Subtract one thing.** Remove one element. If the screen is not worse, it
stays out. This is the single cheapest quality step available and it is almost
always skipped.

---

## 3. The encoding hierarchy

When something must read as *more*, *worse*, *newer*, or *different*, use the
highest channel on this list that can carry it. Do not skip down.

| # | Channel | What it looks like |
|---|---------|--------------------|
| 1 | **Order** | The worst item is first. Costs nothing, never ambiguous, works for everyone. |
| 2 | **Grouping / whitespace** | Sections with real space between them; a count in the group header. |
| 3 | **Type weight & size** | The number that matters is 32px/600. Everything else is 13px/400. |
| 4 | **Glyph or shape** | A small four-bar mark for priority. Achromatic, tiny, learned once. |
| 5 | **Achromatic value** | muted → graphite → ink. Four legible steps before any hue at all. |
| 6 | **Hue** | Last. Smallest scale. One or two values — never a ramp of five. |

**Most bad interfaces start at 6. Most good ones never get past 3.**

Concretely: a severity list should be *rank* (worst first) plus *weight* (the
top item's figure is heavier) plus at most **one** red on the genuinely urgent
bucket. Not five oranges. The five-orange version is strictly less readable —
it asks the viewer to learn a legend to recover information that sorting
already gave them for free.

**The corollary that matters:** if you need five colours for five levels, you
are encoding in the wrong channel. Go back to order.

### When hue IS the right answer

- **Continuous data at large scale** — a heatmap, a chart series, a field
  visualisation. Here hue *is* the data, it occupies real area, and no text is
  fighting it. Use a perceptually ordered ramp, ideally monochromatic running
  into near-white.
- **One semantic state at small scale** — a single red for destructive, a
  single green for success. Two hues. Not a palette.
- **Brand, in one place** — the mark and the primary action. Not the tenth
  place.

**A data-visualisation ramp and a severity scale are different jobs and must
never share tokens.** This collapse is a common and expensive bug: it forces
the viz ramp's mid-tones to serve as *text colours*, and mid-tones are never
legible as text. A pale amber that reads beautifully as a 200px heatmap cell is
about 2:1 on white and unreadable as a numeral.

---

## 4. Patterns that hold up

These recur across interfaces that stay usable at scale. They are structural,
not stylistic — adopting a palette does not get you any of them.

### Chrome

- **The top bar says where you are.** A breadcrumb — `workspace / section` —
  at the left, one or two quiet icon buttons at the right. Keep it short:
  40px is plenty; 56px is already spending real estate on navigation.
- **Don't run two navigation systems.** A large centred search field in the top
  bar is a widely borrowed idiom that competes with the sidebar and pushes
  content down. Search works better as a small affordance near the nav it
  searches, opening a palette over the page.
- **One accent colour** across the whole product, reserved for actions and
  links. The moment a second hue is also clickable, nothing is clickable.

### Rows and lists

- **Rows are tight and full-bleed** — 32–36px, separated by a hairline or by
  nothing at all. Dense lists are easier to scan than airy ones, provided the
  type hierarchy inside the row is doing its job.
- **Controls appear on hover and reserve no space.** Reserved space for an
  invisible control reads as padding and makes every list look bloated. (And an
  `opacity: 0` control with nothing to lift it is invisible dead space forever
  — F5.)
- **State is a small achromatic glyph**, learned once and reused everywhere. A
  12px ring for status, a four-bar mark for priority. Not a coloured word, and
  not a coloured word *and* a dot.
- **Group headers carry a name and a count.** No coloured band. The count is
  the useful part.

### Surfaces

There are two coherent ways to build a page surface, and they do not mix:

1. **Content inside a bordered panel**, sitting on a ground a step darker. The
   panel is the window; cards inside it are delineated by rules and space.
2. **Cards floating on a distinctly darker ground.** Each card is white with a
   real radius, a soft shadow, and generous internal padding. No outer panel.

Pick one and hold it. Mixing them is a large part of why a layout reads as
assembled out of parts from different kits.

### State badges

When a status genuinely needs a filled badge: **pale ground, very dark ink of
the same hue.** The contrast lives in the ink. A mid-tone fill with white text
is the version that fails at small sizes and in bright rooms.

Know the tradeoff before reaching for one: a badge buckets a continuous value
into three or four states. If the precision matters — if 63 and 44 need to read
differently — a badge is the wrong instrument and a well-set numeral is right.

### Restraint

- A defined type ramp, used consistently. Hierarchy comes from weight and size
  before it comes from anything else.
- Colour is never the *sole* carrier of meaning. This is an accessibility
  requirement and it also just reads better.
- Generous hit targets (44px), generous margins, content first.
- Depth from layering and material, not from putting a border on everything.

---

## 5. Colour

### Calibration — the defaults to avoid

These appear regardless of subject, which is what makes them defaults rather
than choices. Unless a brief explicitly asks for one, don't produce one:

1. Warm cream (`#F4F1EA`) + high-contrast serif display + terracotta accent.
2. Near-black + a single acid-green or vermilion accent.
3. Broadsheet: hairline rules, zero radius, dense newspaper columns.

And specifically in product UI:

- **Orange→red severity ramps on a white dashboard.** The most templated choice
  in the entire analytics category.
- **Gradients on surfaces** — cards, headers, page backgrounds, section bands.
- **Purple→blue "AI" gradients.** Instantly dates a product to its cohort.
- **Glassmorphism on everything** rather than on one deliberate layer.

### Rules

- **Two hues maximum on screen at once**, greys aside. One is usually better:
  an action colour, plus a single semantic red for when something is wrong.
- **Grounds are achromatic.** If the grounds are tinted and the data is tinted,
  the data stops reading as data.
- **Never derive colour from a string hash.** That is the rainbow-chip machine.
- **Contrast lives in the ink**, not the fill.
- **Check text contrast as text.** Decorative-fill values are routinely 2:1 and
  unreadable the moment someone reuses them for a numeral.
- **No resting glows.** A permanent `box-shadow` halo on a button is
  marketing-CTA anatomy. Rings appear on `:focus-visible`, doing keyboard work.
- **Dark mode is not an inversion.** Redefine tokens only, and preserve the
  *relationships*: if the rail sits a step darker than the canvas in light mode,
  keep that, which may mean surfaces get *lighter* than the ground in dark.
  Define the full palette on bare `:root`; never give a colour its only
  definition inside a media query.

---

## 6. Type, layout, motion, words

### Type

- **One family** unless there is a stated reason for two. A second family is a
  decision, not a default.
- **One title size for the whole product.** Products drift to three or four
  without anyone deciding to. Pick one and enforce it — a list page and a detail
  page do not need different title scales, and having them makes the product
  feel like two products.
- A tight scale: display / title / body / secondary / label. Five steps used
  consistently beats twelve used loosely.
- Tracking tightens as size grows (`-0.02em` at 20px+, `0` at body). It opens up
  in at most one place, if any.
- **Tabular numerals on anything that changes.** Values must not jitter between
  renders. One line of CSS, routinely forgotten, and it reads as amateurish.

### Layout

- **Space carries more meaning than rules do.** Reach for whitespace before a
  border; most dividers in a first draft can simply be deleted.
- Few radii, used consistently. One value for controls, one for cards.
- Lift exact values from the design system. Do **not** round them to a 4/8px
  grid afterwards — that silently desyncs you from every existing component.
- Responsive is not optional: verify at 375px. Wide content — tables, charts,
  code — scrolls inside its own container. The page body never scrolls sideways.

### Motion

- Motion explains change: where something came from, what just happened.
- One orchestrated moment beats scattered effects. Scattered micro-animations
  are a strong generated-UI tell.
- 150–260ms with an ease-out curve. Longer feels sluggish, shorter feels broken.
- Respect `prefers-reduced-motion`.
- **Watch fill modes.** `animation-fill-mode: both` holding `transform: none`
  still computes to `matrix(1,0,0,1,0,0)` — which creates a containing block and
  silently breaks every `position: fixed` descendant. Use `backwards` for enter
  animations. This costs a day every time it happens.

### Words

Copy is design material, not decoration.

- Name things by what a person controls, never by how the system is built.
  Someone manages notifications; they do not configure a webhook.
- Active voice, sentence case: **"Save changes,"** not "Submit."
- An action keeps its name through the whole flow. The button that says
  "Publish" produces a toast that says "Published."
- Errors state what happened and how to fix it. They do not apologise and they
  are never vague about what failed.
- An empty state is an invitation to act, not a shrug.
- Every element does exactly one job — a label labels, an example demonstrates,
  nothing quietly does double duty.

---

## 7. Completeness

"Built" means all of the following, or it isn't built:

- **Every control wired to a real action.** No decorative buttons, no tab strips
  over one view, no filters that don't filter, no hover-reveal on an element
  with nothing to reveal.
- **Every state exists:** loading, empty, error, exactly one item, many items,
  very long text — and the truncation or overflow behaviour for each.
- **Keyboard reachable**, with a visible focus ring. Tab through it yourself.
- **The unhappy path is designed**, not just the demo path.
- If something genuinely cannot be wired yet, it is **marked inert and
  `aria-hidden`**, or left out entirely. Copy the shape, never the lie.

---

## 8. Verification

A green check is not verification. Three rules:

1. **Run the real path**, with real data, in a browser. Not a type-check.
2. **Break the guard on purpose.** Trigger the error. Submit the empty form.
   Pass the malformed input. Resize to 375px. Load it with 200 rows. If you
   never saw it fail, you do not know the guard runs.
3. **Check the computed value, not the declaration.** What you wrote and what
   the browser resolved are different things, and the gap between them is where
   the bugs live.

Then take a screenshot and actually look at it. You will catch things in the
image that you cannot catch in the markup.

---

## 9. Binding to an existing codebase

**Default behaviour inside a repo: match the existing app exactly, unasked.** A
user should never have to say "use our design system first."

Before drawing anything:

1. **Find the tokens** — `tokens.css`, `theme.*`, `variables.css`, a Tailwind
   theme block, `design-system/`, `ui/`, Storybook, brand fonts in `assets/`.
2. **Find the nearest existing screens** to what is being asked for.
3. **Lift exact values** from real component source: colours, type ramp,
   weights, line-heights, spacing, radii, borders, control heights, icon sizes.
   Follow tokens to their resolved values. **Never round. Never invent a hex.**
4. **Reproduce existing components' anatomy and states as they are.** New UI
   *extends* that vocabulary — same tokens, same density, same components.
5. **Say in one line what you matched**, e.g. "matching `packages/ui` — Söhne,
   6px radii, slate/indigo tokens, 32px controls."

Only when a genuine search finds no app and no design system do you design a
palette from scratch — and then say that you looked.

### Project overrides

If the repo has a `DESIGN.md`, a `.claude/DESIGN.md`, or a design section in
`CLAUDE.md`, **it outranks this skill** wherever they disagree. Project rules
are decisions someone already made and defended; this file is only the default.

Read it before designing. Honour standing bans — a specific colour, a specific
element — even where they contradict a general principle here. If a project rule
looks like a mistake, say so in one sentence and then follow it anyway.

---

## 10. Pre-handover checklist

Every item must be answerable. A "no" is a blocker, not a note.

**Job**
- [ ] Can I state the screen's job in one sentence, both blanks filled?
- [ ] Is exactly one element the loudest thing on screen?
- [ ] Did I cut everything that supports no decision?

**Encoding**
- [ ] Is meaning carried by order, grouping, and type before hue?
- [ ] Two hues maximum, greys aside? No hue ramp standing in for rank?
- [ ] No string-hashed colours? Is colour never the sole carrier of meaning?

**Craft**
- [ ] One type family, one title size, tabular numerals on changing values?
- [ ] Consistent radii? Is space doing the work borders were doing?
- [ ] No surface gradients, no resting glows, no decorative icon chips, no dots
      restating a word that is already there?

**Completeness**
- [ ] Every control wired — or marked inert and hidden from assistive tech?
- [ ] Loading, empty, error, one, many, and long-text states all built?
- [ ] Keyboard reachable with a visible focus ring?

**Proof**
- [ ] Did I run it, look at it, and try to break it?
- [ ] Verified at 375px?
- [ ] Checked computed values where behaviour depends on them?

**Restraint**
- [ ] Did I remove one thing?
- [ ] If a reference was supplied — did I copy the row and the card, or did I
      copy the frame and reinterpret the contents?
