# Quality и Governance

Контроль качества масштабируется по **risk tier** (P7). Не бюрократический взрыв на мелочах.

---

## Risk tier

| Уровень | Примеры | QC |
|---------|---------|-----|
| **low** | Опечатка, форматирование, комментарий | self-check Worker'а |
| **medium** | ADR, спецификация, рефакторинг модуля | critic |
| **high** | Security, API breaking change, архитектура | critic + guardian |
| **critical** | Production, деньги, персональные данные | critic + guardian + **human gate** |

### Правило floor

- Mission задаёт минимальный risk_tier.
- Director может повысить, не понизить.

---

## Роли QC

### Critic

Проверяет:

- соответствие success_criteria;
- качество и ошибки в артефакте;
- согласованность с decisions в Workspace.

Critic — отдельный Worker с competency technical_review и **другим** context slice (output + criteria, не весь проект).

### Guardian (страж)

Контролирует:

- бюджет (токены, cost);
- безопасность (секреты, опасные операции);
- лимиты (размер diff, число Worker'ов).

Guardian может **блокировать** до human.

### Arbiter (арбитр)

При споре critic vs worker или неоднозначном требовании. На ранних фазах — **человек** (human resource из Registry).

---

## qc_depth из SizingDecision

| qc_depth | Роли |
|----------|------|
| 0 | self-check |
| critic | Critic Worker |
| full | Critic + Guardian (+ Arbiter при reject loop) |

---

## Human gates

Из SizingDecision.human_gates:

```yaml
human_gates:
  - after: final_adr
    when: risk_tier >= high
  - after: any
    when: risk_tier == critical
```

При срабатывании:

1. RuntimeCoordinator приостанавливает task graph.
2. Уведомление human resource.
3. Ожидание approve/reject с записью в Workspace.
4. Таймаут и fallback — политика mission (escalate / cancel).

---

## Анти-паттерны

- Critic на каждую строку при low risk.
- Guardian без стража бюджета в длинных mission.
- Arbiter-LLM на critical без human.

---

## Сквозной пример: спецификация Workspace

- mission risk_tier: **medium** (floor).
- Director: qc_depth = **critic**.
- Writer завершает draft → Critic Worker проверяет ADR против success_criteria.
- Guardian: проверка budget_tokens не превышен.
- Human gate: не требуется (medium < high).
- Critic handoff: approve → finalize task.
