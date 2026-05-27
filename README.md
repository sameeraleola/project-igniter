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
| **Dashboard** | GitHub Pages status view with Ignite actions |
| **Ignition Workflow** | GitHub Actions workflow that scaffolds a project from dormant to active |
| **Scaffold Output** | Baseline artifacts every ignited project receives |

---

## Architecture

| Layer | Technology |
|---|---|
| Frontend | GitHub Pages (static site) |
| Data Store | YAML registry committed to this repository |
| Workflow Engine | GitHub Actions |
| DNS and SSL | Cloudflare |

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

## Status

Active build. See [projects/registry.yaml](projects/registry.yaml) for current project states.

---

## Built By

[Sameera Leola](https://github.com/sameeraleola) — part of the Filogico ecosystem.