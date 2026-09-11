# Foundations

The numeric and systemic layer: how to make an interface feel ordered before it feels stylish. These are strong defaults. Break them deliberately and as named tokens, never as random one-off values.

## Contents
1. Order of work
2. Hierarchy
3. Spacing and sizing
4. Typography
5. Color
6. Depth and elevation
7. Borders, radius and separation
8. Images and icons
9. Finishing touches
10. Tailwind mapping
11. Diagnosing an existing interface

---

## 1. Order of work

- **Start with a feature, not the shell.** Design the thing the user actually does (the booking form, the photo grid, the invoice table) before the navigation, footer or layout chrome. The shell should be shaped by the content, not the other way round.
- **Work in grayscale first.** Establish hierarchy with space, size, weight and contrast before adding color. If the layout only works because of color, the hierarchy is weak.
- **Low fidelity until the structure holds.** Decide what exists and where before polishing shadows and gradients.
- **Design only what you are building now.** Leave out speculative features; do not draw placeholders for things with no plan.
- **Pick a personality early.** Type, color, radius and wording all express it. Decide it in the design plan so all four agree.

## 2. Hierarchy

Hierarchy is the single biggest difference between amateur and professional interfaces.

- **Not everything is equally important.** Decide the primary, secondary and tertiary content on every screen before styling.
- **Three tools, in this order of subtlety:** color/contrast (subtlest), weight, size (loudest). Reach for size last; oversized headings are a common way of shouting.
- **Emphasize by de-emphasizing.** When the important element does not stand out, soften its competitors instead of making it louder.
- **Text colors:** at most three (primary, secondary, tertiary), all meeting contrast requirements. Lighter tones are for disabled states and large text only.
- **Weights:** normal (400) or medium (500) for body, semibold (600) or bold (700) for emphasis. Avoid weights under 400 for UI text; de-emphasize with color or size instead.
- **Labels are a last resort.** "12 left in stock" beats "Stock: 12". When a label is needed, make it secondary and let the value lead.
- **Separate visual hierarchy from document hierarchy.** An `h1` does not have to be the biggest thing on the page; section titles often work best small and quiet while the content is the hero.
- **Balance weight and contrast.** Heavy, dense elements (icons, bold text) look darker; compensate with a softer color. Thin elements look lighter; compensate with more weight or contrast.
- **Button hierarchy follows importance, not semantics.** Primary: solid, high contrast, usually one per view. Secondary: outline or low-contrast fill. Tertiary: link style. A destructive action outside a confirmation dialog is tertiary; a solid red button belongs inside the confirmation dialog.

## 3. Spacing and sizing

- **Start with too much space, then remove.** Crowding is the default failure; generous space almost always looks more deliberate.
- **More space around a group than inside it.** Proximity is how the eye reads relationships. A label must be closer to its input than to the previous field.
- **Use a constrained scale.** Values close together (e.g. 12 vs 13px) are indistinguishable and create inconsistency. Each step should differ from its neighbor by at least about 25%.

Default spacing scale (px): **4, 8, 12, 16, 24, 32, 48, 64, 96, 128, 192, 256, 384**

- **Do not fill the screen just because it is there.** Give content the width it needs (forms around 480 to 640px, prose around 65ch) and let the rest be space.
- **Fixed and flexible.** Sidebars and inputs usually want fixed or max widths; main content areas stretch. Prefer `max-width` over percentage widths for elements.
- **Sizes do not scale proportionally.** On small screens, large elements (headings, hero media) should shrink faster than small ones (body text, buttons). Padding on a large button is not simply the small button's padding multiplied.
- **Dense is a choice, not an accident.** High-density interfaces pick smaller steps from the same scale; they do not invent new values.

## 4. Typography

Default type scale (px): **12, 14, 16, 18, 20, 24, 30, 36, 48, 60, 72**. Larger display sizes are allowed as named tokens for expressive heroes.

