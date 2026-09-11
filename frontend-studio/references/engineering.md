# Engineering

How to turn the design into production-grade code. The project's real setup always beats the preferences in this file.

## Contents
1. Stack detection
2. Dependency verification
3. React and Next.js conventions
4. Tailwind CSS v3 and v4
5. Plain HTML/CSS/JS
6. Responsiveness
7. UI states
8. Forms
9. Accessibility floor
10. Performance
11. Icons, images and component kits

---

## 1. Stack detection

Before writing code, look for evidence of the existing stack. Check in this order and stop guessing once you have an answer:

1. **User's words.** An explicit stack in the request wins.
2. **`package.json`:** framework (`next`, `react`, `vue`, `svelte`, `astro`, `@angular/core`), styling (`tailwindcss` and its major version, `styled-components`, `@emotion/*`, `sass`), component library (`@radix-ui/*`, shadcn patterns in `components/ui`, `@mui/*`, `@chakra-ui/*`), animation (`framer-motion`/`motion`, `gsap`), icons.
3. **Config files:** `next.config.*`, `vite.config.*`, `astro.config.*`, `nuxt.config.*`, `svelte.config.*`, `tailwind.config.*`, `postcss.config.*`, `tsconfig.json`.
4. **Lockfile:** `pnpm-lock.yaml`, `yarn.lock`, `bun.lockb`, `package-lock.json` tells you which install command to give.
5. **Existing code conventions:** file naming, TypeScript vs JavaScript, CSS modules vs utility classes, how existing components are structured. Match them.

**Fallback when there is no project:**
- In an environment that renders React (for example claude.ai artifacts): React function component with Tailwind core utilities, single file, default export, no required props.
- When the user wants a standalone page, a file to open in a browser, or mentions plain HTML: a single HTML file with inline CSS and JS.
- Otherwise: React (Vite or Next.js) with Tailwind.

State the detected or chosen stack in one line before the code.

## 2. Dependency verification

Before importing any external package, confirm it is installed (in `package.json`) or available in the environment. If it is not, give the exact install command using the project's package manager before the code. Never assume a library exists. In sandboxed environments with a fixed library list, use only what that environment provides.

## 3. React and Next.js conventions

- **Server Components by default** in the Next.js App Router. Global state and interactivity work only in Client Components.
- **Isolate interactivity:** anything with state, effects, event handlers or animation libraries becomes a small leaf component with `'use client'` at the top. Server Components render the static layout around it.
- **Providers** (theme, state, query clients) live in a dedicated Client Component wrapper.
- **State:** local `useState`/`useReducer` for isolated UI. Global stores only to avoid deep prop drilling, not by default.
- **Effects clean up after themselves:** listeners, observers, timers and animation instances are disposed in the `useEffect` return.
- **Keys and lists:** stable keys, never array indexes for reorderable lists.
- **Composition over configuration:** small components with clear props rather than one component with twenty boolean flags.

## 4. Tailwind CSS v3 and v4

- **Check the major version first** and never mix syntax.
- **v3:** tokens in `theme.extend` in `tailwind.config.js`; PostCSS plugin `tailwindcss`.
- **v4:** tokens in a `@theme` block in CSS; do not use the old `tailwindcss` PostCSS plugin, use `@tailwindcss/postcss` or the Vite plugin; `@import "tailwindcss";` replaces the three `@tailwind` directives.
- **Define tokens once** (colors as ramps, elevation `e1` to `e5`, radii by role, fonts) and use them by name. Repeating the same arbitrary value (`shadow-[...]`, `text-[17px]`) across files is a smell.
- **Arbitrary values** are for genuine one-offs tied to a named reason, not for bypassing the scale.
- In environments without a Tailwind compiler (pre-built stylesheets), only core utility classes work; arbitrary values and custom config will not.

## 5. Plain HTML/CSS/JS

- Tokens as CSS custom properties on `:root`, grouped: color ramps, spacing, type, radius, elevation, motion durations and easings.
- Semantic structure (`header`, `nav`, `main`, `section`, `article`, `footer`), one `h1`.
- CSS layers or a clear order (reset, tokens, base, layout, components, utilities) to avoid specificity fights.
- Watch specificity collisions: a `.section` class rule and an element-level rule can silently override each other's spacing.
- Vanilla JS in a module script at the end, with progressive enhancement: the page works before JS runs.
- External libraries from a reliable CDN only when needed, with `defer`.

