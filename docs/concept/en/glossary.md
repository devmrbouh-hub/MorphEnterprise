# MorphEnterprise v2 glossary

Canonical terms. One term — one meaning.

Russian translation: [../ru/glossary.md](../ru/glossary.md).

---

## Do / Don't

| Use | Don't use |
|-----|-----------|
| Worker | agent, executor |
| Director, Planner, RuntimeCoordinator | orchestrator (without qualification) |
| SizingDecision, Mission, Workspace | solo / small / full org |

---

## Terms

### Mission
Work goal with success_criteria, constraints, budget, and risk_tier (floor). May have sub-missions. One Workspace per mission.

### Director
Triage and sizing role. Determines minimally sufficient organization. Does not execute tasks. May escalate when confidence is low.

### SizingDecision
Structured Director output: executor_count, parallelism, planner_depth, discovery_required, qc_depth, model_assignments, human_gates, estimated_cost, confidence, escalation_policy, rationale.

### Planner
Decomposes work into a task graph and Worker assignments. Active only when planner_depth > 0. Does not depend on a specific execution engine.

### RuntimeCoordinator
Runs the task graph during execution: start Workers, monitor, resize, escalation triggers. Between Planner and ExecutionEngine.

### Worker
Temporary work unit. Lifecycle: created → execution → QC → handoff → destroyed.

### Workspace
Organizational memory and single source of truth: mission, requirements, decisions, artifacts, task_graph, handoff_records, knowledge_links. Context **slices** are read views, not full context.

### context slice
Bounded view of Workspace for one Worker or role (paths, token budget, task scope).

### Handoff
Mandatory structured record when a Worker completes: artifacts, status, rationale. Written to Workspace.

### QualityGovernance
Quality control, budget, safety — depth depends on risk tier and SizingDecision.qc_depth.

### CompetencyRegistry
Catalog of competencies, ModelProfiles, tools, humans. Matching task_profile × model_profile.

### ExecutionEngine
Adapter to concrete runtime (Cursor, CrewAI, LangGraph, shell, human). Not a core domain object; pluggable.

### DiscoveryPhase
Lifecycle phase for exploring unknown scope before planning. Not a standalone runtime object.

### DiscoveryPhase vs Discovery
Use **DiscoveryPhase** (phase), not “Discovery” as an object name.
