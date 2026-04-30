# Align Design System (ADS)

A design system for **Align Technology** — the medical device company behind Invisalign clear aligners, Vivera retainers, iTero intraoral scanners, and exocad CAD/CAM software. This system mirrors the **"06. Web components [0.9.0]"** Figma library used by Align's internal product teams.

> Version 0.9.0 — design-library snapshot recreated from Figma.
> Align Technology is a medical device company listed on NASDAQ (ALGN), with ~21,000 employees and global operations across the US, Israel, Switzerland, Poland, Mexico, and beyond.

## Source

- **Figma file**: `06. Web components [0.9.0].fig` (mounted as a virtual filesystem in the source project — read-only)
- **Internal request workflow referenced in the file**: `jira.aligntech.com` → project key `ADS`
- **Internal contact referenced in the file**: `ads@aligntech.com`

## Products covered

Align's software touches several surfaces — this system is tuned for **internal clinical / admin web applications**, the type of UIs that sit alongside:

- **Doctor Site** — portals used by orthodontists to submit, review, and track patient treatment plans
- **iTero Cloud** — tooling around intraoral scanner outputs, orders, and scan reviews
- **ADS (Align Design System) console** — the system itself as used by internal teams
- **Patient-facing companion surfaces** (Invisalign My App, etc.) — partially covered by the same tokens but typically warmer/larger

The library is deliberately generic — the same tokens run across all of these — so this kit is most accurate for back-office / clinical software, not marketing sites.

---

## Index

Root files:

- **`README.md`** — this file. Brand, content, visual, iconography fundamentals.
- **`colors_and_type.css`** — the token layer. All colors, type scale, spacing, radii, shadows, motion as CSS custom properties. Import this anywhere.
- **`SKILL.md`** — packaging of this folder as a reusable Agent Skill.

Folders:

