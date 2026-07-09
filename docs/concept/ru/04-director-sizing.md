# Director и Sizing

Ключевой слой v2: **организация по необходимости**, а не по умолчанию.

---

## 4.1. Роль Director

Director — **не оракул и не исполнитель**. Это роль triage и sizing:

- оценивает mission и контекст;
- вычисляет capability gap;
- выдаёт SizingDecision;
- оценивает стоимость и confidence.

Director сам является **записью в CompetencyRegistry** (ModelProfile + политика triage).

### Слабая vs сильная модель

| Ситуация | Модель Director |
|----------|-----------------|
| Явно простые задачи, rule-based fast path | weak или без LLM |
| Поток однотипных задач | weak + кэш решений |
| Размытая mission, architecture, high risk | strong |
| weak Director, confidence < 0.7 | strong second opinion |
| strong Director, confidence < 0.5 | human gate |

**Правило:** слабый Director не принимает дорогие организационные решения (высокий executor_count, discovery) без подтверждения.

### Bootstrap Director

Парадокс: Director читает Registry, но сам в Registry.

Решение:

1. **Rule-based fast path** — тривиальные задачи без LLM (diff < N строк, risk=low).
2. **Bootstrap config** — фиксированная модель Director в конфиге первого запуска.
3. **Phase 0** — человек выполняет роль Director; Registry в markdown.

---

## 4.2. Две оси задачи

### Ось A: сложность шага (per unit)

- неопределённость формулировки;
- reasoning_need;
- число компетенций на единицу;
- risk;
- стоимость ошибки.

### Ось B: объём работы

- work_units (число подзадач);
- context_size;
- parallelizable;
- число артефактов/файлов.

**Важно:** простой шаг при большом объёме → много Worker'ов (throughput gap), а не «полная организация».

| | Низкий объём | Высокий объём |
|---|-------------|---------------|
| **Простой шаг** | 1 weak Worker | N weak Workers, parallelism |
| **Сложный шаг** | 1 strong Worker | strong + специалисты + QC |

---

## 4.3. Capability gap

Организация растёт там, где **одна модель не закрывает разрыв**:

| Измерение | Gap означает |
|-----------|--------------|
| reasoning | reasoning_need > model.relative_reasoning |
| context | context_estimate > model.context_window |
| throughput | work_units × unit_time > допустимое время одной модели |
| competencies | len(required) > что одна модель может «надеть» |
| risk | risk > model.trust_for_risk |

**Порядок закрытия gap:**

1. Сменить модель на более сильную (без добавления Worker'ов).
2. Добавить Worker'ов (parallelism или разделение компетенций).
3. Включить Planner (planner_depth).
4. Включить Discovery.
5. Эскалировать к человеку.

---

## 4.4. SizingDecision

Выход Director. Схема: [../schemas/sizing-decision.yaml](../schemas/sizing-decision.yaml).

```yaml
# Непрерывные параметры (первичны)
executor_count: 2
parallelism: 1

# Уровни глубины (shorthand)
planner_depth: 1          # 0 | 1 | 2
discovery_required: false
qc_depth: critic          # 0 | critic | full

model_assignments:
  director: model-sonnet
  worker_writer: model-sonnet
  worker_critic: model-haiku

human_gates:
  - after: final_adr
    if: risk_tier >= high

estimated_cost:
  tokens: 120000
  usd: 1.2

confidence: 0.82
escalation_policy:
  on_low_confidence: strong_director_review
  on_failure: add_critic

rationale: >
  Две компетенции (design + review), medium risk,
  один сильный writer и дешёвый critic дешевле одного opus.
```

### planner_depth

| Значение | Смысл |
|----------|--------|
| 0 | Нет Planner; RuntimeCoordinator запускает Worker'ов напрямую по SizingDecision |
| 1 | Lite Planner: линейный или простой DAG task graph |
| 2 | Full Planner: discovery hints, параллельные ветки, шаблоны организаций |

### qc_depth

| Значение | Смысл |
|----------|--------|
| 0 | self-check Worker'а |
| critic | отдельный Worker-критик |
| full | critic + guardian (+ arbiter при спорах) |

---

## 4.5. Алгоритм sizing (7 шагов)

```
1. PARSE
   Разобрать mission → task_profile
   (work_units, competencies, risk, context_estimate, parallelizable)

2. SELECT_DIRECTOR
   Выбрать модель Director (или rule-based skip)
   При ambiguity → strong Director

3. MATCH_MODELS
   Для каждой компетенции — минимально достаточная модель из Registry

4. CHECK_SINGLE_MODEL
   Может ли ОДНА модель закрыть всё
   (все компетенции + объём + risk + context)?

5. IF YES → executor_count=1, planner_depth=0, минимальный qc

6. IF NO → определить gap:
   - throughput → executor_count, parallelism
   - competencies → несколько Workers
   - reasoning → stronger model или critic
   - uncertainty → discovery_required, planner_depth ≥ 1
   - risk → qc_depth, human_gates

7. ESTIMATE_COST + CONFIDENCE
   Сравнить варианты; выбрать минимально достаточный по бюджету
   confidence < threshold → escalation_policy
```

### risk_tier

- Mission задаёт **floor** (минимальный risk).
- Director может **только повысить**, не понизить.

---

## 4.6. Примеры sizing

| Задача | work_units | executor_count | planner_depth | discovery | Модели | Почему |
|--------|------------|----------------|---------------|-----------|--------|--------|
| Исправить опечатку | 1 | 1 | 0 | false | 1× weak | gap=0 |
| Написать ADR Workspace | 3 | 2 | 1 | false | strong + medium critic | 2 компетенции, medium risk |
| 50 однотипных тестов | 50 | 10 | 1 | false | 10× weak parallel | throughput gap |
| Новый продукт для МСБ | 20+ | 8+ | 2 | true | mixed | uncertainty + много доменов |
| Выбор лицензии | 1 | 1 | 0 | false | 1× medium | узко, human_gate |

---

## Сквозной пример: спецификация Workspace

**Task profile:**

```yaml
work_units: 3
competencies: [system_design, api_design, technical_review]
reasoning_need: 0.7
risk: medium
context_estimate: 40000
parallelizable: false
```

**SizingDecision:** executor_count=2, planner_depth=1, qc_depth=critic, discovery=false.

Director выбирает strong writer + haiku critic — дешевле одного opus при том же качестве review.
