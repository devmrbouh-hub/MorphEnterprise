# Workspace

Главный объект системы (P2). Не просто память — **единый источник правды** о mission.

---

## Содержимое Workspace

| Поле | Описание |
|------|----------|
| mission | Текущая mission и sub-missions |
| requirements | Требования, в т.ч. из Discovery |
| decisions | ADR, выборы, обоснования |
| artifacts | Документы, схемы, код |
| task_graph | DAG задач (часть Workspace, не отдельный объект) |
| current_state | Статус фаз lifecycle |
| handoff_records | Записи завершённых Worker'ов |
| knowledge_links | Ссылки на внешний Knowledge |
| competencies_active | Компетенции, задействованные в mission |

---

## Четыре слоя памяти

Сохранено из v1 §6. Слои — **логические**, физически могут жить в одном хранилище с тегами.

### 1. Knowledge

Общие знания: документация, стандарты, исследования, методики. Разделяется между mission.

### 2. Competency Memory

Память компетенции: лучшие практики, прошлые решения, ошибки, шаблоны. Привязана к competency_id в Registry.

### 3. Project Memory

Память mission: почему приняли решение, какие проблемы возникли. = decisions + lessons в Workspace.

### 4. Working Context

Текущая работа: что делаем сейчас, что нужно активному Worker'у. Эфемерно; при handoff важное переносится в Project Memory.

---

## Context slice

Worker не получает весь Workspace. **Context slice** — адресный срез:

```yaml
worker_id: worker-writer-001
mission_id: mission-001
task_id: task-draft-adr
competency_ids: [system_design, api_design]
includes:
  - mission.goal
  - mission.success_criteria
  - decisions: relevant_only
  - artifacts: [Концепция.md sections 6-7]
  - competency_memory: [system_design, api_design]
excludes:
  - full_task_graph
  - other_workers_handoffs
max_tokens: 30000
```

### Политика доступа

| Кто | Может |
|-----|--------|
| Worker | Читать slice по своей competency + task |
| Planner | Читать summary + task graph + requirements |
| Director | Читать mission summary + risk + state (не детали артефактов) |
| RuntimeCoordinator | Читать task graph + state; **не расширяет** slice Worker'а без пересмотра SizingDecision |
| Critic | Slice исполнителя + output + success_criteria |

---

## Handoff protocol (P8)

Handoff — **операция записи** в Workspace, не отдельный сервис.

Обязательные типы записей:

| Тип | Содержание |
|-----|------------|
| **Decision** | Что решили, альтернативы, обоснование |
| **Lesson** | Что узнали, что не сработало |
| **Artifact** | Ссылка или тело результата |

Схема: [schemas/handoff-record.yaml](schemas/handoff-record.yaml).

```yaml
handoff_id: handoff-001
worker_id: worker-writer-001
task_id: task-draft-adr
timestamp: "2026-07-09T00:00:00Z"
records:
  - type: artifact
    path: docs/decisions/ADR-001-workspace-schema.md
    summary: "Черновик спецификации Workspace"
  - type: decision
    id: DEC-001
    title: "Task graph хранится в Workspace"
    rationale: "Единый источник правды"
  - type: lesson
    text: "Нужен явный slice policy до написания ADR"
status: completed
```

Без handoff Worker не считается завершённым.

---

## Минимальный Workspace

### executor_count = 1

- mission, current_state, working_context
- handoff_records по завершении
- Без полного task graph (опционально один task)

### Полная организация

- Все поля
- Полный task graph
- discovery outputs в requirements
- Множественные handoff_records

---

## Связь Workspace ↔ Mission ↔ Task graph

```
Mission 1──1 Workspace
Workspace 1──1 TaskGraph (поле task_graph)
TaskGraph *──* Tasks
Task 1──* Worker (последовательно во времени)
```

---

## Сквозной пример: спецификация Workspace

1. **До работы:** Workspace содержит mission, ссылку на Концепция.md v1.
2. **Planner** пишет task_graph: draft → review → finalize.
3. **Writer** получает slice: §6–7 концепции, success_criteria.
4. **Writer handoff:** artifact ADR draft + decision о слоях памяти.
5. **Critic** получает slice: draft ADR + success_criteria.
6. **Critic handoff:** lesson + approve/reject.
7. **Финал:** decisions и artifact в Workspace; mission → completed.
