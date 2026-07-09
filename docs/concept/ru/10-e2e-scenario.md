# Сквозной сценарий: спецификация Workspace

Единая задача, проходящая через все разделы концепции v2 без «магических шагов».

**Mission:** Написать спецификацию Workspace на основе [Концепция.md](../../../Концепция.md) v1.

---

## 1. Mission ([02-architecture.md](02-architecture.md))

```yaml
id: mission-001
goal: "Написать спецификацию Workspace на основе Концепция.md v1"
success_criteria:
  - "ADR согласован и покрывает 4 слоя памяти"
  - "Описан context slice с примером"
  - "Описан handoff protocol"
constraints:
  max_duration: "2 weeks"
  budget_tokens: 500000
risk_tier: medium
workspace_id: ws-001
```

---

## 2. Director + SizingDecision ([04-director-sizing.md](04-director-sizing.md))

**Task profile:**

```yaml
work_units: 3
competencies: [system_design, api_design, technical_review]
reasoning_need: 0.7
risk: medium
context_estimate: 40000
parallelizable: false
```

**SizingDecision:**

```yaml
executor_count: 2
parallelism: 1
planner_depth: 1
discovery_required: false
qc_depth: critic
model_assignments:
  director: model-sonnet
  worker_writer: model-sonnet
  worker_critic: model-haiku
confidence: 0.82
rationale: "Design + review; medium risk; не нужна полная организация"
```

**Принципы:** P0 (минимальная орг), P9 (confidence достаточен — без strong review).

---

## 3. Registry ([06-registry.md](06-registry.md))

| ID | Тип | Роль в сценарии |
|----|-----|-----------------|
| system_design | competency | Writer |
| api_design | competency | Writer |
| technical_review | competency | Critic |
| model-sonnet | model | Writer, Director |
| model-haiku | model | Critic |

---

## 4. Planner + Task graph ([03-lifecycle.md](03-lifecycle.md))

```yaml
tasks:
  - id: task-draft-adr
    title: "Черновик ADR Workspace"
    competency: system_design
    depends_on: []

  - id: task-review-adr
    title: "Review ADR"
    competency: technical_review
    depends_on: [task-draft-adr]

  - id: task-finalize
    title: "Финализация ADR"
    competency: system_design
    depends_on: [task-review-adr]
```

Task graph записывается в `Workspace.task_graph`.

---

## 5. Workspace + Slices ([05-workspace.md](05-workspace.md))

**Writer slice:**

```yaml
worker_id: worker-writer-001
task_id: task-draft-adr
includes:
  - mission.goal
  - mission.success_criteria
  - artifacts:Концепция.md#6-7
  - competency_memory:system_design
max_tokens: 30000
```

**Critic slice:**

```yaml
worker_id: worker-critic-001
task_id: task-review-adr
includes:
  - mission.success_criteria
  - artifacts:ADR-draft
excludes:
  - full_task_graph
```

---

## 6. RuntimeCoordinator + Execution ([08-execution-layer.md](08-execution-layer.md))

| Шаг | Действие |
|-----|----------|
| 1 | task-draft-adr ready → create worker-writer-001 |
| 2 | ExecutionEngine.invoke(writer) → draft ADR |
| 3 | QC self-check → handoff writer |
| 4 | task-review-adr ready → create worker-critic-001 |
| 5 | ExecutionEngine.invoke(critic) → review |
| 6 | QC critic approve → handoff critic |
| 7 | task-finalize → writer или auto-merge |
| 8 | Success check |

---

## 7. Quality ([07-quality-governance.md](07-quality-governance.md))

- risk_tier: medium → qc_depth: critic
- Guardian: budget_tokens не превышен
- Human gate: не требуется (medium < high)

---

## 8. Handoff ([05-workspace.md](05-workspace.md))

**Writer handoff:**

```yaml
handoff_id: handoff-001
worker_id: worker-writer-001
records:
  - type: artifact
    path: docs/decisions/ADR-001-workspace-schema.md
  - type: decision
    id: DEC-001
    title: "Task graph в Workspace"
    rationale: "Единый источник правды"
status: completed
```

**Critic handoff:**

```yaml
handoff_id: handoff-002
worker_id: worker-critic-001
records:
  - type: lesson
    text: "Добавить явные поля slice policy в ADR"
  - type: decision
    id: DEC-002
    title: "Approve draft"
    rationale: "Покрыты 4 слоя памяти"
status: completed
qc_result:
  approved: true
```

---

## 9. Success check + Complete

| Критерий | Статус |
|----------|--------|
| ADR согласован | ✓ |
| 4 слоя памяти | ✓ |
| Пример context slice | ✓ |

Mission → **completed**. Workspace содержит финальный ADR, decisions, lessons.

---

## 10. Dogfooding ([09-dogfooding.md](09-dogfooding.md))

**Phase 1** этого сценария: выполняется вручную (человек = Director + RuntimeCoordinator).

**Lesson (пример):**

```yaml
text: "executor_count=2 достаточно; полная организация не нужна"
hypothesis_H1: confirmed
```

---

## Проверка принципов P0–P9

| Принцип | В сценарии |
|---------|------------|
| P0 | 2 Worker'а, не полная org |
| P1 | Worker'ы временные |
| P2 | Всё в Workspace |
| P3 | Slices ограничены |
| P4 | competency_ids, не роли |
| P5 | Task graph под mission |
| P6 | При reject → retry finalize |
| P7 | critic только (medium) |
| P8 | Два handoff |
| P9 | confidence 0.82 — без escalation |

---

## Что бы сломалось (негативные ветки)

| Изменение | Последствие |
|-----------|-------------|
| Director: executor_count=10 | P0 нарушен, лишняя стоимость |
| Нет handoff | P8, потеря ADR между сессиями |
| Critic получает full Workspace | P3, перегруз контекста |
| planner_depth=0 для 3 задач | Нет DAG, дублирование |
| risk critical без human | P7, P9 нарушены |
