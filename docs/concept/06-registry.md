# Competency Registry

Каталог возможностей системы. Все роли (Director, Planner, Worker, QC) берут ресурсы отсюда.

---

## ResourceType

```yaml
ResourceType: model | tool | human
```

| Тип | Примеры |
|-----|---------|
| model | LLM с ModelProfile |
| tool | git, linter, search, MCP |
| human | эксперт для human gate |

---

## Competency

Компетенция — **навык**, не должность (P4).

```yaml
id: api_design
name: "Проектирование API"
description: "Схемы данных, контракты, REST/gRPC"
required_tools: [schema_validator]
memory_namespace: competency/api_design
domains: [software_architecture]
```

Схема: [schemas/competency.yaml](schemas/competency.yaml).

---

## ModelProfile

```yaml
id: model-sonnet
name: "Claude Sonnet (пример)"
resource_type: model
context_window: 200000
cost_per_1k_tokens: 0.003
relative_reasoning: 0.75
strengths: [coding, architecture, review, speed]
weaknesses: [highest_risk_architecture_alone]
domains: [software, documentation]
trust_for_risk:
  low: true
  medium: true
  high: false
  critical: false
```

Схема: [schemas/model-profile.yaml](schemas/model-profile.yaml).

Director, Planner и Worker ссылаются на model_id из Registry.

---

## Tool

```yaml
id: tool-git
resource_type: tool
name: "Git operations"
capabilities: [read, commit, diff]
constraints:
  require_human_approval_for: [push]
```

---

## Human resource

```yaml
id: human-founder
resource_type: human
name: "Founder / Architect"
availability: async
gates: [architecture_decision, critical_risk]
contact: github_discussion
```

Используется в human_gates SizingDecision и QualityGovernance.

---

## TaskProfile

Вход для matching (создаётся Director при parse):

```yaml
work_units: 3
competencies: [system_design, api_design, technical_review]
reasoning_need: 0.7
risk: medium
context_estimate: 40000
parallelizable: false
```

Схема: [schemas/task-profile.yaml](schemas/task-profile.yaml).

---

## Matching: task_profile × model_profile

```
FOR each competency IN task_profile.competencies:
  SELECT model FROM Registry
  WHERE model.domains MATCH competency
    AND model.relative_reasoning >= task_profile.reasoning_need (if single-model path)
    AND model.trust_for_risk[task_profile.risk]
  ORDER BY cost ASC, reasoning DESC
```

При capability gap — см. [04-director-sizing.md](04-director-sizing.md).

---

## Director в Registry

```yaml
id: role-director-weak
resource_type: model
model_id: model-haiku
role: director
triage_policy:
  max_executor_count_without_review: 1
  require_strong_review_if_confidence_below: 0.7
```

```yaml
id: role-director-strong
resource_type: model
model_id: model-opus
role: director
triage_policy:
  used_for: [ambiguous_mission, high_risk, second_opinion]
```

---

## Решение v1 §3: объединить / разделить / человек / инструмент

| Ситуация | Решение Registry + Director |
|----------|----------------------------|
| Одна компетенция, слабый gap | 1 Worker, 1 model |
| Несколько компетенций, одна модель справляется | 1 Worker, несколько competency_ids |
| Компетенции требуют разделения ролей | N Workers |
| risk critical | human resource в human_gates |
| Детерминированная операция | tool без LLM |

---

## Сквозной пример: спецификация Workspace

| Ресурс | Использование |
|--------|---------------|
| competency: system_design | Writer |
| competency: technical_review | Critic |
| model-sonnet | Writer |
| model-haiku | Critic, Director (weak) |
| human-founder | gate после finalize, если risk повышен |
