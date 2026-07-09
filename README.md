# MorphEnterprise

Architecture for **autonomous agent organizations**: not a pre-built swarm of agents, but a system that assembles **minimally sufficient teams** per mission.

**Differentiators:** parametric **SizingDecision** (not solo/small/full), **Director** at level 0, **Workspace**-centric memory with context slices, mandatory **Handoff**, QC by risk tier, **resize** not only restart.

## Documentation

| Version | Description |
|---------|-------------|
| [docs/concept/en/00-overview.md](docs/concept/en/00-overview.md) | **v2 canonical (EN)** — start here |
| [docs/concept/ru/00-overview.md](docs/concept/ru/00-overview.md) | v2 full detail (RU, chapters 01–10) |
| [Концепция.md](Концепция.md) | v1 archive (Russian) |

```
docs/concept/
├── en/           # canonical specification (English)
├── ru/           # detailed chapters (Russian)
├── schemas/      # YAML contracts
└── lessons.md    # dogfooding lessons
```

## Status

Concept v2 ready for ADR decomposition. **Current state:** [docs/state.md](docs/state.md)

## Repository

https://github.com/devmrbouh-hub/MorphEnterprise

## Author

Machnev Andrei Sergeevich ([devmrbouh-hub](https://github.com/devmrbouh-hub))

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[Apache License 2.0](LICENSE)

---

## Русский

Архитектурная концепция **автономной агентной организации**: не рой заранее созданных агентов, а организация, создающая команды минимально достаточного размера под каждую mission.

### Документация

| Версия | Описание |
|--------|----------|
| [Концепция.md](Концепция.md) | v1 — исходная концепция (архив) |
| [docs/concept/ru/00-overview.md](docs/concept/ru/00-overview.md) | **v2** — полный текст на русском |
| [docs/concept/en/00-overview.md](docs/concept/en/00-overview.md) | v2 — канон на английском |

### Концепция v2 (структура)

```
docs/concept/
├── en/                     # канон (EN)
├── ru/
│   ├── 00-overview.md
│   ├── 01-principles.md    # P0–P9
│   ├── 02-architecture.md  # 10 объектов
│   ├── 03-lifecycle.md
│   ├── 04-director-sizing.md
│   ├── 05-workspace.md
│   ├── 06-registry.md
│   ├── 07-quality-governance.md
│   ├── 08-execution-layer.md
│   ├── 09-dogfooding.md
│   ├── 10-e2e-scenario.md
│   └── glossary.md
├── schemas/
└── lessons.md
```

### Для работы с AI

- [AGENTS.md](AGENTS.md) — инструкции для агента в Cursor
- [docs/ROADMAP.md](docs/ROADMAP.md) — дорожная карта
- [docs/JOURNAL.md](docs/JOURNAL.md) — журнал изменений

### Phase 0 Workspace

| Файл | Назначение |
|------|------------|
| [docs/state.md](docs/state.md) | Где мы сейчас |
| [docs/competencies.md](docs/competencies.md) | Registry stub |
| [docs/decisions/](docs/decisions/) | ADR |
| [docs/concept/lessons.md](docs/concept/lessons.md) | Уроки dogfooding |

Следующий шаг — ADR-001: Workspace spec.
