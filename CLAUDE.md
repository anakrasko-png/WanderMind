# WanderMind

A web app that generates personalized travel itineraries from a Traveler Profile. The Profile is the heart of the product — designed first, with onboarding and itinerary generation built around it.

The user driving this is a visual designer (UI / visual storytelling / strategy) who is vibe-coding. Lead with visual quality, restraint, and editorial sensibility. Simple is elegant. Avoid product-y patterns when an editorial gesture works better.

## Current state

HTML mockups in this folder, vibe-coded to establish the visual language and styled on the BYCo (blacheyong & co) brand foundation. They are NOT production code — they are north-star artifacts that the real React/Next.js build should reverse-engineer from.

- `index.html` — landing page (entry point at root URL). Hero with the editorial headline "Travel that feels like *you*," a how-it-works section in three numbered steps, a three-tile showcase grid (Slow Wanderer / Wild Voyager / Night Owl), a placeholder "Recently from travelers" rail (community future-state), and a closing CTA. Top nav has an "Explore by archetype" link (currently labeled "soon," not active) and a "Begin →" button. Top nav and closing CTA both point to `onboarding-welcome.html`.
- `profile-result.html` — the finished Traveler Profile, designed first as the destination.
- `onboarding-welcome.html` — step 1 of 6, type-driven welcome screen with staggered fade-up animation. Single Begin button.
- `onboarding-rhythm.html` — step 2 of 6, paired sliders for Pace and Budget. Sliders show a live word ("Unhurried," "Considered," etc.) above the track and a Super Blue fill bar to the left of the thumb. JS updates word and fill on input.
- `onboarding-loves.html` — step 3 of 6, "What makes you say yes?" image-card screen. Template for the other onboarding screens.
- `onboarding-skips.html` — step 4 of 6, "What do you skip?" chip cloud (optional, faster pace).
- `onboarding-practical.html` — step 5 of 6, "A few practical things" combined screen with chip groups for dietary, accessibility, languages, and travel companions.
- `onboarding-bucket-list.html` — step 6 of 6, "Where do you dream of?" free input + suggestion chips, with a live-updating wandering line preview as destinations are added.
- `onboarding-reveal.html` — the celebration screen with choreographed staggered fade-up animations (eyebrow → name → spirit animal → palette → tagline → CTA), linking forward into `profile-result.html`.

The full flow chains forward via `<a>` Continue links: landing → welcome → rhythm → loves → skips → practical → bucket list → reveal → profile. Back links chain backward in parallel.

The brand integration is **done** at the token level — colors, type weights, radii, and the italic-→-color-shift signature gesture have all been applied. The next phase is the real React/Next.js app and additional archetypes.

## Voice & register

Quietly elegant, editorial, magazine-feeling. Taglines speak in the first person *as* the traveler, not *about* them. Restraint earns the reveal moments. Use evocative phrasing over category nouns ("Slow mornings" not "Cafés," "Old streets" not "Architecture"). Frame minimums as encouragement, not rules ("Pick four or more. Skip anything that doesn't move you.").

## Type system

- **Brand typeface:** SegmentAlt (BYCo brand font, licensed). Weights: Regular, Medium, SemiBold, Bold. **No italic.** Currently using Inter as a Google Fonts placeholder until the licensed file is installed — swap `font-family: 'Inter'` declarations to `'SegmentAlt'` in production.
- **Display headings:** SegmentAlt Bold (700) with negative letter-spacing per brand spec (`-0.025em` at 120px scale).
- **Body / UI:** SegmentAlt Regular (400) and Medium (500). Eyebrow caps in Inter UI sizes work the same.
- **Display sizing:** `clamp()` for fluid scale. Step questions: `clamp(40px, 6vw, 72px)`. Hero archetype name: `clamp(60px, 10vw, 120px)`.
- **Eyebrow / labels:** 11px, `letter-spacing: 0.2em`, uppercase, color `--muted`.
- **Small caps timing:** 10–12px, `letter-spacing: 0.16em`, uppercase, color `--muted`.

