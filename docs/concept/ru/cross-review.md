# Cross-review: готовность концепции v2 к декомпозиции

Дата проверки: 2026-07-09

---

## Критерии готовности

| # | Критерий | Статус | Примечание |
|---|----------|--------|------------|
| 1 | Полнота: 9 разделов + glossary + 8 schemas | ✓ | 00–10, glossary, 8 yaml |
| 2 | Сквозной сценарий без магических шагов | ✓ | [10-e2e-scenario.md](10-e2e-scenario.md) |
| 3 | 10 принципов с тестами dogfooding | ✓ | [01-principles.md](01-principles.md) |
| 4 | 10 объектов: поля, связи, пример YAML | ✓ | architecture + schemas |
| 5 | Границы scope явны | ✓ | [00-overview.md](00-overview.md) |
| 6 | Нет solo/small/full как веток | ✓ | Параметры SizingDecision |
| 7 | Таблица миграции v1→v2, включая §8–9 | ✓ | [migration-inventory.md](migration-inventory.md) |
| 8 | Терминология единая (Worker) | ✓ | [glossary.md](glossary.md) |

---

## Чеклист самопроверки плана

| Проверка | Статус |
|----------|--------|
| Нет противоречий 04-director-sizing ↔ 08-execution | ✓ |
| Director / Planner / RuntimeCoordinator разделены | ✓ |
| P0–P9 отражены в lifecycle | ✓ |
| У 10 объектов вход/выход | ✓ |
| Bootstrap Phase 0 не требует системы | ✓ |
| Примеры: low volume + high volume | ✓ (опечатка + 50 тестов + продукт) |
| v1 §8–9 сохранены как паттерны | ✓ |
| risk_tier floor/escalate | ✓ |
| RuntimeCoordinator в architecture + execution | ✓ |
| Handoff — операция Workspace, не сервис | ✓ |
| Discovery — фаза, не объект | ✓ |
| Task graph — часть Workspace | ✓ |
| Bootstrap Director описан | ✓ |

---

## Декомпозиция (следующий проход)

| Источник v2 | Артефакт |
|-------------|----------|
| 05-workspace.md + schemas | ADR-001: Workspace spec |
| 06-registry.md + schemas | ADR-002: Registry spec |
| 04-director-sizing.md + schemas | ADR-003: Director/Sizing spec |
| 03-lifecycle.md | ADR-004: Lifecycle state machine |
| 08-execution-layer.md | ADR-005: Runtime coordination spec |
| 09-dogfooding.md | ROADMAP.md |
| 10-e2e-scenario.md | E2E walkthrough |
| 01-principles.md | Acceptance criteria MVP |

---

## Открытые вопросы (не блокируют декомпозицию)

1. Конкретный формат хранения Workspace (файлы vs БД) — вне scope v2.
2. Алгоритм confidence калибровки Director — уточнить при реализации.
3. Таймаут human gate — политика mission, детализировать в ADR.

---

## Вердикт

**Концепция v2 готова к декомпозиции.**

Рекомендуемый первый ADR: **Workspace spec** (ADR-001), т.к. от него зависят все остальные компоненты.
