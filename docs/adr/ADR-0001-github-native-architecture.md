# ADR-0001: GitHub-Native Architecture for Project Igniter

**Status:** Accepted  
**Date:** 2026-05-27  
**Author:** Sameera Leola

---

## Context

Project Igniter needs a home. The choices are:

1. A hosted web application with a custom backend
2. An existing SaaS project management tool
3. A fully GitHub-native stack: GitHub Pages + GitHub Actions + committed YAML

This decision records why option 3 was chosen.

---

## Decision

Project Igniter is built entirely on GitHub infrastructure.

- **Frontend:** GitHub Pages (static site, zero server cost)
- **Data Store:** YAML registry files committed directly to this repository
- **Workflow Engine:** GitHub Actions (triggers ignition, updates registry, generates scaffold artifacts)
- **DNS and SSL:** Cloudflare

---

## Reasoning

### Why not a custom backend server right now?

The Filogico Synthetic Data Tool already has a FastAPI backend in its future roadmap. Building a second backend for Project Igniter before the first one exists means maintaining two servers before shipping either project. GitHub Actions is sufficient as a workflow engine for v1 scope.

### Why not an existing SaaS tool (Notion, Linear, Jira)?

Project Igniter is a developer operations tool built for builders who work in and around GitHub. Keeping the tool inside GitHub keeps the credibility signal aligned and eliminates a third-party dependency. Every artifact produced by Project Igniter is version-controlled automatically.

### Why not ClickFunnels or a marketing platform?

ClickFunnels is purpose-built for converting visitors into buyers. Project Igniter is a developer workflow tool. Using a conversion platform as a developer tool sends the wrong signal and lacks the programmable workflow behavior the ignition process requires.

---

## Consequences

**Positive:**
- Zero infrastructure cost for v1
- Everything version-controlled by default
- GitHub Actions provides enough workflow power for ignition automation
- Upgrade path to FastAPI backend is clean when needed

**Negative / Tradeoffs:**
- GitHub Pages is static; dynamic features (real-time dashboard updates, search) require workarounds or the future FastAPI upgrade
- YAML as a data store has limits at scale; migration to a real database will be needed before Filogico's project count grows large

---

## Upgrade Path

When dynamic capability is needed, the migration plan is:

1. Add a FastAPI backend (reusing patterns from the Synthetic Data Tool)
2. Migrate YAML registry to PostgreSQL
3. Keep the GitHub Pages frontend in place; replace static data calls with API calls
4. GitHub Actions workflow triggers remain unchanged

Nothing about the v1 architecture prevents this migration. It is additive, not destructive.

---

## Related Documents

- [Project Igniter Foundation Document](../../README.md)
- [Project Registry](../../projects/registry.yaml)