- **`assets/`** — logo SVG, avatar placeholders. Copy what you need into real projects.
- **`fonts/`** — (Roboto is loaded from Google Fonts; no local files). If you need offline use, drop the Roboto .ttfs here and swap the `@import` in `colors_and_type.css`.
- **`ui_kits/ads-web/`** — UI kit: JSX components and a live click-through `index.html` demonstrating the system in a realistic internal web app.
- **`preview/`** — small HTML cards used to populate the Design System tab (tokens, type specimens, component states). Reference these when you need a one-glance reminder of what something looks like.
- **`align-ds-react/`** — Vite + React 19 reference app showing the components in use. See [Use in another project](#use-in-another-project) below.

---

## Brand & content fundamentals

### Voice & tone

Align's product copy is **functional, clinical, and short**. It is written for a medical professional or internal operator — never "marketing-y", never whimsical. When you're writing for this system, think of an EHR, a medical dashboard, or a CAD tool — not a consumer app.

Observed patterns from the Figma library:

- **Imperative, minimal**: *"To create new request click the "Create" button"*, *"If the request is not valid or was created earlier, then it is closed."*
- **Second person ("you") when giving instructions**, third person otherwise. Example: *"If you want to change existing icons/components or add a new one, use this issue type."*
- **Sentence case everywhere.** Headings, buttons, menu items, tabs, tags — all sentence case. The only Title Case appears in proper nouns (product names, "Create", etc.). Reserve ALL CAPS for two-letter avatar monograms only.
- **No exclamation marks.** No emoji.
- **Recommendations are labelled** with "Recommendation:" and a one-paragraph explanation — never bulleted in the design guidance files.
- **Action labels** are verb-first: `Create`, `Save changes`, `Cancel`, `Delete`, `Submit request`. No "Go ahead and…", no "Let's…".
- **Empty / placeholder text** is descriptive, not clever: `Placeholder text`, `Optional helper text`, `Label`.

Examples, paraphrased from the file:

> **Introduction**
> All inquiries are accepted in Jira. This space was chosen in order to easily keep track of all requests in one place and follow their progress throughout the release cycle.

> **Feature request**
> This type of request is submitted when the library needs to be modified or extended.

> **Recommendation:**
> When creating a "Feature request" provide a clear and concise description of what the problem is trying to solve. Be sure to attach screenshots, videos or link to illustrate the problem.

Mirror this register: measured, explanatory, practical.

### Casing

- **UI labels**: sentence case (`Create new request`, `Button text`, `Optional helper text`).
- **Status / inline messages**: `Success headline:`, `Error headline:` — bold prefix + colon + neutral body copy.
- **Required markers**: a single red asterisk `*` after the label, color `var(--ads-error-500)`.

### Length

Keep page titles to a single line (~1024px wide max). Section headings 2–4 words. Body paragraphs stay narrow — 464px in the Figma, ~56ch in practice. Long prose is rare; forms, tables, toolbars, and cards dominate.

---

## Visual foundations

### Color vibe

The palette is **cool, clinical, high-contrast**. One signature blue (`rgb(0,154,206)`) does all the heavy lifting for action and emphasis. Text is black with alpha — `0.93` for primary, `0.63` for secondary, `0.445` for subtle — not tonal grays. Surfaces are near-white (`#FFF`) floating on a warm-neutral page (`#F4F4F4`).

- **Primary**: `#009ACE` (blue) — the only saturated color used for action at rest.
- **Error / required**: `#D43F58` (rose-red).
- **Danger button**: `#CF2E38` (darker red — used *only* on destructive buttons).
- **Success**: `#25764A` / `#00964E`.
- **Warning**: `#FA8E41` (used very sparingly — one toast state).
- **Info**: identical to primary blue.
- **Page bg**: `#F4F4F4`. Components sit on `#FFF`.

Tag tints are the one place the palette opens up — blue, green, red, orange, purple, magenta — all as **pale fill + matching pale border + deep-tint text**. Never use these tag colors as section fills or backgrounds for anything larger than a chip.

### Typography

**Roboto** is the only typeface, used in three weights:

- **300 (Light)** — only at display size (44/52), used on the cover frame for hero text.
- **400 (Regular)** — the workhorse. Body at 14/20, labels at 12/16, button labels at 14/18.
- **500 (Medium)** — section headings (20/28), card/accordion headlines (17/24), avatar monograms, "required" asterisks, inline-message headlines.

Dominant size is **14/20** — about 85% of text in the file is Roboto Regular 14px. Secondary size is **12/16** for helper text, labels, tags. Display sizes are rare and only appear on covers and landing pages.

> **Fallback**: If Roboto is unavailable, use the system sans (`-apple-system`, `Segoe UI`, `Helvetica Neue`). `Inter` appears once in the file (12px, one instance) — treat this as a stray, not a second brand face.

### Spacing

4px base grid. All observed spacing is a multiple of 4: `4, 8, 12, 16, 20, 24, 32, 40, 64`. Field-label-to-field gap is 8px; field-to-helper gap is 8px; section-to-section gap is 32 or 64.

### Corners & radii

- **4px** — buttons, fields, cards, modals, notifications, focus outer.
- **2px** — inner focus ring.
- **28px** — pill shapes: toggles and tags.
- **50%** — avatars, toggle handles.
- Never rounder than 4 on rectangular containers; never square (0px) except for dividers.

### Borders

- Separators: `1px solid rgba(0,0,0,0.085)` — very subtle black alpha.
- Secondary button outline: `1px solid rgb(143,143,143)`.
- Tag border: pale tint of the tag color.
- Never dashed, never doubled, never colored borders on primary containers.

### Elevation / shadows

Shadows are **restrained and directional-down only**. Two recurring tokens:

- `0 2px 12px rgba(0,0,0,0.125)` — cards, popovers, contextual menus.
- `0 4px 12px rgba(0,0,0,0.08)` — toasts.

Cards at rest have **no shadow** — only 1px dividers. Shadows appear on floating surfaces (menus, toasts, modals). Never use colored shadows.

### Backgrounds & imagery

This is **not** a system of gradients, hand-drawn illustrations, or repeating patterns. Backgrounds are flat, near-white, sometimes with a single full-bleed product photograph (e.g. patient imagery in clinical dashboards). When imagery does appear in this family of products (Invisalign marketing, scanner product pages) it is:

- **Cool-toned, high-key** — soft studio lighting, white/pale backdrops.
- **Clinical photography** — real patients, real practitioners, real scanners. No lifestyle filters, no grain, no duotones.
- **Sparing** — one hero image per surface, not image-heavy pages.

Avoid: bluish-purple gradients, radial blobs, noise, grain, hand-drawn flourishes. None of these appear in the file.

### Transparency & blur

Black alpha is used for **text and dividers only** — not backdrop-blur, not frosted panels. No translucent surfaces.

### Cards

Cards are:
- White fill (`#FFF`)
- 4px radius
- No border at rest; optional 1px subtle divider inside
- No shadow at rest; a 2-12-rgba(0,0,0,0.125) on hover or when floated as a popover

### Hover states

Hover darkens the primary color slightly (`#009ACE` → `#0277B5`) and lightens ghost/link buttons to a pale blue tint wash. Ghost hover is `rgba(0,154,206,0.08)`-ish background. No scale, no lift, no shadow change on small controls.

### Pressed states

Pressed goes **deeper** (`#015990`) on primary, and pulls the background down for ghost/link. No scale-down animation — the file shows instant state change.

### Focus states

Focus is a **doubled ring**: 1px outer blue (`#009ACE`), 2px inner gap (white), inner control. In CSS this is `outline: 1px solid var(--ads-focus-ring); outline-offset: 1px; box-shadow: inset 0 0 0 1px #fff`. Appears on every interactive control — buttons, fields, toggles, tabs.

### Disabled states

Disabled uses `#F5F5F5` fill with `#C7C7C7` label. No strikethrough. No hatch. Cursor not-allowed.

### Animation

Quick, straight transitions only. **120–180ms** on color/opacity; no bounces, no springs, no layered stagger. Easing is a standard `cubic-bezier(0.2, 0, 0, 1)`. Loading spinners are a thin indeterminate ring.

### Layout rules

- Max content width typically **1024px** for clinical admin pages; dense tables can go wider.
- Page padding: **40px** horizontal, **40px** top, **80px** bottom on landing-type screens.
- Navigation panel: fixed left rail, 80px wide collapsed / 240px expanded.
- Page header: 944px inner content max inside 1024px page frame, with title (28/36) and optional subtitle (14/20).

---

## Iconography

Align's library uses a **custom in-house icon set** (not Material, not Font Awesome, not Lucide). Icons appear as SVG components in Figma, exposed as `Size=16x16` and `Size=20x20` symbols. Observed characteristics:

- **Sizes**: 16×16 (inside tags, labels) and 20×20 (inside buttons, fields, toasts). 32×32 exists for oversized cases.
- **Style**: outline, 1.5–2px stroke, rounded line caps, clinical/neutral shapes (checkmark, close, chevron, plus, pencil, calendar, search, etc.). Filled variants only for status indicators (`checkmark-fill`, `error-fill`).
- **Color**: icons inherit their container's foreground. On buttons, icon == label color. On toast indicators, icon == status color.
- **No emoji. No unicode-as-icon. No mixed icon styles.**

### What this kit includes

- `assets/align-logo.svg` — the Align wordmark, extracted directly from the Figma file.
- Generic 20×20 icon placeholders in the UI kit for actions we don't have source SVGs for (plus, chevron, close, search, more) — drawn to match the observed stroke weight. **Flagged**: for production use, request the real ADS icon set from the Align team.

### Substitution

Because the real ADS icon set is not shipped with the Figma file, the UI kit draws a **minimal set of line icons inline** that match the observed stroke weight (~1.75px, rounded caps). These should be swapped for the production ADS icons before shipping anywhere customer-facing. **Do not** substitute Material or Heroicons — the stroke weights and corner curves don't match.

### Logos included

- `assets/align-logo.svg` — the "Align" wordmark from the Figma cover frame. Black fill, transparent background.

---

## Use in another project

Two paths depending on the stack you're dropping it into.

### Path A — Vanilla HTML / CSS (any framework)

This is the smallest possible integration: pull in the token layer and start using the CSS variables.

1. **Copy the files.** From this repo, copy `colors_and_type.css` and the `assets/` folder into your project (e.g. `src/styles/` and `src/assets/`).
2. **Import the tokens once, at the root of your app.** In a vanilla page:
   ```html
   <link rel="stylesheet" href="/styles/colors_and_type.css">
   ```
   Or in a bundler (Vite, webpack, Next, etc.):
   ```js
   import "./styles/colors_and_type.css";
   ```
3. **Use the variables.** All tokens are CSS custom properties prefixed with `--ads-`:
   ```css
   .my-button {
     background: var(--ads-blue-500);
     color: var(--ads-text-on-primary);
     border-radius: var(--ads-radius-sm);
     font: 500 14px/18px var(--ads-font-sans);
   }
   .my-button:hover  { background: var(--ads-blue-600); }
   .my-button:active { background: var(--ads-blue-700); }
   ```
4. **Optional — install as a git submodule** so you can pull design updates:
   ```bash
   git submodule add https://github.com/lior25659567/align-ds.git vendor/align-ds
   ```
   Then import from `vendor/align-ds/colors_and_type.css`.

### Path B — React (Vite / Next / CRA)

The `align-ds-react/` folder is a working Vite + React 19 reference app. To reuse its components in another project:

1. **Copy these into your project's `src/`:**
   - `align-ds-react/src/styles/tokens.css` (or this repo's root `colors_and_type.css` — same tokens)
   - `align-ds-react/src/styles/components.css`
   - `align-ds-react/src/components/` (Kit.jsx, Shell.jsx, Icon.jsx, index.js)
2. **Wire it up in `main.jsx` / `_app.tsx`:**
   ```jsx
   import "./styles/tokens.css";
   import "./styles/components.css";
   ```
3. **Use the components:**
   ```jsx
   import { Button, Card, TextField, Tag } from "./components";

   export default function Page() {
     return (
       <Card>
         <TextField label="Patient ID" placeholder="e.g. 1024-AB" />
         <Button variant="primary">Save changes</Button>
       </Card>
     );
   }
   ```
4. **Roboto font.** `tokens.css` `@import`s Roboto from Google Fonts. If you serve fonts locally, drop the `.ttf`s in your project's `public/fonts/` and replace the `@import` with a local `@font-face` block.

### Path C — Run the reference app locally

To poke around the live demo before integrating:

```bash
git clone https://github.com/lior25659567/align-ds.git
cd align-ds/align-ds-react
npm install
npm run dev
```

Open the printed `http://localhost:5173`. The static `index.html` at the repo root works without any build step — just open it in a browser.

### What to copy vs. what to leave behind

| You probably want | You can skip |
| --- | --- |
| `colors_and_type.css` (tokens) | `preview/` (specimen cards, dev-only) |
| `assets/align-logo.svg` | `align-ds-react/index.html` (the demo shell) |
| `align-ds-react/src/components/` | `align-ds-react/src/screens/` (the demo screens) |
| `align-ds-react/src/styles/` | `ui_kits/ads-web/Screens.jsx` (demo only) |

### Versioning & updates

Pin to a tag/commit, don't track `main`. When you want updates:

```bash
# submodule path
git -C vendor/align-ds fetch && git -C vendor/align-ds checkout <new-tag>

# copy path
# diff your local copies against the new commit and merge by hand
```

The token names (`--ads-blue-500`, `--ads-radius-sm`, `--ads-text-primary`, `--ads-font-sans`, etc.) are the public API — those are the names you should depend on. Internal class names inside `components.css` may change.

---

## Flags & caveats

1. **Icon set**: real Align icons are not shipped with the Figma file. The UI kit uses hand-drawn matching placeholders. Swap before production use.
2. **Fonts**: Roboto is loaded from Google Fonts CDN. For offline/air-gapped use, drop the files in `fonts/` and change the `@import` in `colors_and_type.css`.
3. **Scope**: this library is Web only. Mobile (Invisalign My App) and the iTero touch-scanner UI use different rules and are out of scope.
4. **Version 0.9.0**: the file is explicitly pre-1.0. Expect gaps (e.g. no full dark-mode palette beyond Tab, limited form-error states).
5. **Copy and motion specifics** are inferred from the static file — confirm with the Align ADS core team (`ads@aligntech.com`) for anything shipping publicly.
