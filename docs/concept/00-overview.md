# MorphEnterprise — обзор концепции v2

Архитектурная концепция **автономной агентной организации**: не рой заранее созданных агентов, а **организация, создающая команды минимально достаточного размера** под каждую mission.

Предыдущая версия: [Концепция.md](../../Концепция.md) (v1, архив).

---

## Эволюция v1 → v2

| Аспект | v1 | v2 |
|--------|----|----|
| Вход | Mission → Discovery → Planner | **Director** (triage/sizing) как уровень 0 |
| Масштаб | 3 размера организации | **Параметрический sizing** (объём × capability gap) |
| Модели | Общее упоминание | **ModelProfile** в Registry |
| Оркестратор | Один слой | **Director + Planner + RuntimeCoordinator** |
| Завершение Worker | Не описано | **Обязательный Handoff** |
| QC | Всегда полный | **По risk tier** |
| Объектов ядра | 3 | **10** + DiscoveryPhase как фаза |

Полная таблица миграции: [migration-inventory.md](migration-inventory.md).

---

## Pitch

MorphEnterprise — **протокол координации** исполнителей (LLM, инструменты, люди) вокруг общего **Workspace**. Метафора «виртуального предприятия» полезна для дизайна, но система не симулирует компанию буквально.

Система:

1. Получает mission.
2. **Director** оценивает объём, сложность, risk и способности моделей.
3. Выдаёт **SizingDecision** — минимально достаточную конфигурацию.
4. При необходимости: Discovery → Planner → task graph.
5. **RuntimeCoordinator** ведёт исполнение через **Worker**'ов.
6. **QualityGovernance** по risk tier.
7. **Handoff** в Workspace; при тупике — resize или escalation.

---

## Границы системы

### В scope концепции v2

- Нормативное описание объектов, принципов, lifecycle.
- Протоколы sizing, памяти, handoff, QC.
- Dogfooding как метод валидации.
- Абстрактный ExecutionEngine (адаптер).

### Вне scope концепции v2

- Конкретный стек (Python, БД, фреймворк).
- GitHub, лицензии, сообщество (отдельный трек).
- Полная реализация MVP (следующий проход — декомпозиция в ADR).
- UI, деплой, мониторинг production.

### Отложено до MVP

- Автоматический Director на всех типах задач.
- Полностью автономный цикл без human gate.
- Интеграция с конкретным CrewAI/LangGraph.

---

## Отличие от других подходов

| Подход | Уровень | MorphEnterprise |
|--------|---------|-----------------|
| **CrewAI / LangGraph** | Исполнение агентов, графы | Исполнительный слой (ExecutionEngine), не ядро |
| **AutoGPT / рой** | Один агент + инструменты в цикле | Организация с sizing; не рой по умолчанию |
| **Фиксированные роли** | Архитектор, кодер, тестер | Компетенции + временные Worker'ы |
| **Один большой промпт** | Всё в одном контексте | Workspace + context slice |

---

## Карта документов v2

| Документ | Содержание |
|----------|------------|
| [01-principles.md](01-principles.md) | P0–P9, инварианты |
| [02-architecture.md](02-architecture.md) | 10 объектов, диаграммы, паттерны |
| [03-lifecycle.md](03-lifecycle.md) | Главный цикл, escalation, resize |
| [04-director-sizing.md](04-director-sizing.md) | Director, capability gap, алгоритм |
| [05-workspace.md](05-workspace.md) | Память, slices, handoff |
| [06-registry.md](06-registry.md) | Компетенции, ModelProfile, ресурсы |
| [07-quality-governance.md](07-quality-governance.md) | Risk tier, QC, human gates |
| [08-execution-layer.md](08-execution-layer.md) | RuntimeCoordinator, ExecutionEngine |
| [09-dogfooding.md](09-dogfooding.md) | Bootstrap, фазы, чеклист |
| [10-e2e-scenario.md](10-e2e-scenario.md) | Сквозной сценарий |
| [glossary.md](glossary.md) | Термины и карта v1→v2 |
| [schemas/](schemas/) | YAML-контракты объектов |
| [cross-review.md](cross-review.md) | Проверка готовности к декомпозиции |

---

## Сквозной пример

Задача: **«Написать спецификацию Workspace»**. Проходит через все разделы — см. [10-e2e-scenario.md](10-e2e-scenario.md).