- **Use px or rem for font sizes, not em.** Nested em values drift off the scale.
- **Line length:** about 45 to 75 characters for body text. Constrain paragraphs even inside wide containers.
- **Line height is inversely related to size.** Body text around 1.5 to 1.7; large headings around 1.0 to 1.2. Longer lines need more line height.
- **Letter spacing:** tighten large headings slightly; loosen small uppercase text if you use it (and use it rarely, see anti-patterns).
- **Alignment:** left-align almost everything in left-to-right languages. Center only short, standalone blocks. Right-align numbers in tables so digits line up. Justified text needs hyphenation or it creates rivers.
- **Align mixed sizes on the baseline**, not on the vertical center, when a large and small text sit on one line.
- **Tabular numerals** (`font-variant-numeric: tabular-nums`) for any column or changing number.
- **Choose typefaces with enough weights** (at least 400/500/600/700) and good legibility at small sizes for UI text. Characterful display faces can be used for headlines only.
- **Links in text need more than color**: underline or weight so they survive color-blindness and grayscale.

## 5. Color

### Building a palette
- **You need more colors than you think, but fewer hues.** A real UI palette contains: one neutral ramp, one accent ramp, and semantic ramps (error, warning, success, info) only if the interface has those states. Chart series colors are separate and only when needed.
- **Every color is a ramp of about 9 to 10 shades** (100 to 900), not a single value. Pick the base (the shade that works as a button background), then the darkest (text on light) and lightest (tinted backgrounds), then fill the steps between.
- **Define colors in HSL** (or OKLCH) so relationships stay understandable. Do not generate shades at runtime with `lighten()`, `darken()` or `color-mix()` for hover states; define them as tokens.
- **Keep ramps vibrant at the ends.** As lightness moves toward the extremes, increase saturation slightly, otherwise light and dark shades wash out. Rotating the hue a few degrees toward a brighter hue (yellow, cyan, magenta) when lightening, or toward a darker hue (red, green, blue) when darkening, keeps shades lively.
- **Neutrals are rarely pure grey.** Give the neutral ramp a slight temperature (cool blue-ish or warm yellow-ish) that suits the brand. Use one neutral ramp throughout; do not mix warm and cool greys.

### Using color
- **One accent does the talking.** Semantic colors signal state and never compete with the accent as decoration.
- **Never grey text on a colored background.** Use a shade of the background's own hue, or white with reduced opacity, so it reads as muted rather than dirty.
- **Never color as the only signal.** Pair with an icon, shape, pattern or text (errors, status, chart series).
- **Dark mode is its own design.** Do not invert; rebuild the ramps. Lighter surfaces indicate elevation in dark mode.

### Contrast requirements (WCAG 2.1 AA, the quality floor)
| Element | Minimum ratio |
|---|---|
| Body text (under 24px, or under 18.66px bold) | 4.5:1 |
| Large text (24px+, or 18.66px+ bold) | 3:1 |
| Essential UI boundaries (input border when it is the only affordance, focus ring, icon-only buttons) | 3:1 |
| Decorative dividers, disabled states | no requirement |

- **Flip contrast for colored surfaces:** instead of white text on a light-ish brand color, try dark text on a light tint of that color.
- **Text on images or glass** must meet contrast against both the lightest and darkest part of what is behind it.

## 6. Depth and elevation

- **Light comes from above.** Raised elements get a lighter top edge and a shadow below; inset elements (inputs, wells) get a darker top edge.
- **Shadows mean position on the Z axis**, not decoration. Choose a level by how "high" the element sits.

Default elevation tokens (tint the shadow color toward the background hue if needed; keep geometry and opacity):

```css
--shadow-e1: 0 1px 3px hsla(0 0% 0% / .2);    /* buttons, cards at rest */
--shadow-e2: 0 4px 6px hsla(0 0% 0% / .2);    /* dropdowns */
--shadow-e3: 0 5px 15px hsla(0 0% 0% / .2);   /* hovered or lifted cards */
--shadow-e4: 0 10px 24px hsla(0 0% 0% / .2);  /* popovers, dragged items */
--shadow-e5: 0 15px 35px hsla(0 0% 0% / .2);  /* modals */
```

- **Two-part shadows look more physical:** a larger soft shadow for the light source plus a small, tight, darker shadow for the contact point. The tight one should fade as elevation increases.
- **Use one shadow system per project.** Mixing unrelated shadow values breaks the illusion.
- **Interaction changes elevation:** hover can raise a card one or two levels; pressing (`:active`) drops it one level or nudges it down by 1px.
- **Depth without shadows:** overlapping elements, background color steps, and lighter surfaces on top of darker ones.

