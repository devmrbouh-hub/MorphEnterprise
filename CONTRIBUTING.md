# Contributing to MorphEnterprise

Thank you for your interest. Public specification is **English-first**; detailed Russian chapters live in `docs/concept/ru/`.

## How to propose a change

1. Open an **Issue** — describe the problem or idea.
2. Wait for brief discussion (for non-trivial changes).
3. Open a **Pull Request** with a clear description and link to the Issue.

Small fixes (typos, wording) may skip the Issue step.

## Terminology

The project uses **concept v2** terms:

| Use | Don't use |
|-----|-----------|
| Worker | agent, executor |
| Director, Planner, RuntimeCoordinator | orchestrator (unqualified) |
| SizingDecision, Mission, Workspace | solo / small / full org |

Full glossary: [docs/concept/en/glossary.md](docs/concept/en/glossary.md).

## Where to look

- [docs/concept/en/00-overview.md](docs/concept/en/00-overview.md) — architecture v2 (canonical)
- [docs/ROADMAP.md](docs/ROADMAP.md) — phases and near-term tasks
- [docs/state.md](docs/state.md) — current status (Russian)
- [AGENTS.md](AGENTS.md) — Cursor agent rules (Russian)

## Language policy

- **Specification changes:** edit **English** first (`docs/concept/en/`).
- **Russian (`docs/concept/ru/`):** update in the same PR or follow-up Issue «Sync RU translation».
- **ADR:** English only (`docs/decisions/`).
- **JOURNAL / state:** Russian OK (internal dogfooding).

## Developer Certificate of Origin (DCO)

By submitting a Pull Request, you confirm that:

- you have the right to submit the contribution;
- the contribution is licensed under [Apache License 2.0](LICENSE);
- you agree to the license terms.

Optionally add to the PR description or commit:

```
Signed-off-by: Your Name <your.email@example.com>
```

A CLA is **not** required at this stage.

## License

By contributing, you agree that your contribution will be licensed under Apache 2.0 together with the rest of the repository.

---

## По-русски

Внутренние заметки (`docs/state.md`, `docs/JOURNAL.md`) и полные главы концепции — на русском в `docs/concept/ru/`. Канон публичной спецификации — английский в `docs/concept/en/`.
