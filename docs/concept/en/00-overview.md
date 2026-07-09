# MorphEnterprise — concept overview v2

An architecture for **autonomous agent organizations**: not a pre-built swarm of agents, but an organization that assembles **minimally sufficient teams** for each mission.

Previous version: [Концепция.md](../../../Концепция.md) (v1 archive, Russian).

**Language:** Canonical specification is **English** (`docs/concept/en/`). Detailed chapters 01–10 are currently **Russian only** in [`../ru/`](../ru/); translations are incremental. Feedback welcome via [GitHub Issues](https://github.com/devmrbouh-hub/MorphEnterprise/issues).

---

## v1 → v2 evolution

| Aspect | v1 | v2 |
|--------|----|----|
| Entry | Mission → Discovery → Planner | **Director** (triage/sizing) at level 0 |
| Scale | 3 organization sizes | **Parametric sizing** (volume × capability gap) |
| Models | General mention | **ModelProfile** in Registry |
| Orchestration | Single layer | **Director + Planner + RuntimeCoordinator** |
| Worker completion | Not described | **Mandatory Handoff** |
| QC | Always full | **By risk tier** |
| Core objects | 3 | **10** + DiscoveryPhase as a lifecycle phase |

Full migration table: [../ru/migration-inventory.md](../ru/migration-inventory.md) (RU).

---

## Pitch

MorphEnterprise is a **coordination protocol** for executors (LLMs, tools, humans) around a shared **Workspace**. The “virtual enterprise” metaphor guides design; the system does not literally simulate a company.

The system:

1. Receives a mission.
2. **Director** assesses volume, complexity, risk, and model capabilities.
3. Produces a **SizingDecision** — minimally sufficient configuration.
4. When needed: Discovery → Planner → task graph.
5. **RuntimeCoordinator** runs execution through **Workers**.
6. **QualityGovernance** by risk tier.
7. **Handoff** into Workspace; on deadlock — resize or escalation.

---

## How we differ

| Approach | Level | MorphEnterprise |
|----------|-------|-----------------|
| **CrewAI / LangGraph** | Agent execution, graphs | Execution layer (ExecutionEngine), not the core |
| **AutoGPT / swarms** | One agent + tools in a loop | Organization with sizing; not a swarm by default |
| **Fixed roles** | Architect, coder, tester | Competencies + temporary Workers |
| **One large prompt** | Everything in one context | Workspace + context slices |

---

## Ten core objects

| # | Object | One-liner |
|---|--------|-----------|
| 1 | **Mission** | Goal with success criteria, constraints, budget, risk tier |
| 2 | **Director** | Triage and sizing — how much organization is needed |
| 3 | **SizingDecision** | Parametric output of Director (executors, depth, QC, models) |
| 4 | **Workspace** | Single source of truth; memory layers and task graph |
| 5 | **CompetencyRegistry** | Catalog of competencies, models, tools, humans |
| 6 | **Planner** | Decomposition into task graph (when planner_depth > 0) |
| 7 | **Worker** | Temporary execution unit; not “agent” |
| 8 | **RuntimeCoordinator** | Runs task graph during execution; resize, escalation |
| 9 | **QualityGovernance** | QC, budget, safety by risk tier |
| 10 | **ExecutionEngine** | Adapter to concrete runtime (CrewAI, LangGraph, Cursor, …) |

DiscoveryPhase is a **lifecycle phase**, not a separate core object. See [glossary.md](glossary.md).

---

## Scope

### In scope (concept v2)

- Normative description of objects, principles, lifecycle.
- Protocols for sizing, memory, handoff, QC.
- Dogfooding as validation method.
- Abstract ExecutionEngine (adapter).

### Out of scope (concept v2)

- Concrete stack (Python, DB, framework).
- Full MVP implementation (next step — ADR decomposition).
- Production UI, deploy, monitoring.

### Deferred until MVP

- Automatic Director on all task types.
- Fully autonomous loop without human gates.
- Concrete CrewAI/LangGraph integration.

---

## Document map

| Document | Language | Content |
|----------|----------|---------|
| [en/00-overview.md](00-overview.md) | EN | This file (canonical entry) |
| [en/glossary.md](glossary.md) | EN | Terms (canonical) |
| [../ru/01-principles.md](../ru/01-principles.md) | RU | P0–P9 principles |
| [../ru/02-architecture.md](../ru/02-architecture.md) | RU | 10 objects, diagrams |
| [../ru/03-lifecycle.md](../ru/03-lifecycle.md) | RU | Main cycle, escalation |
| [../ru/04-director-sizing.md](../ru/04-director-sizing.md) | RU | Director, capability gap |
| [../ru/05-workspace.md](../ru/05-workspace.md) | RU | Memory, slices, handoff |
| [../ru/06-registry.md](../ru/06-registry.md) | RU | Competencies, models |
| [../ru/07-quality-governance.md](../ru/07-quality-governance.md) | RU | Risk tier, QC |
| [../ru/08-execution-layer.md](../ru/08-execution-layer.md) | RU | RuntimeCoordinator |
| [../ru/09-dogfooding.md](../ru/09-dogfooding.md) | RU | Bootstrap, phases |
| [../ru/10-e2e-scenario.md](../ru/10-e2e-scenario.md) | RU | End-to-end scenario |
| [../schemas/](../schemas/) | neutral | YAML contracts |

---

## End-to-end example

Task: **“Write Workspace specification”** — walks through all sections. See [../ru/10-e2e-scenario.md](../ru/10-e2e-scenario.md) (RU).