### Signature gesture: color shift, not italic

The original design used a single italicized word colored `--accent` as the archetype signature ("The *Slow* Wanderer"). Because SegmentAlt has no italic, the gesture now becomes a **color shift only** — the accent word stays in the same weight as the rest of the display, but its color flips to `--accent` (Super Blue). This mirrors BYCo's own wordmark, where "blacheyong" is in ink and "&co" is in Super Blue.

## Color tokens

Six CSS variables in `:root` of every file, mapped to BYCo brand. These ARE the design system's parametric foundation.

```css
:root {
  --bg: #FFFFFF;       /* White */
  --ink: #000000;      /* Black */
  --muted: #848A97;    /* Uni Grey 500 */
  --accent: #2D39F7;   /* Super Blue 500 — brand signature */
  --line: #E3E4EA;     /* Aluminium / Grey 200 — dividers, borders */
  --soft: #F0F1F4;     /* Grey 100 — card surfaces */
  /* Brand support colors — used in archetype palettes, not page chrome */
  --sun: #FFB200;      /* Sun 500 */
  --mint: #00C378;     /* Mint 500 */
}
```

The chrome of the page (background, ink, muted, line, soft, accent) is fixed by the BYCo brand. The two support colors (`--sun`, `--mint`) are reserved for **archetype palettes** — the four-swatch row in the Profile hero — so each traveler type can hold its own emotional tone within the brand's tonal range. All component logic, layout, and class structure are parametric on these variables. SVG illustrations use `currentColor` so they inherit ink color from context.

## The Archetype Model

Every traveler resolves to an archetype. Each archetype has four signature elements, designed coherently as a set:

1. **Name** — "The [Adjective] [Wanderer/Traveler/Seeker/Chaser/etc.]" with one accent word colored `--accent` (Super Blue). Example: "The Slow Wanderer" with "Slow" in Super Blue. Same display weight throughout — the gesture is a color flip, not an italic.
2. **Tagline** — first-person SegmentAlt Regular, captures the emotional core. Example: "Quiet mornings, neighborhood markets, and the long way home — you travel to slow down, not speed up."
3. **Palette** — 4 colors expressed as small swatches in the hero. Palette reinforces the archetype's *meaning* within BYCo's tonal range. Slow Wanderer = Sun 200 + Sun 500 + Uni Grey + Black (warm morning light). Sun Chaser would lean Sun 400/600 + grey deeps. Night Owl would lean deep Greys 800/900 + Super Blue. Use `--sun` and `--mint` to inject warmth or freshness when the chrome alone would feel too cool.
4. **Spirit animal** — a creature whose nature embodies the archetype. Hand-drawn line illustration, ink silhouette, viewBox `0 0 100 100`. Slow Wanderer = heron (patience, slow elegance, watching). Other archetype suggestions: Sun Chaser = swift or fox; Night Owl = owl; Culture Seeker = cat; Adventurer = wolf or hawk.

When adding a new archetype, design all four elements together so they cohere.

## Profile Result Page

`profile-result.html` — the destination view that onboarding fills in. Sections:

- **Hero:** spirit-animal avatar (top-left, ~104px), eyebrow ("You are"), archetype name (giant Fraunces with one italic accent word), tagline (italic serif), 4-swatch palette (top-right).
- **Wandering line:** full-width SVG band showing the bucket list as a curving line with destination dots. Each dot labeled with place (Fraunces italic) + season (Inter small caps). Personal to the user.
- **Attribute grid:** 2-column with `.section.full` spanning both. Fields: Pace (meter), Budget (meter), Travels with, Languages, Loves (solid ink chips), Skips (muted dashed chips with strikethrough), Dietary, Accessibility, Bucket list (two-column).
- **CTA:** single dark `--ink` block, italic Fraunces line, pill button "Generate my itinerary →".
- **Footer:** minimal, two small caps lines.

