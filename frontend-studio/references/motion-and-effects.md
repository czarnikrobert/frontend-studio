# Motion and effects

Read this when the MOTION dial is 4 or higher, or when the user asks for animation, scroll effects, Bento grids or a named effect. Everything here is opt-in: an effect earns its place by serving the brief, not by being available.

## Contents
1. Motion philosophy
2. Technique defaults
3. Performance rules for motion
4. Library boundaries
5. Effects arsenal
6. Pattern: Bento motion engine

---

## 1. Motion philosophy

- **Two kinds of motion.** *Responsive motion* answers a user action (open, expand, confirm, drag, reorder) and shows what changed; it is almost always welcome. *Ambient motion* happens on its own (entrances, loops, parallax); it must be rationed.
- **Default budget (MOTION 1 to 6):** one orchestrated ambient moment, such as a page-load sequence or a single reveal, plus responsive motion. This lands better than scattered effects everywhere.
- **High budget (MOTION 7 to 10):** scroll-driven storytelling, physics, perpetual micro-interactions inside components. Still with a clear hierarchy: one lead effect, supporting effects quieter.
- **Reduced motion is part of the design.** Under `prefers-reduced-motion: reduce`, remove parallax, loops and large movement; keep instant state changes and gentle opacity fades.

## 2. Technique defaults

- **Plain HTML:** CSS transitions and keyframes first; `IntersectionObserver` or CSS scroll-driven animations (`animation-timeline`) for reveals. No `scroll` event listeners on `window`.
- **React:** the Motion library (`motion` / `framer-motion`) when installed or available.
- **Easing:** no linear easing for UI movement. A good general curve: `cubic-bezier(0.16, 1, 0.3, 1)`. Springs for physical interactions, starting around `type: "spring", stiffness: 100, damping: 20`, then tune by feel.
- **Durations:** micro feedback 100 to 200ms; component transitions 200 to 400ms; page-level choreography up to about 800ms total. Exits faster than entrances.
- **Staggering:** reveal lists and groups with a small stagger (roughly 40 to 100ms per item) through `staggerChildren` or `animation-delay: calc(var(--i) * 60ms)`. Parent and children must live in the same client tree.
- **Layout animation:** `layout` and `layoutId` in Motion for reordering and shared-element transitions.
- **Pointer-driven effects** (magnetic buttons, tilt, spotlight): use motion values (`useMotionValue`, `useTransform`) or direct style updates via `requestAnimationFrame`, never React state on every pointer move.

## 3. Performance rules for motion

- Animate `transform` and `opacity` only.
- Perpetual loops live in their own small Client Component, wrapped in `React.memo`, so they never re-render the parent layout.
- Pause off-screen loops and canvases (IntersectionObserver, `document.visibilityState`).
- Every effect started in `useEffect` is torn down in its cleanup.
- Target 60fps on a mid-range phone; if an effect cannot hold it, simplify it on small screens.

## 4. Library boundaries

- **Motion/Framer Motion** is the default for UI motion in React.
- **GSAP (with ScrollTrigger)** for complex scroll storytelling and timelines.
- **Three.js / WebGL / canvas** for 3D scenes and generative backgrounds.
- Never mix GSAP or Three.js with Motion inside the same component tree. Isolate GSAP and WebGL in their own components with full cleanup in `useEffect`.
- Always verify the library is installed or available before using it.

## 5. Effects arsenal

A menu of named effects to draw from when the brief calls for them. Choose at most one lead effect per view.

### Navigation and menus
- **Dock magnification:** icons scale smoothly with pointer proximity.
- **Magnetic button:** the control drifts toward the pointer.
- **Gooey menu:** sub-items separate like a viscous liquid.
- **Dynamic island:** a pill that morphs to show status or alerts.
- **Radial context menu:** a circular menu opening at the click point.
- **Floating speed dial:** a FAB that fans out into a curved row of actions.
- **Mega menu reveal:** full-width dropdowns with a staggered fade.

