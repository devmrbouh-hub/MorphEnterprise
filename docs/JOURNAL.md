# Журнал изменений

Новые записи **сверху**. Формат: дата/время (UTC+9), что сделано, зачем, файлы, коммит.

---

## 2026-07-18 18:20 (UTC+9)

**Что сделано** — слой `docs/references/`: README, шаблон, backlog, sources/landscapes/comparisons; конспект Крестникова, landscape мультиагентности 2026, comparison vs MorphEnterprise; morph-references.mdc; ссылки в AGENTS, concept/README, decisions/README

**Зачем** — оформить внешние исследования (Knowledge layer) и путь идея → backlog → ADR без смешения с каноном concept

**Файлы** — docs/references/**, .cursor/rules/morph-references.mdc, AGENTS.md, docs/concept/README.md, docs/decisions/README.md, docs/state.md

**Коммит** — _(pending)_

---

**Что сделано** — RU-перевод ADR-001 (`docs/decisions/ru/`); политика bilingual ADR в README, CONTRIBUTING; ссылки EN↔RU

**Зачем** — Director (человек) читает ADR на русском; EN остаётся каноном для публичной спецификации

**Файлы** — docs/decisions/ru/ADR-001-workspace-spec.md, docs/decisions/README.md, CONTRIBUTING.md, docs/state.md

**Коммит** — 474a41a

---

## 2026-07-09 15:30 (UTC+9)

**Что сделано** — ADR-001 Workspace spec (EN, proposed): protocol-first WorkspaceStore / SliceResolver / HandoffWriter; workspace profiles; dogfooding appendix

**Зачем** — Phase 1: формализовать Workspace-протокол без выбора storage; закрыть draft для Issue #2

**Файлы** — docs/decisions/ADR-001-workspace-spec.md, docs/decisions/README.md, docs/ROADMAP.md, docs/state.md, docs/concept/lessons.md

**Коммит** — 9c9515c

---

## 2026-07-09 15:00 (UTC+9)

**Что сделано** — EN-канон: `docs/concept/en/`; RU в `ru/`; bilingual README; CONTRIBUTING EN-first; GitHub templates; миграция ссылок

**Зачем** — Discoverability для англоязычной аудитории при сохранении RU dogfooding

**Файлы** — docs/concept/en/, docs/concept/ru/, README.md, CONTRIBUTING.md, AGENTS.md, .github/, docs/ROADMAP.md, docs/state.md

**Коммит** — 59be5f5

---

## 2026-07-09 13:58 (UTC+9)

**Что сделано** — Первый push на GitHub: `main` → origin, remote настроен

**Зачем** — Публичная публикация концепции v2 и Phase 0 Workspace

**Файлы** — docs/state.md, docs/ROADMAP.md

**Коммит** — d132a47

---

## 2026-07-09 13:55 (UTC+9)

**Что сделано** — Подготовка к публикации на GitHub: LICENSE (Apache 2.0), NOTICE, CONTRIBUTING; обновлены README, ROADMAP, lessons; ветка `main`

**Зачем** — Публичный репозиторий с явным авторством и правилами контрибьюта перед первым push

**Файлы** — LICENSE, NOTICE, CONTRIBUTING.md, README.md, docs/ROADMAP.md, docs/concept/lessons.md

**Коммит** — d1b5e52

---

## 2026-07-09 02:52 (UTC+9)

**Что сделано** — Phase 0 Workspace: state, ROADMAP, JOURNAL, competencies, lessons, decisions; AGENTS.md; Cursor rules

**Зачем** — dogfooding: фиксация контекста для сессий с AI, подготовка к ADR-001

**Файлы** — docs/state.md, docs/ROADMAP.md, docs/JOURNAL.md, docs/competencies.md, docs/concept/lessons.md, docs/decisions/, AGENTS.md, .cursor/rules/

**Коммит** — 8e771bf

---

## 2026-07-09 02:35 (UTC+9)

**Что сделано** — Инициализирован git, первый коммит; README, .gitignore

**Зачем** — Зафиксировать базу проекта под version control

**Файлы** — README.md, .gitignore, весь docs/concept/

**Коммит** — ee9181a

---

## 2026-07-09 02:22 (UTC+9)

**Что сделано** — Написана концепция MorphEnterprise v2: 10 разделов, 8 YAML-схем, cross-review, e2e-сценарий

**Зачем** — Формализовать архитектуру (Director, Sizing, RuntimeCoordinator, Workspace) для декомпозиции

**Файлы** — docs/concept/*, docs/concept/schemas/*

**Коммит** — (включено в ee9181a)

---

## 2026-07-08 (UTC+9)

**Что сделано** — Исходная концепция v1 (Концепция.md)

**Зачем** — Первая сводная модель «виртуального предприятия»

**Файлы** — Концепция.md

**Коммит** — (включено в ee9181a)

---