## Onboarding flow architecture

Six screens, deliberately varied input types so the flow feels like a conversation, not a form:

1. **Welcome** — minimal, sets tone, single Begin button.
2. **Your rhythm** — paired sliders for pace + budget.
3. **What you love** — 12 image cards, multi-select, minimum 4. (Built. `onboarding-loves.html` is the template.)
4. **What you skip** — chip cloud, faster pace.
5. **The practical bits** — combined screen for dietary, accessibility, languages, companions.
6. **Bucket list** — free input with smart-suggestion chips. Wandering line previews live as destinations are added.
7. **The reveal** — archetype name draws in, spirit animal materializes, palette fades in, drops user into their finished profile.

Progress shown as 6 small dashes (24px × 3px each) at top. Current step `--accent`, completed `--ink`, upcoming `--line`.

## Component patterns established

- **Hero typography hierarchy:** eyebrow (small caps, `--muted`) → display (SegmentAlt Bold, one accent-colored word in `--accent`) → tagline (SegmentAlt Regular, `--muted`).
- **Image-select cards:** soft `--soft` bg default → ink `--ink` bg when selected (full inversion). Small `--accent` circle with white check appears top-right. Selection feels like *filling in*. Card radius: `12px`.
- **Buttons:** pill-shaped (border-radius 999px). Primary action (Continue, CTA) uses `--accent` background. Secondary uses `--ink`. Disabled = opacity 0.3, no pointer events. Hover = `translateX(4px)`.
- **Dividers:** `1px solid var(--line)` (Aluminium).
- **Corner radii:** brand scale of 8 / 12 / 16 / 20 / 24 / 32 / round-full. Cards use 12. Containers use 12. Pills use 999.
- **Spirit-animal avatar:** ink fill + stroke, viewBox `0 0 100 100`, displayed at ~96–104px. Now in true black (`#000000`).
- **Wandering-line band:** single SVG path (cubic Bezier) for the line in `--accent` (Super Blue), dots in `--ink` with `--bg` halo, vertical stems in `--line`, place labels in SegmentAlt SemiBold, season labels in SegmentAlt small caps.
- **Selected-count + Continue button:** lives in step footer; button stays disabled until minimum threshold met. Continue uses `--accent`.

## Brand integration (BYCo)

The client brand (BYCo / blacheyong & co) has been integrated. What was applied:

1. **The six CSS variables** were swapped to BYCo tokens (White / Black / Uni Grey / Super Blue / Aluminium / Grey 100). Two support tokens added (`--sun`, `--mint`) for archetype palettes.
2. **Type stack** swapped from Fraunces + Inter to **SegmentAlt** (Inter is loaded as a placeholder until the licensed font is installed in production).
3. **Italic gesture became color-shift gesture** — SegmentAlt has no italic, so the accent word in display strings now flips color to `--accent` while staying the same weight as the rest. Mirrors BYCo's own wordmark.
4. **Corner radii** updated to brand scale (12 for cards/containers, 999 for pills).
5. **Component logic, layout, class names, and copy** are untouched — the design system being parametric on the six variables is what made the swap clean.
6. **Archetype palettes** re-derived within brand range. Slow Wanderer now uses Sun 200 + Sun 500 + Uni Grey + Black instead of sage/sand/terracotta/ink.

When future archetypes are added, follow this rule: chrome stays brand-fixed; the four-swatch palette can pull from `--sun`, `--mint`, the grey ramp, and Super Blue to express the archetype's emotional core within BYCo's vocabulary.

The brand foundation document lives at the Figma file *Foundations-BYCo* (file key `bFV4lUCM2DDq6Gy84cSmEw`). Reference it for spacing scale (4px-base), grid breakpoints (XL 1920 / L 1280 / M 768 / S 360), corner radius scale, color ramps, and effects (over-image radial overlay in Super Blue, drop shadows for annotations).

