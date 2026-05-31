# ADR-0002: Hosting Platform for Project Igniter

**Status:** Accepted  
**Date:** 2026-05-30  
**Author:** Sameera Leola

---

## Context

Project Igniter needs a hosting platform for its dashboard and documentation site. The initial scaffold placed this on GitHub Pages. After the repository was created, the hosting decision was revisited. The choices were:

1. GitHub Pages (static hosting, built into GitHub ecosystem)
2. Cloudflare Pages (static hosting with edge network, Cloudflare Workers integration, D1 database access)
3. A paid hosting provider (Vercel, Netlify, Render)

This decision records why Cloudflare Pages was chosen over the initial GitHub Pages default.

---

## Decision

Project Igniter is hosted on **Cloudflare Pages**.

- **Frontend hosting:** Cloudflare Pages (static site, zero cost on free tier)
- **DNS and SSL:** Cloudflare (already in use for other projects)
- **Build pipeline:** GitHub Actions triggers the build; Cloudflare Pages deploys on push to main
- **Future data layer:** Cloudflare D1 (SQLite at the edge) when dynamic capability is needed
- **Future compute layer:** Cloudflare Workers when server-side logic is needed

---

## Reasoning

### Why not GitHub Pages?

GitHub Pages is static-only with no upgrade path to dynamic compute. Moving from GitHub Pages to a backend later would require migrating the hosting entirely. Cloudflare Pages starts static but has a clean, additive upgrade path to Workers and D1 without changing the hosting provider or domain configuration. Since other projects (DMReply) are already running on Cloudflare Workers + D1, staying inside the Cloudflare ecosystem reduces context switching and keeps infrastructure knowledge consolidated.

### Why not Vercel or Netlify?

Both are strong platforms but introduce a third-party dependency outside the existing GitHub + Cloudflare stack. Vercel is optimized for Next.js; Netlify adds its own function runtime. Neither integrates as cleanly with Cloudflare D1 or Workers. Staying in one ecosystem (GitHub for source control, Cloudflare for compute and hosting) keeps the mental model simple.

### Why not a paid server (VPS, Render, Railway)?

No server is needed at v1 scope. The dashboard is a static site reading YAML data files committed to the repository. Paying for a server before dynamic capability is required adds cost and maintenance overhead with no benefit.

---

## Consequences

**Positive:**
- Zero hosting cost on the Cloudflare free tier
- Edge-delivered performance globally
- Clean upgrade path to Cloudflare Workers + D1 when dynamic features are needed
- DNS, SSL, and hosting all managed in one place
- Consistent with the DMReply infrastructure already in use

**Negative / Tradeoffs:**
- Cloudflare Pages has a slightly more involved initial setup than GitHub Pages
- Build configuration must be maintained in both GitHub Actions and Cloudflare Pages dashboard
- ADR-0001 references GitHub Pages; that document reflects the original decision and is superseded by this one

---

## Upgrade Path

When dynamic capability is needed, the migration plan is:

1. Add a Cloudflare Worker as the API layer
2. Migrate YAML registry data to Cloudflare D1
3. Keep the Cloudflare Pages frontend in place; replace static data reads with Worker API calls
4. GitHub Actions workflow triggers remain unchanged

Nothing about the v1 architecture prevents this migration. It is additive, not destructive.

---

## Related Documents

- [ADR-0001: GitHub-Native Architecture](./ADR-0001-github-native-architecture.md)
- [Project Igniter Foundation Document](../../README.md)
- [Project Registry](../../projects/registry.yaml)
