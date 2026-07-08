# Инвентаризация Концепция.md v1 → v2

Таблица миграции каждого раздела оригинальной концепции.

| § v1 | Название | Действие | Куда в v2 |
|------|----------|----------|-----------|
| 1 | Главная идея | переписать | `00-overview.md`, `01-principles.md` (P1) |
| 2 | Главные уровни (Mission, Discovery, Planner) | переписать | `03-lifecycle.md`, `04-director-sizing.md`; Director как уровень 0 |
| 3 | Компетенции вместо профессий | сохранить + расширить | `06-registry.md`, `01-principles.md` (P4) |
| 4 | Агент — временная единица | переписать | `02-architecture.md` (Worker), `05-workspace.md` (handoff) |
| 5 | Оркестратор не должен знать всё | переписать | `01-principles.md` (P3), `05-workspace.md` (context slice); оркестратор → Director + Planner + RuntimeCoordinator |
| 6 | Архитектура памяти (4 слоя) | сохранить | `05-workspace.md` |
| 7 | Workspace | сохранить + расширить | `05-workspace.md`, `02-architecture.md` |
| 8 | Адаптивная организация (3 размера) | переписать | `04-director-sizing.md` (параметрический sizing, не 3 ветки) |
| 9 | Матрица, Agile, Team Topologies | сохранить как метафоры | `02-architecture.md` (организационные паттерны) |
| 10 | Не привязываться к CrewAI | сохранить | `08-execution-layer.md` |
| 11 | Динамическое создание workflow | сохранить | `03-lifecycle.md`, `08-execution-layer.md` |
| 12 | Контроль качества | переписать | `07-quality-governance.md` (QC по risk tier) |
| 13 | Главный цикл | переписать | `03-lifecycle.md` |
| 14 | Виртуальное предприятие + 3 объекта | переписать | `00-overview.md`, `02-architecture.md` (10 объектов) |
| — | Director / Sizing | новое | `04-director-sizing.md` |
| — | RuntimeCoordinator | новое | `02-architecture.md`, `08-execution-layer.md` |
| — | Handoff protocol | новое | `05-workspace.md`, `01-principles.md` (P8) |
| — | Dogfooding | новое | `09-dogfooding.md` |
| — | ModelProfile, TaskProfile | новое | `06-registry.md`, `04-director-sizing.md` |
| — | Human as Registry resource | новое | `06-registry.md`, `07-quality-governance.md` |

## Удалено / не переносится буквально

- Жёсткое деление «маленькая / средняя / большая задача» как единственная модель sizing.
- Термин «агент» как канонический (заменён на Worker).
- Единый «оркестратор» как один объект.

## Сохранено по сути

- Идея «организация, создающая команды».
- Workspace как центр.
- Компетенции вместо должностей.
- Четыре слоя памяти.
- Динамический workflow.
- Отделение ядра от CrewAI/LangGraph.
