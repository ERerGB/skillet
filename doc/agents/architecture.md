# Architecture — Skillet

## System Overview

Skillet is a creator-facing content terminal that orchestrates
SkillRank (hub discovery), Prism (knowledge graph), and platform SDKs
(publishing) into an end-to-end content workflow accessible via IM agents.

## Module Map

| Module | Responsibility | Dependencies |
|--------|---------------|-------------|
| `src/discovery/` | Hub/Skill discovery via SkillRank API | SkillRank |
| `src/runner/` | Skill loading, caching, execution | Prism (ingest) |
| `src/editor/` | Content organization and arrangement | Prism (recall) |
| `src/publisher/` | Platform-specific publishing adapters | Platform APIs |
| `src/agent/` | IM Agent interface (OpenClaw or standalone) | IM SDKs |

## Data Flow

```
IM Input → Agent → Discovery → Runner → Editor → Publisher → Platform
              │         │          │         │          │
              └── SkillRank ──── Prism ──── Prism ── Platform SDK
```
