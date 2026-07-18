# Внешние исследования (references)

Конспекты, обзоры и сравнения **чужих работ** — не канон MorphEnterprise. Нормативная спека: [concept/](../concept/). Решения: [decisions/](../decisions/).

## Связь с Workspace

| Путь | Слой памяти (concept §05) | Содержание |
|------|---------------------------|------------|
| `sources/`, `landscapes/` | **Knowledge** (Phase 0) | Внешние знания, `knowledge_links` |
| `comparisons/`, `backlog.md` | Наша интерпретация | До ADR — не Project Memory |
| ADR, `concept/lessons.md` | Project Memory | После принятия / dogfooding |

**Цепочка внедрения:** `sources/` → `comparisons/` → `backlog.md` / ROADMAP → ADR → concept (при необходимости).

Идеи из references **не попадают в concept напрямую**.

## Типы записей

| Тип | Папка | Содержание |
|-----|-------|------------|
| `source` | `sources/` | Нейтральный конспект одного источника (без «берём / не берём») |
| `landscape` | `landscapes/` | Синтез нескольких источников по теме |
| `comparison` | `comparisons/` | Наша оценка ↔ P0–P9, ADR; action items |

Шаблон: [_template.md](_template.md). Кандидаты на внедрение: [backlog.md](backlog.md).

## Workflow

| Шаг | Действие | Артефакт |
|-----|----------|----------|
| 1 | Найти источник | URL в frontmatter |
| 2 | Конспект рабочих идей | `sources/<slug>.md`, status: `draft` |
| 3 | Сопоставить с концепцией | `comparisons/<topic>.md` (если есть решение внедрять/отклонять) |
| 4 | Зафиксировать действия | `backlog.md`; крупное → [ROADMAP.md](../ROADMAP.md) или issue |
| 5 | Внедрение | ADR; после dogfooding → [lessons.md](../concept/lessons.md) |

**Статусы:** `draft` → `reviewed` → `stale` (>6 мес или заменено новым ref).

**Именование файлов:** `<author>-<topic>-<year>.md` (sources), `<topic>-landscape-<year>.md` (landscapes), `<topic>-vs-morphenterprise.md` (comparisons).

## Ссылки (knowledge_links)

- **ID:** `ref:<id>` (например `ref:ref-2026-krestnikov-git-skills`)
- **Путь:** `docs/references/sources/<file>.md`
- В ADR: `Research: [title](path) (ref:<id>)`

## Каталог

| id | title | type | status | morph_takeaway |
|----|-------|------|--------|----------------|
| ref-2026-krestnikov-git-skills | Git-skills как память агентов | source | reviewed | Lazy skill load ≈ context slice (P3) |
| ref-2026-multi-agent-landscape | Мультиагентность 2026 | landscape | reviewed | Платформы + оркестрация; evals отстают от observability |
| ref-2026-krestnikov-comparison | Крестников vs MorphEnterprise | comparison | reviewed | Skill-bundle → ADR-002; loops → lifecycle |

## Быстрый старт

1. Скопировать `_template.md` в нужную подпапку.
2. Заполнить frontmatter (`id`, `type`, `urls`, …).
3. Добавить строку в таблицу каталога выше.
4. При влиянии на дизайн — `comparisons/` и пункты в `backlog.md`.