## 6. Responsiveness

- Standard breakpoints (`sm`, `md`, `lg`, `xl`); design mobile first.
- Constrain page content with a max width (e.g. `max-w-7xl mx-auto`) and horizontal padding.
- Full-height sections: `min-h-[100dvh]`, never `h-screen` (mobile browser toolbars break `100vh`).
- Use CSS Grid for multi-column layouts instead of percentage math like `w-[calc(33%-1rem)]`.
- Fixed-width sidebars, flexible main area; `max-width` on elements rather than percentage widths.
- Headings and hero media shrink faster than body text on small screens.
- High-variance layouts collapse to a clean single column under 768px.
- Test mentally at 360px, 768px, 1024px and 1440px.
- Touch targets at least 44 by 44px on touch interfaces.

## 7. UI states

Whenever data or async work is involved, deliver all of these:

- **Loading:** skeletons shaped like the final layout, not generic spinners. Keep layout stable (no content jump).
- **Empty:** explain what will appear here and offer the primary action to create it.
- **Error:** inline, specific, with a way to recover (semantic color plus icon plus text).
- **Disabled:** visibly different, not just lower opacity on text that then fails contrast silently; explain why when it is not obvious.
- **Active/pressed feedback:** a 1px downward nudge or `scale(0.98)`, with elevation dropping one level.
- **Focus:** a visible focus ring with at least 3:1 contrast.
- **Success:** confirm with the same verb as the action ("Publish" results in "Published").

## 8. Forms

- Label above the input, always visible (placeholders are not labels).
- Helper text in the markup, connected with `aria-describedby`.
- Error message directly below the field, connected the same way, with `aria-invalid`.
- Consistent small gap (8px) between label, input and helper; larger gap between fields.
- An input border that is the only visual affordance needs 3:1 contrast with the background. Decorative dividers are a separate, softer token.
- Correct `type`, `inputmode` and `autocomplete` attributes.
- Validate on blur or submit, not on every keystroke; never clear the user's input on error.

## 9. Accessibility floor

Non-negotiable regardless of aesthetic direction:

- Contrast per the table in `foundations.md`.
- Keyboard: everything interactive reachable and operable, logical tab order, visible focus, no keyboard traps, Escape closes overlays.
- Semantics: real `button` and `a` elements, headings in order, landmarks, lists as lists, tables for tabular data.
- Names: every control has an accessible name; icon-only buttons get `aria-label`.
- Images: meaningful `alt`, empty `alt=""` for decoration.
- Motion: honor `prefers-reduced-motion` by disabling non-essential animation and parallax.
- Color is never the only signal.
- Language attribute set on the document.

## 10. Performance

- Animate only `transform` and `opacity`.
- Grain and noise overlays only on fixed, `pointer-events: none` pseudo-elements, never on scrolling containers.
- `will-change` sparingly and only on elements that are about to animate.
- `z-index` only for real stacking contexts (sticky headers, modals, overlays, toasts), from a small named scale.
- Images: correct dimensions, `loading="lazy"` below the fold, modern formats, `width`/`height` or aspect-ratio to prevent layout shift.
- Fonts: limit families and weights, `font-display: swap`, preload the primary face.
- Heavy effects (WebGL, canvas, perpetual animations) isolated so they do not re-render the surrounding tree; see `motion-and-effects.md`.

## 11. Icons, images and component kits

- **Icons:** use the project's existing icon set. Otherwise pick one family available in the environment (for example Phosphor, Radix Icons or Lucide) and set one stroke width project-wide.
- **No emoji** in code, markup or alt text as icons or decoration.
- **Placeholder images:** seeded placeholders such as `https://picsum.photos/seed/{word}/800/600`, clearly marked for replacement. Prefer the brief's real assets.
- **Component kits** (shadcn/ui, Radix, MUI and others) are fine as a base, never in their default visual state: adapt radius, color, shadow and type to the project tokens.
