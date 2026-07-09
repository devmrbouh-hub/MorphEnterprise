# Roadmap MorphEnterprise

## Текущая фаза

**Phase 0 → Phase 1:** концепция v2 завершена; настраиваем Workspace в markdown и переходим к ADR-001.

---

## Фазы (dogfooding)

| Фаза | Миссия | Статус | Критерий готовности | Артефакт |
|------|--------|--------|---------------------|----------|
| **0** | Оформить концепцию v2 + Phase 0 Workspace | done | cross-review пройден | [docs/concept/en/00-overview.md](concept/en/00-overview.md) |
| **0b** | JOURNAL, ROADMAP, AGENTS, Cursor rules | done | файлы созданы, commit 8e771bf | AGENTS.md, .cursor/rules/ |
| **1** | Спецификация Workspace | next | ADR согласован, 4 слоя памяти | ADR-001 |
| **2** | Workspace как код | planned | CRUD mission/decision/slice | код + тесты |
| **3** | Полуавтоматический Planner | planned | 70% планов с малыми правками | Planner module |
| **4** | Quality layer | planned | Critic ловит 50% до человека | QC module |
| **5** | Замкнутый цикл | planned | Mission без ручного планирования | E2E demo |

---

## Декомпозиция концепции v2 → ADR

| ADR | Тема | Источник | Статус |
|-----|------|----------|--------|
| ADR-001 | Workspace spec | [05-workspace.md](concept/ru/05-workspace.md) | planned |
| ADR-002 | Registry spec | [06-registry.md](concept/ru/06-registry.md) | planned |
| ADR-003 | Director/Sizing | [04-director-sizing.md](concept/ru/04-director-sizing.md) | planned |
| ADR-004 | Lifecycle state machine | [03-lifecycle.md](concept/ru/03-lifecycle.md) | planned |
| ADR-005 | Runtime coordination | [08-execution-layer.md](concept/ru/08-execution-layer.md) | planned |

---

## Ближайшие 2 недели

- [x] Концепция v2
- [x] Git init
- [x] Phase 0 Workspace docs (state, JOURNAL, ROADMAP, competencies, lessons)
- [x] AGENTS.md + Cursor rules
- [x] GitHub: repo — [devmrbouh-hub/MorphEnterprise](https://github.com/devmrbouh-hub/MorphEnterprise)
- [x] GitHub: первый push (`main`)
- [x] EN canonical docs (`docs/concept/en/`, `ru/` migration)
- [ ] ADR-001: Workspace spec (черновик, EN)

---

## Вне scope (пока)

- База данных (решение в ADR-001)
- Код Python/TypeScript (Phase 2)
- CLA (DCO в CONTRIBUTING достаточно на старте)
- Автономный Director/Planner
