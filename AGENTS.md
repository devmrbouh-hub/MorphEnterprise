# AGENTS.md — инструкции для AI-агента

Проект **MorphEnterprise**. Читай этот файл в начале сессии.

---

## О проекте

Архитектурная концепция автономной агентной организации: не рой агентов, а организация минимально достаточного размера под каждую mission.

**Точка входа (канон, EN):** [docs/concept/en/00-overview.md](docs/concept/en/00-overview.md)

**Полный текст (RU):** [docs/concept/ru/00-overview.md](docs/concept/ru/00-overview.md)

---

## Начало каждой сессии

1. Прочитать [docs/state.md](docs/state.md) — где мы сейчас
2. Прочитать [docs/ROADMAP.md](docs/ROADMAP.md) — фаза и next step
3. При необходимости — последние 2 записи [docs/JOURNAL.md](docs/JOURNAL.md)

---

## Терминология (v2, обязательно)

| Использовать | Не использовать |
|--------------|-----------------|
| Worker | agent, executor |
| Director, Planner, RuntimeCoordinator | оркестратор (без уточнения) |
| SizingDecision, Mission, Workspace | solo / small / full org |

Полный глоссарий: [docs/concept/en/glossary.md](docs/concept/en/glossary.md) (канон) · [ru/glossary.md](docs/concept/ru/glossary.md)

---

## Принципы (кратко)

- **P0** — минимально достаточная организация
- **P1** — организация важнее Worker'ов
- **P2** — Workspace — центр тяжести
- **P3** — context slice, не весь контекст
- **P4** — компетенции, не должности
- **P5** — workflow = результат планирования
- **P6** — resize, не только restart
- **P7** — QC по risk tier
- **P8** — обязательный handoff
- **P9** — эскалация: модель → организация → человек

Подробно: [docs/concept/ru/01-principles.md](docs/concept/ru/01-principles.md)

---

## Конец сессии (только Agent mode)

Если были изменения в репозитории:

1. Обновить [docs/state.md](docs/state.md) (фаза, next step, последний коммит, дата UTC+9)
2. Добавить запись в начало [docs/JOURNAL.md](docs/JOURNAL.md)
3. Уроки dogfooding — в [docs/concept/lessons.md](docs/concept/lessons.md) при наличии
4. Git commit с понятным сообщением

В **Ask mode** журнал и state не менять без явной просьбы пользователя.

---

## Phase 0 ограничения

- **Без БД** — markdown + git
- **Без преждевременного кода** — до ADR-001 и Phase 2
- **Не менять** [Концепция.md](Концепция.md) v1 без явной просьбы
- Архитектурные правки — сверка с [docs/concept/](docs/concept/)

---

## Карта docs/

| Путь | Содержание |
|------|------------|
| [docs/state.md](docs/state.md) | Текущий статус |
| [docs/ROADMAP.md](docs/ROADMAP.md) | Фазы и ADR |
| [docs/JOURNAL.md](docs/JOURNAL.md) | Журнал сессий |
| [docs/competencies.md](docs/competencies.md) | Registry stub |
| [docs/decisions/](docs/decisions/) | ADR (канон, EN) |
| [docs/decisions/ru/](docs/decisions/ru/) | ADR (перевод, RU) |
| [docs/concept/en/](docs/concept/en/) | Концепция v2 (канон, EN) |
| [docs/concept/ru/](docs/concept/ru/) | Концепция v2 (полный текст, RU) |
| [docs/concept/lessons.md](docs/concept/lessons.md) | Уроки dogfooding |
| [docs/concept/schemas/](docs/concept/schemas/) | YAML-контракты |
| [docs/references/](docs/references/) | Внешние исследования (не канон); см. [README](docs/references/README.md) |

---

## Dogfooding

Мы строим MorphEnterprise её же принципами: человек = Director, `docs/` = Workspace, Cursor = ExecutionEngine.

См. [docs/concept/ru/09-dogfooding.md](docs/concept/ru/09-dogfooding.md)
