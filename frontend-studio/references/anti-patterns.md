# Anti-patterns: the tells of generated design

Use this catalog in two places: when reviewing the design plan (Step 3) and during the final critique (Step 5).

**Important:** every pattern here is legitimate for *some* brief. If the user explicitly asks for one, follow the brief exactly. The problem is not the pattern; it is reaching for it by default, regardless of subject. If you notice one in your plan, ask whether this specific brief chose it. If not, replace it.

## Contents
1. The five aesthetic clusters
2. Typography tells
3. Color tells
4. Layout and composition tells
5. Component tells
6. Motion tells
7. Content and data tells
8. Asset tells

---

## 1. The five aesthetic clusters

Generated design currently clusters around these looks. Each is a complete default that appears whatever the subject is:

1. **Warm editorial:** cream background (near `#F4F1EA`), high-contrast serif display, terracotta or clay accent (near `#D97757`, which is also Anthropic's own interface accent, so it reads as a tell on a user's brief).
2. **Dark with acid accent:** near-black background with one bright acid-green or vermilion accent.
3. **Broadsheet:** hairline rules, zero border radius, dense newspaper columns.
4. **SaaS card kit:** content chopped into identical rounded cards, one radius on everything, the same soft grey shadow (`rgba(0,0,0,.1)`) under each, gradient washes as decoration.
5. **Template chrome:** tracked-out ALL-CAPS eyebrow above every heading, meta strings joined with middle dots (`A · B · C`), labels built as `WORD — fragment` with a spaced em dash, tinted near-black (`#0B0B0B`, `#111`) standing in for black, monospace for small data labels, an arrow appended to every link and button.

Also classic: **purple or blue gradients on white**, and purple/violet glows, often called "AI purple".

**Instead:** derive palette, type and layout from the subject's own world (materials, era, industry, vernacular). Write down where each choice comes from.

## 2. Typography tells

| Tell | Instead |
|---|---|
| Inter, Roboto, Arial, system stacks, or the same "safe interesting" font every time (e.g. Space Grotesk) | Pick for this brief; rotate across projects; justify overused families |
| One word in a headline accented with italic, bold or a different color | Let the whole headline work, or make the type treatment itself the design |
| ALL-CAPS labels and eyebrows everywhere | Sentence case; use caps only where it carries a real convention |
| Unnecessary labels above content that already explains itself | Remove the label |
| Gradient-filled text on large headlines | Solid color with strong typography |
| Screaming H1 (huge size doing all the work) | Build hierarchy with weight and color first, size last |
| Monospace for small data labels by reflex | Tabular numerals in the body face, unless the aesthetic is genuinely technical |

## 3. Color tells

| Tell | Instead |
|---|---|
| Purple/violet glows, neon gradients | A neutral base with one accent chosen for the subject |
| Reflex `#000000` or reflex `#111` | The darkest step of your own neutral ramp |
| Several accents competing | One accent; semantic colors only for states |
| Oversaturated neon accents | Saturation chosen within a designed ramp |
| Gradient washes as generic decoration | Backgrounds with a reason: texture, photography, material, data |
| Outer glows around buttons and cards | A subtle inner border or a tinted shadow |

## 4. Layout and composition tells

| Tell | Instead |
|---|---|
| Hero: big number, small label, supporting stats, gradient accent | Open with the most characteristic thing in the subject's world |
| Centered hero text over a darkened stock image | Asymmetric composition, split layout, or an image that fades into the background color, chosen for the brief |
| Three equal cards in a row | Zig-zag, asymmetric grid, horizontal scroll, a list, or a table: whatever the content actually is |
| Numbered markers (01 / 02 / 03) on non-sequential content | Numbers only for real sequences (steps, timelines, rankings) |
| Every section the same height and rhythm | Vary rhythm by content importance |
| Awkward floating elements with uneven gaps | Snap everything to the spacing scale; more space around groups than inside |

## 5. Component tells

| Tell | Instead |
|---|---|
| Cards for everything | Cards only when elevation means something; otherwise spacing, dividers, background steps |
| One border radius on every element | A radius hierarchy by role |
| The same soft shadow under everything | Elevation levels by Z position |
| `shadcn/ui` or other kits in their default state | Customize radius, color and shadow to the project tokens |
| Emoji used as icons | One icon family with a consistent stroke, or custom SVG |
| Generic spinners | Skeletons shaped like the content |
| Custom cursors in apps | Native cursor; custom only for expressive experimental pages |

## 6. Motion tells

| Tell | Instead |
|---|---|
| Fade-and-slide-up on every section | One orchestrated entrance moment |
| Hover animation on every card | Hover feedback where the element is actually interactive |
| Linear easing | Springs or custom cubic-bezier curves |
| Scroll listeners on `window` | IntersectionObserver, CSS scroll-driven animations, or library hooks |
| Animating `width`, `height`, `top`, `left` | `transform` and `opacity` only |

## 7. Content and data tells

| Tell | Instead |
|---|---|
| "John Doe", "Jane Smith", "Jan Kowalski" | Realistic, varied names fitting the audience and locale |
| "Acme", "Nexus", "Quantum" style company names | Names that fit the brief's industry and tone |
| Round, predictable numbers (99.99%, 50%, 10k+) | Organic figures (47.2%, 1,284) |
| Copy clichés: "Elevate", "Seamless", "Next-gen", "Unleash", "Revolutionize" | Concrete verbs describing what actually happens |
| "Submit", "Click here", "Learn more" everywhere | Buttons that say exactly what happens |
| `Label: value` pairs where context is obvious | "12 left", "Due Friday" |
| Lorem ipsum | Real or realistic content from the brief |

See `copywriting.md` for the full writing guidance.

## 8. Asset tells

| Tell | Instead |
|---|---|
| Generic stock photography, hot-linked Unsplash images | The brief's real assets; otherwise seeded placeholders like `https://picsum.photos/seed/{word}/800/600` clearly marked as placeholders |
| Egg-shaped SVG blobs as avatars | Initials avatars or seeded placeholder images |
| Scaled-up small icons as illustrations | Icons inside colored shapes, or a real illustration |
