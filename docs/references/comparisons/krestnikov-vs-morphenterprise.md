---
id: ref-2026-krestnikov-comparison
title: "Крестников (git-skills) vs MorphEnterprise"
type: comparison
status: reviewed
published: 2026-07-18
reviewed: 2026-07-18
authors: [MorphEnterprise]
tags: [krestnikov, harness, skills, workspace, registry]
urls:
  - https://youtu.be/a-NIeMB-Hj8
related_concept:
  - docs/concept/ru/01-principles.md
  - docs/concept/ru/05-workspace.md
  - docs/concept/ru/06-registry.md
  - docs/concept/ru/08-execution-layer.md
related_adr: [ADR-001, ADR-002, ADR-004]
morph_takeaway: "Взять: skill-bundle, lazy slice, Curator, outer loops. Не брать: замена handoff, dark factory без risk tier"
---

# Крестников (git-skills) vs MorphEnterprise

**Источник:** [sources/krestnikov-git-skills-2026.md](../sources/krestnikov-git-skills-2026.md) (`ref-2026-krestnikov-git-skills`)

---

## TL;DR

Крестников описывает **уровень harness** (один универсальный агент + skills). MorphEnterprise — **уровень организации** (Director, Sizing, Workers, Handoff). Идеи совместимы: skills ≈ lazy Competency Memory; git-repo ≈ Knowledge layer; Curator ≈ Registry lifecycle. Не совместимо как замена: handoff, risk-tier QC, sizing.

---

## Матрица: их идея ↔ MorphEnterprise

| Их идея | У нас (P / ADR) | Вердикт |
|---------|-----------------|---------|
| Harness с ~30 тулами | ExecutionEngine, tools из Registry (§08) | **Совпадает** — адаптер, не ядро |
| Двухэтапная загрузка скилла | P3 context slice, SliceResolver (ADR-001) | **Взять** — формализовать в ADR-002 / SliceResolver |
| Skill-repo в git | Workspace Phase 0, Knowledge + `knowledge_links` | **Совпадает** — `docs/references/` = Knowledge |
| Скиллы = вся память | 4 слоя памяти + handoff (P2, P8, ADR-001) | **Частично** — skills = Competency Memory, не вся память |
| CI как backpressure | P7 QC по risk tier | **Усилить** — CI в dogfooding + QC layer |
| Man-on-the-loop | Director, P9 escalation | **Совпадает** |
| Hermes Curator (prune/merge) | Registry (ADR-002), P6 resize | **Взять** — Curator-паттерн для Registry |
| Ralph / meta loop | Lifecycle resize/retry (ADR-004) | **Взять** — явно описать outer/meta loops |
| Один harness решает всё | P0 минимально достаточная организация | **Расходится** — организация при capability gap |
| Dark factory без человека | P7, P9 human gates | **Не брать** для high risk |
| Замена handoff эволюцией скилла | P8 обязательный handoff | **Не брать** |
| MCP мёртв | Registry: tool type MCP (§06) | **Не брать** — skills + MCP дополняют |

---

## Рекомендуемые действия

→ дублировано в [backlog.md](../backlog.md)

| # | Действие | Target | Priority |
|---|----------|--------|----------|
| 1 | Описать competency как skill-bundle (`SKILL.md` + scripts + `data_namespace`) | ADR-002 | high |
| 2 | Двухэтапный индекс в SliceResolver (короткий дескриптор → полный slice) | ADR-001 appendix / Phase 2 | high |
| 3 | Curator для Registry: pruning неиспользуемых competency, consolidation дублей | ADR-002 | medium |
| 4 | Ralph Loop (outer) и meta loop для `discovery_required` mission | ADR-004 lifecycle | medium |
| 5 | CI backpressure в dogfooding (валидация при коммите агента) | Phase 0 practice | medium |

---

## Не брать

- **Скилл заменяет handoff** — знания остаются в skill-silo без Decision/Lesson/Artifact в Workspace
- **Git для всех данных** — большие blob только по ref (ADR-001); не 200 ГБ в repo
- **Dark factory без human gate** — только low risk; high/critical → Director + QC (P7, P9)
- **Отказ от организационного слоя** — хакатонный harness ≠ mission с sizing и QC
- **Auto-skill после 5 tool calls** без Curator и CI — риск мусорных competency

---

## См. также

- [Мультиагентность 2026](../landscapes/multi-agent-landscape-2026.md)
- [backlog.md](../backlog.md)