## Profile data model

The Traveler Profile is the canonical user object that onboarding produces and every other surface reads from. Reserved schema for the React/Next.js build:

```typescript
{
  archetype: string,           // "slow-wanderer" | "night-owl" | "wild-voyager" | ...
  pace: number,                // 0–4 (Slow days → Packed schedule)
  budget: number,              // 0–4 (Frugal → No limit)
  companions: string[],        // multi-select: Solo / +1 / Family / Friends / Mixed
  languages: string[],         // multi-select
  loves: string[],             // multi-select keys from loves screen
  skips: string[],             // multi-select keys from skips screen
  dietary: string[],
  accessibility: string[],
  bucketList: { place: string, season: string }[],
  visibility: "private" | "public",   // default "private"
  createdAt: string,
  updatedAt: string
}
```

The `visibility` field is reserved for forthcoming community features (the archetype-tagged itinerary library, profile sharing). Default `"private"` for all new profiles. When the community ships, only `"public"` profiles surface in the feed; `"private"` stays user-only. Building the field from day one avoids retrofit when the community phase begins.

For v1, persist to `localStorage` keyed by user. When auth is added (Clerk + Supabase recommended), migrate to a typed table.

## Future-state community (planned, deferred)

A community pillar is planned but **not built yet**. When it ships it will consist of, in order: an itinerary library (public itineraries tagged by archetype + destination), stories (text/photo posts from real trips, archetype-filterable), and companion matching (travelers with compatible profile + dates + destination).

The landing page already reserves spatial real estate for it — a "Recently from travelers" rail under the archetype showcase and an "Explore by archetype" link in the top nav — both labeled "soon" and not yet active. The Profile schema's `visibility` field plus a future `Itinerary` model with the same field are the data primitives that make the eventual launch cheap. Bake these in now; do not migrate later.

## Recommended stack for the real build

- **Framework:** Next.js 14+ (App Router) + TypeScript
- **Styling:** Tailwind CSS, with the six tokens mapped to `theme.extend.colors`
- **Components:** shadcn/ui or Radix primitives for accessibility
- **Motion:** Framer Motion for screen transitions and the reveal sequence
- **State:** React useState/useReducer; persist to `localStorage` for v1 (no auth or DB yet)
- **Fonts:** `next/font` with Fraunces + Inter (or whatever brand pairs replace them)
- **File structure:** one route per onboarding screen under `app/onboarding/[step]/`, profile under `app/profile/`, shared design tokens in `app/globals.css`

## Open decisions

- Design 4–6 fully realized archetypes (Slow Wanderer is fully designed; Wild Voyager and Night Owl exist as showcase tiles on the landing only — they need full profile pages, palettes mapped to onboarding answers, and tagline copy that's been pressure-tested).
- Decide whether real photography replaces line illustrations on the loves cards in production. Recommendation: keep illustrations for v1, photography in v2.
- Define how preferences map to archetype resolution (the data model is in place; the resolver isn't).
- Persistence strategy beyond localStorage when ready (Supabase + Clerk would be a low-friction pairing).
- Edit profile flow — currently the "Edit profile" link in `profile-result.html` restarts the entire onboarding from welcome. A future version should let users jump directly to specific steps.

## Build sequence (recommended)

1. Translate the design tokens (colors, type, the six CSS vars) into Tailwind config.
2. Build the Profile result page first as a static React component with hardcoded data — beautiful, complete, indexed by archetype.
3. Build the onboarding step components, starting with the loves screen (it's the template).
4. Wire navigation and shared state across steps.
5. Build the welcome and reveal screens.
6. Polish: micro-animations, empty states, edge cases.

Resist the temptation to build the landing page or the itinerary generator first. The Profile is the heart of the product. If the Profile feels precious, everything else follows.