## 7. Borders, radius and separation

- **Use fewer borders.** Before adding a border, try more space, a background color step, or a shadow. Borders everywhere make interfaces look busy.
- **Radius hierarchy:** pick radii by role from 4, 8, 12, 16, 24, 32px: one for large containers, one for controls (buttons, inputs), optionally one for chips/tags. Nested radii: inner radius equals outer radius minus the padding between them.
- **Do not mix sharp and rounded corners** within the same family of elements unless it encodes a difference.
- **Radius expresses personality:** small or zero reads serious and precise; large reads friendly and soft. Choose in the design plan.
- **Accent borders** (a colored top or left edge on a card or alert) add character cheaply when they carry meaning.

## 8. Images and icons

- **Text over photos needs help:** a darkening or lightening overlay, a lower-contrast image, a colorized image, or a text shadow with a large, soft blur. Check contrast on the busiest region.
- **Everything has an intended size.** Do not scale small icons (16 to 24px designs) up to 48px; they look clumsy. Put the small icon inside a shape with a background color instead. Do not shrink detailed illustrations or screenshots to tiny sizes; crop or simplify them.
- **Control user-uploaded content:** fixed aspect-ratio containers with `object-fit: cover`, and a subtle inner border or shadow so light images do not bleed into light backgrounds.
- **Icon consistency:** one icon family, one stroke width across the project.

## 9. Finishing touches

- **Replace defaults with something considered:** bullet points can be icons or checkmarks, quotes can become visual elements, form controls can carry the brand color.
- **Add color through backgrounds, not just text:** alternate section backgrounds, subtle patterns or gradients built from two close hues, when they fit the aesthetic.
- **Empty states are a feature.** Illustrate or explain, and put the primary action right there. Hide filters and tabs that do nothing without data.
- **Think outside the component defaults:** a table does not have to be rows of equal text; a dropdown can have sections, icons and descriptions; radio buttons can become selectable cards.

## 10. Tailwind mapping

Spacing and sizing (padding, margin, gap, width, height):

| px | 4 | 8 | 12 | 16 | 24 | 32 | 48 | 64 | 96 | 128 | 192 | 256 | 384 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| class | `1` | `2` | `3` | `4` | `6` | `8` | `12` | `16` | `24` | `32` | `48` | `64` | `96` |

Intermediate Tailwind steps (`5`, `7`, `9`, `10`, `11`, `14`, `20`, `28`, `36`, `40`, `44`, `52`, `56`, `60`, `72`, `80`) are off-scale. Use them only as a named, justified exception.

Type: `text-xs` 12 · `text-sm` 14 · `text-base` 16 · `text-lg` 18 · `text-xl` 20 · `text-2xl` 24 · `text-3xl` 30 · `text-4xl` 36 · `text-5xl` 48 · `text-6xl` 60 · `text-7xl` 72.

Opacity steps: `/5`, `/10`, `/20`, `/40`, `/60`, `/80`.

Define project tokens once: Tailwind v3 in `theme.extend` of `tailwind.config`, Tailwind v4 in a `@theme` block in CSS. Elevation tokens `e1` to `e5` go there too.

## 11. Diagnosing an existing interface

Walk through in this order and note findings ranked by impact:

1. **Purpose:** is it obvious within five seconds what the screen is for and what the main action is?
2. **Hierarchy:** is there one clear primary element? Are there more than three text colors or more than two weights competing?
3. **Spacing:** are groups separated more than their members? Are values consistent, or is every gap slightly different?
4. **Typography:** line lengths, line heights, number of sizes in use, alignment of numbers.
5. **Color:** how many accents are fighting? Grey text on color? Any contrast failures?
6. **Depth and separation:** borders everywhere? Random shadows? Mixed radii?
7. **Consistency:** the same component looking different in different places.
8. **States:** what happens when loading, empty, erroring, disabled, focused?
9. **Responsiveness:** does it survive 360px wide and 1440px wide?

Report the three to five most impactful problems in plain language before rewriting.
