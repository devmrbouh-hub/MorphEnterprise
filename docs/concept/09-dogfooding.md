# Dogfooding

Метод валидации концепции: **строить MorphEnterprise с помощью MorphEnterprise**.

---

## Bootstrap paradox

Полная самореференция с нуля невозможна. Нужен **Phase 0 — ручное ядро**:

| Объект v2 | Phase 0 |
|-----------|---------|
| Workspace | `docs/` + markdown + git |
| Registry | `docs/competencies.md` |
| Director | Человек |
| Planner | Человек + LLM в Cursor |
| RuntimeCoordinator | Человек |
| Workers | Cursor Agent / ручные сессии |
| QC | Человек смотрит результат |
| ExecutionEngine | Cursor |

Система эволюционирует из костыля, не рождается из себя.

---

## Правило фазы

Каждая фаза = **гипотеза + критерий успеха + lesson в Workspace**.

```yaml
hypothesis: "Структурированный Workspace лучше одного Концепция.md"
success_criteria:
  - "Новый участник понимает проект за 15 минут"
lesson_location: docs/concept/lessons.md
```

---

## Фазы 0–5 (кратко)

| Фаза | Миссия | Гипотеза | Критерий |
|------|--------|----------|----------|
| **0** | Оформить docs/concept v2 | Workspace в markdown работает | 15 мин onboarding |
| **1** | Спецификация Workspace (ADR) | Компетенции лучше одного промпта | ADR ≥2 ролями |
| **2** | Workspace как код | Код = markdown model | CRUD mission/decision/slice |
| **3** | Полуавтоматический Planner | LLM строит task graph | 70% планов с малыми правками |
| **4** | Quality layer | Critic ловит 50% до человека | Меньше итераций |
| **5** | Замкнутый цикл | Mission без ручного планирования | Зелёные критерии, handoff |

Детальный ROADMAP — следующий проход (из этого документа).

---

## Чеклист «так ли радужно»

| # | Вопрос | Если нет |
|---|--------|----------|
| 1 | Новая сессия понимает проект за 15 мин? | Workspace не работает |
| 2 | Worker'ы не дублируют работу? | Planner / task graph слабые |
| 3 | Решения не теряются между сессиями? | Нет handoff (P8) |
| 4 | Простая задача не требует 10 Worker'ов? | Director переусложняет |
| 5 | Сложная задача не проходит без QC? | Quality layer слабый |
| 6 | Стоимость предсказуема? | Нет guardian / бюджета |
| 7 | Человек только где нужно? | Нет risk tier |
| 8 | Можно заменить ExecutionEngine? | Planner привязан к исполнителю |

---

## Методология (ранний проход)

1. Взять реальную задачу по MorphEnterprise.
2. Пройти lifecycle вручную по docs/concept.
3. Заполнить SizingDecision, task graph, handoff в markdown.
4. Зафиксировать lesson.
5. Сравнить с принципами P0–P9.

---

## Примеры (поздний проход)

### Phase 0 — написание концепции v2

- **Mission:** docs/concept v2 готов к декомпозиции.
- **Director (человек):** executor_count=1 для каждого §, planner_depth=0 на черновики.
- **Lesson:** inventory v1 первым спас §8–9.

### Phase 1 — спецификация Workspace

См. [10-e2e-scenario.md](10-e2e-scenario.md).

---

## Ожидаемые провалы (нормально)

- Director переоценивает сложность → дорого.
- Handoff теряет nuance → дополнить Lesson.
- Planner создаёт лишних Worker'ов → калибровка capability gap.
- Resize thrashing → ужесточить лимит реорганизаций.

Каждый провал → lesson → правка концепции.
