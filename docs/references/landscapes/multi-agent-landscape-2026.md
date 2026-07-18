---
id: ref-2026-multi-agent-landscape
title: "Мультиагентность и agentic engineering — обзор 2026"
type: landscape
status: reviewed
published: 2026-07-18
reviewed: 2026-07-18
authors: [MorphEnterprise research]
tags: [multi-agent, harness, orchestration, a2a, agentic-engineering]
urls: []
related_concept:
  - docs/concept/ru/02-architecture.md
  - docs/concept/ru/08-execution-layer.md
related_adr: [ADR-004, ADR-005]
morph_takeaway: "Платформы дают coordinator+specialists; evals отстают от observability; A2A+MCP дополняют друг друга"
---

# Мультиагентность и agentic engineering — обзор 2026

Синтез внешних источников (янв–июл 2026). Локальные конспекты — по мере добавления в `sources/`.

---

## TL;DR

Индустрия сместилась от «работают ли агенты?» к «как эксплуатировать надёжно». Тренды: coordinator + специализированные субагенты, длинные outer loops с CI backpressure, skills + lazy context, протоколы A2A (агент↔агент) и MCP (агент↔инструмент), multi-model по умолчанию. ~57% организаций с агентами в production, но quality и evals — главные пробелы.

---

## Каталог источников

| id / URL | Автор / org | Суть | Теги | local source |
|----------|-------------|------|------|--------------|
| ref-2026-krestnikov-git-skills | [Krestnikov](https://youtu.be/a-NIeMB-Hj8) | Harness, skills в git, Ralph/meta loops | harness, skills | [да](../sources/krestnikov-git-skills-2026.md) |
| — | [Karpathy — Sequoia Ascent 2026](https://www.youtube.com/watch?v=96jN2OCOfLs) | Software 3.0, agentic engineering, jagged intelligence | karpathy, quality | нет |
| — | [Karpathy — autoresearch](https://github.com/karpathy/autoresearch) | Автономный ML-loop: verifier + git ratchet | loop, karpathy | нет |
| — | [Anthropic — Code with Claude 2026](https://www.youtube.com/watch?v=wjvESxKgqaQ) | Managed Agents, multiagent orchestration, dreaming | anthropic, multi-agent | нет |
| — | [Anthropic — multiagent docs](https://platform.claude.com/docs/en/managed-agents/multiagent-orchestration) | Coordinator, до 20 агентов, shared FS, isolated threads | anthropic | нет |
| — | [OpenAI — Multi-agent API](https://developers.openai.com/api/docs/guides/responses-multi-agent) | GPT-5.6: spawn_agent, max 3 concurrent subagents | openai | нет |
| — | [Google — Managed Agents Gemini](https://ai.google.dev/gemini-api/docs/agents) | Antigravity agent, AGENTS.md + SKILL.md | google, harness | нет |
| — | [Google — Gemini Enterprise Agent Platform](https://cloud.google.com/blog/products/ai-machine-learning/introducing-gemini-enterprise-agent-platform) | ADK graph sub-agents, Agent Garden | google, enterprise | нет |
| — | [A2A Protocol v1.0](https://a2a-protocol.org/) | Agent-to-agent стандарт (Linux Foundation) | protocol, a2a | нет |
| — | [Microsoft Agent Framework 1.0](https://devblogs.microsoft.com/agent-framework/agent-frameworks-orchestration-patterns-reach-1-0/) | Sequential, concurrent, handoff, magentic patterns | microsoft, patterns | нет |
| — | [LangChain — State of Agent Engineering 2026](https://www.langchain.com/state-of-agent-engineering) | 57% in production; quality #1 barrier; 89% observability vs 52% evals | survey | нет |
| — | [Datadog — State of AI Engineering 2026](https://www.datadoghq.com/state-of-ai-engineering/) | 69% multi-model; 59% agent requests = 1 call; rate limits | survey, ops | нет |

---

## Пять трендов

1. **Harness + минимальные тулы** — расширение через skills, не сотни MCP-функций в контексте.
2. **Coordinator + specialists** — Anthropic, OpenAI, Google, Microsoft: lead agent делегирует с изолированным контекстом и общей FS/sandbox.
3. **Длинные циклы** — Ralph Loop, autoresearch: outer loop + verifier (CI, метрика) + git state.
4. **Протоколы, не один победитель** — MCP (tools) + A2A (agents); federated stack.
5. **Agent engineering как дисциплина** — observability table stakes; evals и governance отстают.

---

## Что читать первым

1. [Karpathy — Sequoia Ascent 2026](https://www.youtube.com/watch?v=96jN2OCOfLs) — общая картина Software 3.0
2. [Krestnikov — git-skills](../sources/krestnikov-git-skills-2026.md) — практика harness + skills (RU)
3. [LangChain State of Agent Engineering 2026](https://www.langchain.com/state-of-agent-engineering) — цифры production
4. [A2A Protocol](https://a2a-protocol.org/) — если планируются remote Workers
5. [Microsoft Magentic pattern](https://learn.microsoft.com/en-us/agent-framework/workflows/orchestrations/magentic) — open-ended multi-agent

---

## См. также

- [Крестников vs MorphEnterprise](../comparisons/krestnikov-vs-morphenterprise.md)
- [backlog.md](../backlog.md) — кандидаты на внедрение
