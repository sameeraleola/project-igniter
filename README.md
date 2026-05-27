# Project Igniter

> A structured ignition and scaffolding system that transforms dormant project ideas into active, documented, and repository-ready builds through a GitHub-native workflow.

---

## What This Is

Project Igniter is both a tool and a philosophy. Good builders accumulate ideas faster than they can execute them. Most systems treat that backlog as a failure state. Project Igniter treats it as fuel.

A dormant project is not a dead project. It is an unlit one.

---

## Core Components

| Component | Purpose |
|---|---|
| **Project Registry** | YAML-based record of every project in any state |
| **Dashboard** | Cloudflare Pages status view with Ignite actions |
| **Ignition Workflow** | GitHub Actions workflow that scaffolds a project from dormant to active |
| **Scaffold Output** | Baseline artifacts every ignited project receives |

---

## Architecture

| Layer | Technology |
|---|---|
| Frontend | Cloudflare Pages |
| Landing Pages | ClickFunnels (mounted via Cloudflare) |
| Authentication | Cloudflare Access (Zero Trust) |
| Data Store | YAML registry committed to this repository |
| Workflow Engine | GitHub Actions |
| Domain | sameeraleola.dev/project-igniter/ |

Full architectural reasoning is documented in [ADR-0001](docs/adr/ADR-0001-github-native-architecture.md).

---

## Repository Structure

```
project-igniter/
  projects/
    registry.yaml          # The dormant project registry
  docs/
    adr/
      ADR-0001-github-native-architecture.md
  .github/
    workflows/
      ignite.yml           # Ignition workflow (in progress)
  README.md
```

---

## Build Log

Every session is documented in the public build log. It captures decisions made, artifacts built, and what comes next.

[Project Igniter — Build Log](https://gist.github.com/sameeraleola/1828a42806a0143bfb5cc1fab029c4fd)

---

## Status

Active build — v0.1 UI Definition in progress. Target: June 3, 2026.

See [projects/registry.yaml](projects/registry.yaml) for current project states.

---

## Built By

[Sameera Leola](https://github.com/sameeraleola) using the [MarketSecrets.ai](https://www.getaisecrets.com/) platform.
