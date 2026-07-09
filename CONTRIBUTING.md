# Участие в MorphEnterprise

Спасибо за интерес к проекту. Документация и обсуждения ведутся на **русском языке**.

## Как предложить изменение

1. Откройте **Issue** — опишите проблему или идею.
2. Дождитесь краткого обсуждения (для нетривиальных изменений).
3. Создайте **Pull Request** с понятным описанием и ссылкой на Issue.

Для мелких правок (опечатки, формулировки) Issue можно пропустить.

## Терминология

Проект использует терминологию **концепции v2**. Обязательно:

| Использовать | Не использовать |
|--------------|-----------------|
| Worker | agent, executor |
| Director, Planner, RuntimeCoordinator | оркестратор (без уточнения) |
| SizingDecision, Mission, Workspace | solo / small / full org |

Полный глоссарий: [docs/concept/glossary.md](docs/concept/glossary.md).

## Куда смотреть

- [docs/ROADMAP.md](docs/ROADMAP.md) — фазы и ближайшие задачи
- [docs/state.md](docs/state.md) — текущее состояние
- [docs/concept/00-overview.md](docs/concept/00-overview.md) — архитектура v2
- [AGENTS.md](AGENTS.md) — правила для AI-агентов в Cursor

## Developer Certificate of Origin (DCO)

Делая Pull Request, вы подтверждаете, что:

- имеете право на предлагаемый вклад;
- вклад распространяется под [Apache License 2.0](LICENSE);
- вы согласны с условиями лицензии.

При желании добавьте в конец описания PR или в коммит:

```
Signed-off-by: Your Name <your.email@example.com>
```

CLA (Contributor License Agreement) на старте проекта **не требуется**.

## Лицензия

Внося вклад, вы соглашаетесь, что он будет лицензирован под Apache 2.0 вместе с остальным репозиторием.
