# MorphEnterprise

Архитектурная концепция **автономной агентной организации**: не рой заранее созданных агентов, а организация, создающая команды минимально достаточного размера под каждую mission.

## Документация

| Версия | Описание |
|--------|----------|
| [Концепция.md](Концепция.md) | v1 — исходная концепция (архив) |
| [docs/concept/00-overview.md](docs/concept/00-overview.md) | **v2** — актуальная концепция, точка входа |

### Концепция v2

```
docs/concept/
├── 00-overview.md          # Обзор и границы
├── 01-principles.md        # P0–P9
├── 02-architecture.md      # 10 объектов системы
├── 03-lifecycle.md         # Главный цикл
├── 04-director-sizing.md   # Director, capability gap
├── 05-workspace.md         # Память, slices, handoff
├── 06-registry.md          # Компетенции, модели
├── 07-quality-governance.md
├── 08-execution-layer.md
├── 09-dogfooding.md
├── 10-e2e-scenario.md      # Сквозной сценарий
├── glossary.md
└── schemas/                # YAML-контракты
```

## Статус

Концепция v2 готова к декомпозиции в ADR. **Текущее состояние:** [docs/state.md](docs/state.md)

## Репозиторий

https://github.com/devmrbouh-hub/MorphEnterprise

## Автор

Machnev Andrei Sergeevich ([devmrbouh-hub](https://github.com/devmrbouh-hub))

## Contributing

См. [CONTRIBUTING.md](CONTRIBUTING.md).

## Лицензия

[Apache License 2.0](LICENSE)

## Для работы с AI

- [AGENTS.md](AGENTS.md) — инструкции для агента в Cursor
- [docs/ROADMAP.md](docs/ROADMAP.md) — дорожная карта
- [docs/JOURNAL.md](docs/JOURNAL.md) — журнал изменений

## Phase 0 Workspace

| Файл | Назначение |
|------|------------|
| [docs/state.md](docs/state.md) | Где мы сейчас |
| [docs/competencies.md](docs/competencies.md) | Registry stub |
| [docs/decisions/](docs/decisions/) | ADR |
| [docs/concept/lessons.md](docs/concept/lessons.md) | Уроки dogfooding |

Следующий шаг — ADR-001: Workspace spec.
