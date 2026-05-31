# ADR-0003: Frontend Framework Stack

**Status:** Accepted  
**Date:** 2026-05-30  
**Author:** Sameera Leola

---

## Context

Project Igniter follows a UI-first development philosophy: build the frontend dashboard first, define what needs to be built, then build the backend based on what the UI requires. This means the frontend stack is the first real technical decision after hosting.

The dashboard will include repeated patterns: project cards, status indicators, phase trackers, milestone lists, and ADR indexes. The site also doubles as a guided learning deliverable, which means it needs to be readable, fast, and easy to maintain by someone who is not a full-time frontend developer.

The choices were:

1. Plain HTML + CSS (no framework, no build step)
2. Astro + Tailwind CSS + Alpine.js (static-first framework with lightweight interactivity)
3. SvelteKit (reactive framework, full SSR/SSG capability)
4. Next.js or Nuxt (React/Vue-based, full-stack capable)

---

## Decision

The Project Igniter dashboard is built with **Astro + Tailwind CSS + Alpine.js**.

- **Astro:** Site framework. Handles routing, component composition, and static site generation. Deploys to Cloudflare Pages with zero additional configuration.
- **Tailwind CSS:** Utility-first styling. Paired directly with the AiASH brand color system already defined as CSS variables.
- **Alpine.js:** Lightweight JavaScript for interactivity (dropdowns, toggles, tab panels). No virtual DOM, no build complexity. Loaded as a script tag.

---

## Reasoning

### Why not plain HTML?

The dashboard has repeated component patterns: project cards, status badges, phase trackers, nav bars. Writing those in plain HTML means copying and editing the same blocks every time a new section is added. A component-based framework writes it once and reuses it everywhere. Plain HTML also has no upgrade path to dynamic features without a full rewrite.

### Why not SvelteKit?

SvelteKit is an excellent framework and a clean upgrade path if dynamic capability is needed at scale. It was kept as an explicit upgrade option. For v1 scope, it adds reactive state management complexity that is not yet needed. Astro handles static generation better out of the box and has a simpler mental model for a UI-first build where the data layer does not exist yet.

### Why not Next.js or Nuxt?

Both are React/Vue-based frameworks built for applications with heavy client-side interactivity and server-side rendering. Project Igniter v1 is a static dashboard reading committed YAML files. Bringing in Next.js or Nuxt at this stage is over-engineering. They also have larger build footprints and more complex Cloudflare Pages integration than Astro.

### Why Alpine.js instead of a full JS framework?

The interactivity needed at v1 (dropdowns, expandable sections, tab switching) does not require React, Vue, or Svelte. Alpine.js handles it with HTML attributes and no build step. It keeps the frontend footprint small and readable by someone learning the stack alongside the build.

---

## Consequences

**Positive:**
- Component-based architecture without heavy framework overhead
- Astro's island architecture means JavaScript is only shipped where it is actually needed
- Tailwind integrates directly with the existing AiASH brand CSS variables
- Zero Cloudflare Pages configuration required for Astro deployment
- Clean upgrade path to SvelteKit if the data layer grows complex
- Readable by a non-expert; Astro files look like enhanced HTML

**Negative / Tradeoffs:**
- Astro is not a full application framework; real-time features (live dashboard updates, search) require adding a backend or client-side data fetching
- Alpine.js is not suitable for complex stateful UI; a component framework would be needed at that point
- Team must learn Astro's component model and `.astro` file syntax

---

## Upgrade Path

When dynamic capability is needed, the migration plan is:

1. Add Cloudflare Workers as the API layer (consistent with ADR-0002)
2. Swap Alpine.js interactions for a Svelte or React island where complex state is needed (Astro supports mixed islands natively)
3. Migrate YAML data reads to Worker API calls without changing the page structure
4. If the full app becomes reactive, migrate to SvelteKit while keeping Cloudflare Pages as the host

Nothing about the v1 architecture prevents this migration. It is additive, not destructive.

---

## Related Documents

- [ADR-0001: GitHub-Native Architecture](./ADR-0001-github-native-architecture.md)
- [ADR-0002: Hosting Platform](./ADR-0002-hosting-platform.md)
- [Project Igniter Foundation Document](../../README.md)