### Layout and grids
- **Bento grid:** asymmetric tile grouping of mixed sizes.
- **Masonry:** grid without fixed row heights.
- **Chroma grid:** tiles with slowly shifting color fields.
- **Split-screen scroll:** two halves scrolling in opposite directions.
- **Curtain reveal:** the hero parts like a curtain on scroll.

### Cards and containers
- **Parallax tilt card:** 3D tilt following the pointer.
- **Spotlight border:** the border lights up under the pointer.
- **Glass panel:** frosted backdrop blur plus a 1px inner border (for example `border-white/10`) and a faint inset top highlight for edge refraction. Text on glass must meet contrast against the lightest and darkest content behind it.
- **Holographic foil:** iridescent reflections on hover.
- **Swipe stack:** a stack of cards dismissed by swiping.
- **Morphing modal:** a button that expands into a full dialog.

### Scroll
- **Sticky stack:** cards that stick and layer over each other.
- **Horizontal scroll hijack:** vertical scrolling pans a horizontal gallery. Always provide a normal fallback for keyboard and reduced motion.
- **Scrubbed sequence:** a video or image sequence tied to scroll position.
- **Zoom parallax:** a background that zooms gently with scroll.
- **Scroll progress path:** an SVG line that draws as you scroll.
- **Liquid page transition:** page changes with a viscous wipe.

### Galleries and media
- **Dome gallery:** images arranged on a 3D dome.
- **Coverflow:** a 3D carousel with the center item in focus.
- **Drag-to-pan canvas:** a borderless grid dragged in any direction.
- **Accordion image slider:** image strips that expand on hover.
- **Image trail:** images appearing along the pointer path.
- **Glitch image:** RGB-split distortion on hover.

### Type and text
- **Kinetic marquee:** endless bands that react to scroll direction.
- **Text mask reveal:** type as a window onto video or imagery.
- **Text scramble:** characters decode into the final word.
- **Circular text path:** text rotating along a circle.
- **Stroke gradient animation:** a gradient traveling along outlined type.
- **Kinetic type grid:** letters that move away from the pointer.

### Micro-interactions
- **Particle burst:** a CTA dissolving into particles on success.
- **Liquid pull-to-refresh:** a droplet-like refresh indicator.
- **Skeleton shimmer:** a sheen passing across placeholders.
- **Direction-aware hover:** fill entering from the side the pointer came from.
- **Ripple:** waves from the click point.
- **SVG line drawing:** vectors drawing their own outlines.
- **Mesh gradient background:** slow organic color fields.
- **Depth blur:** background blur to push focus onto the foreground action.

## 6. Pattern: Bento motion engine

A recognizable pattern for SaaS feature sections and product dashboards: a Bento grid where every tile shows a small, living demonstration. Use it when the brief is a software product that benefits from showing behavior. Be aware it is also a widely copied look, so adapt palette, type and radius to the brief rather than using it as a template.

**Structure**
- Background one step off the lightest neutral; tiles on the surface color with a quiet decorative border.
- Tile radius from the container role in the radius hierarchy; inner elements one smaller step.
- Tile shadow `e1` at rest, `e3` on hover.
- Generous inner padding (32 to 48px).
- Titles and descriptions may sit below the tiles for a gallery-like presentation.
- Example grid: row one with three columns, row two split 70/30.

**Tile archetypes**
1. **Self-sorting list:** a vertical stack that reorders itself periodically with `layoutId`, suggesting prioritization.
2. **Command input:** a search or prompt field with a typewriter effect, a blinking caret and a shimmering "working" state.
3. **Live status:** a schedule or status board with gently pulsing indicators and a notification badge that pops with overshoot, then leaves.
4. **Data stream:** a seamless horizontal carousel of metrics looping at a calm speed.
5. **Focus mode:** a document where a block highlights in sequence and a small floating toolbar slides in.

**Engine rules**
- Springs, not linear easing.
- Dynamic lists inside `AnimatePresence`.
- Each perpetual tile is its own memoized Client Component; loops pause when off-screen.
- Under reduced motion, tiles show a static representative frame.
