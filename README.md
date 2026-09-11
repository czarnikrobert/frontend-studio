# Frontend Studio

**A Claude skill that designs and builds distinctive, production-grade frontend interfaces that do not look AI-generated.**

Frontend Studio turns Claude into a design lead and a senior frontend engineer working as one: it commits to a clear aesthetic direction for each brief, backs it with a real design system (spacing, type, color, depth, contrast), and ships clean, accessible, performant code in whatever stack your project already uses.

It merges three layers that used to live in separate skills into one coherent workflow with explicit conflict rules.

---

## Why

Generated UIs tend to converge on the same handful of looks: cream backgrounds with terracotta accents, purple gradients, identical rounded cards with the same soft shadow, ALL-CAPS eyebrows above every heading, a fade-and-slide animation on every section. They are not wrong, they are just defaults that show up regardless of what the product is.

Frontend Studio makes Claude:

- **derive** palette, typography and layout from the subject's own world instead of a default list,
- **plan, then challenge the plan** against a catalog of generated-design tells before writing any code,
- **build on a numeric foundation** so bold designs still feel ordered,
- **never trade the quality floor** (contrast, keyboard access, reduced motion, responsiveness, UI states, performance) for aesthetics.

## What's inside

```
frontend-studio/
├── SKILL.md                        Core workflow, principles, dials, conflict rulings, checklist
├── LICENSE.txt, NOTICE.txt,
│   APACHE-2.0.txt                  License terms bundled with the packaged skill
└── references/
    ├── foundations.md              Design-system layer: hierarchy, spacing and type scales,
    │                               color ramps, elevation, radius, contrast, UI diagnosis
    ├── anti-patterns.md            Catalog of AI-generated design tells, each with an alternative
    ├── engineering.md              Stack detection, React/Next.js, Tailwind v3/v4, plain HTML,
    │                               responsiveness, UI states, forms, accessibility, performance
    ├── motion-and-effects.md       Motion philosophy, technique defaults, effects arsenal,
    │                               Bento motion-engine pattern (all opt-in)
    └── copywriting.md              Writing interface copy and realistic placeholder content
```

`SKILL.md` stays lean; reference files are loaded only when a task needs them (progressive disclosure).

## How it works

1. **Understand the brief:** subject, audience, primary job; new build or existing UI; detect the stack.
2. **Set three dials:** VARIANCE, MOTION and DENSITY (1 to 10), derived from the brief and adjustable live ("calmer", "denser", "more dynamic").
3. **Write a compact design plan:** 4 to 6 named colors, type roles, a layout concept with an ASCII wireframe, principles, and the one memorable element.
4. **Challenge the plan** against the anti-pattern catalog and revise anything that reads like a default.
5. **Build** on the foundation tokens with the engineering rules.
6. **Critique** with a final checklist and, where possible, a visual check.

### Precedence rules

When layers disagree, Frontend Studio resolves them in this order:

1. The brief's own words
2. The quality floor (accessibility, responsiveness, performance, UI states)
3. Creative direction
4. Foundation scales (strong defaults, broken only deliberately and as named tokens)
5. Engineering conventions (the project's real setup first)

### Stack support

The stack is detected from the request, `package.json`, config files, lockfiles and existing code. Works with React, Next.js (App Router with Server Components), Vue, Svelte, Astro or plain HTML/CSS/JS, and with Tailwind CSS v3 or v4, CSS modules or custom properties. With no project present it falls back to React with Tailwind, or a single HTML file when that is what the situation calls for.

## Installation

### Claude Code

Personal skill (available in all projects):

```bash
git clone https://github.com/czarnikrobert/frontend-studio.git
mkdir -p ~/.claude/skills
cp -r frontend-studio/frontend-studio ~/.claude/skills/
```

Project skill (shared with your team through the repo):

```bash
mkdir -p .claude/skills
cp -r path/to/frontend-studio/frontend-studio .claude/skills/
```

### Claude.ai and the Claude apps

Download `frontend-studio.zip` from the [Releases](../../releases) page and upload it in the Skills section of Claude's settings. Skills must be enabled for your plan and account.

## Usage examples

Once installed, the skill triggers on frontend requests automatically. For example:

- "Build a landing page for a small bakery that ships sourdough starters."
- "Make this settings page look less generic." (with the file attached)
- "A dashboard for dispatchers tracking 40 delivery vans, dense, dark theme."
- "Portfolio for a landscape photographer, calm, lots of space, one striking interaction."
- "Restyle our pricing section, keep our brand blue."

You can steer it with the dials directly: "V8 M3 D2", or in plain words: "more asymmetric, less motion".

## Conflict rulings

The source skills disagreed on several points. Frontend Studio settles them in favor of creative freedom, as long as the quality floor holds:

| Topic | Ruling |
|---|---|
| Fonts | No fixed allowlist; chosen per brief; overused families need a reason |
| Motion | One orchestrated moment plus responsive motion by default; perpetual loops only at MOTION 7+ |
| Numbers in dense UI | Tabular numerals; monospace only when the aesthetic calls for it |
| Border radius | A radius hierarchy by component role, not one radius everywhere |
| Spacing | Default scale; off-scale values only as named, justified tokens |
| Custom cursors | Only for expressive, experimental pages; never in apps or forms |
| Black | Derived from the palette's own neutral ramp, never a reflex `#000` or `#111` |

## Origins and credits

Frontend Studio is a merge and rewrite of these sources:

- **`frontend-design`** by Anthropic, licensed under Apache 2.0. The design-direction process, the aesthetic-cluster calibration and the writing guidance are adapted from it. See [`NOTICE`](NOTICE) and [`licenses/APACHE-2.0.txt`](licenses/APACHE-2.0.txt).
- **`frontend`**, a Polish-language community skill focused on engineering conventions, UI scales, performance rules and an effects arsenal. Its content was translated, restructured and reconciled with the other sources.
- **[`refactoring-ui-skill`](https://github.com/s0xDk/refactoring-ui-skill)** by s13k, licensed under MIT. The `frontend` skill used it as its source of spacing, type, color and shadow scales, and those scales carry over into this project's foundations layer. See [`licenses/MIT-refactoring-ui-skill.txt`](licenses/MIT-refactoring-ui-skill.txt).
- **The foundations layer** (`references/foundations.md`) was rewritten for this project on top of those scales. The underlying design rules come from the book *Refactoring UI* by Adam Wathan and Steve Schoger. This project does not reproduce the book's text and is not affiliated with or endorsed by its authors. If the foundations help you, [buy the book](https://www.refactoringui.com/).

## Contributing

Issues and pull requests are welcome. Useful contributions:

- new entries for the anti-pattern catalog, with a concrete alternative for each,
- stack-specific notes in `engineering.md` (Vue, Svelte, Astro),
- before-and-after examples showing the workflow on a real brief.

Please keep `SKILL.md` under about 500 lines and put detail in the reference files.

## License

MIT for original content, see [`LICENSE`](LICENSE). Portions adapted from Anthropic's `frontend-design` skill remain under the Apache License 2.0, and scales derived from `refactoring-ui-skill` retain its MIT notice. See [`NOTICE`](NOTICE).
