# Глоссарий MorphEnterprise v2

Канонические термины. Один термин — одно значение.

---

## Карта терминов v1 → v2

| Термин v1 | Термин v2 | Примечание |
|-----------|-----------|------------|
| Агент | **Worker** | Временная рабочая единица |
| Executor | **Worker** | Единый термин, не использовать «executor» в документации |
| Оркестратор (управление) | **Director + Planner + RuntimeCoordinator** | Три разделённые роли |
| Организатор (§10) | **RuntimeCoordinator + ExecutionEngine** | Runtime + адаптер |
| Планировщик | **Planner** | Только декомпозиция, при planner_depth > 0 |
| — | **Director** | Новое: triage и sizing (уровень 0) |
| — | **SizingDecision** | Новое: выход Director |
| — | **RuntimeCoordinator** | Новое: ведение task graph во время исполнения |
| Discovery | **DiscoveryPhase** | Фаза lifecycle, не объект |
| Память агента | **Workspace** (слои) + **context slice** | Память организационная |

---

## Термины

### Mission
Цель работы с success_criteria, constraints, budget и risk_tier (floor). Может иметь sub-missions. Один Workspace на mission.

### Director
Роль triage и sizing. Определяет минимально достаточную организацию. Не исполняет задачи. Может использовать слабую или сильную модель из Registry. Эскалирует себя при низком confidence.

### SizingDecision
Структурированный выход Director: executor_count, parallelism, planner_depth, discovery_required, qc_depth, model_assignments, human_gates, estimated_cost, confidence, escalation_policy, rationale.

### Planner
Декомпозирует работу в task graph и назначения Worker'ам. Активен только при planner_depth > 0. Не знает деталей исполнительного движка (CrewAI и т.д.).

### RuntimeCoordinator
Ведёт task graph во время исполнения: запуск Worker'ов, мониторинг, resize, триггеры escalation. Между Planner и ExecutionEngine.

### Worker
Временная рабочая единица с целью, компетенциями, моделью, context slice и критериями успеха. После handoff исчезает.

### Workspace
Центральное хранилище: mission, requirements, decisions, artifacts, task graph, current state, handoff records, knowledge links.

### Context slice
Адресный срез Workspace для конкретного Worker'а. Авторизуется политикой доступа (компетенция + задача). RuntimeCoordinator не расширяет slice без пересмотра SizingDecision.

### Handoff
Операция записи в Workspace по завершении Worker'а: Decision, Lesson, Artifact (см. handoff-record).

### CompetencyRegistry
Каталог компетенций, ModelProfile, Tool и Human resource. Все роли берут модели и инструменты отсюда.

### ModelProfile
Профиль модели: strengths, weaknesses, context_window, cost, relative_reasoning, domains.

### TaskProfile
Профиль задачи: work_units, competencies, reasoning_need, risk, context_estimate, parallelizable.

### Capability gap
Разрыв между требованиями задачи и способностями одной модели по осям: reasoning, context, throughput, competencies, risk.

### DiscoveryPhase
Опциональная фаза исследования до планирования. Включается через discovery_required в SizingDecision.

### QualityGovernance
Контур QC: критики, стражи, арбитры, human gates. Масштабируется по risk_tier.

### ExecutionEngine
Тонкий адаптер к CrewAI, LangGraph или другому исполнителю. Не содержит бизнес-логики организации.

### Risk tier
Уровень риска: low | medium | high | critical. Mission задаёт floor; Director может только повысить.

### Dogfooding
Метод валидации: строить MorphEnterprise с помощью протоколов самой MorphEnterprise.

---

## Устаревшие термины (не использовать в v2)

- «Рой агентов»
- «Агент» (вместо Worker)
- «Solo / small team / full org» как режимы (заменить параметрами SizingDecision)
- «Оркестратор» без уточнения (Director / Planner / RuntimeCoordinator)
