# Plan Contract & Implementation Gate

> Use when: you want an AI coding agent to produce a high-quality plan first, then implement only after explicit approval.

## Why This Template?

Many implementation failures start with weak plans: missing constraints, vague validation, and unclear acceptance criteria.
This template forces a contract-style plan format before any code is changed, which reduces drift and rework.

## The Prompt

```
You are in PLAN-ONLY mode. Do not implement anything.

Task:
[PASTE TASK]

Output must follow this exact schema and nothing else:

1) FACTS
- Bullet list of only verifiable facts from repo/context.

2) ASSUMPTIONS
- Numbered list.
- Any ambiguity must be listed here, not guessed.

3) NON-NEGOTIABLES
- Re-state these exact constraints verbatim:
  - No refine UX reintroduction
  - No speculative claims in source-backed sections
  - Must include performance budgets and measured SLOs
  - Must include blocking JD semantic gate with 422 fallback
  - Other roles must be non-blocking with explicit empty reason
  - Background-safe completion must survive lock/background/cold start
  - Must include verification commands and pass/fail criteria

4) REQUIREMENT→FILE MAP (table)
- Requirement | Files | Pass criterion
- Every requirement must map to at least one file and one measurable pass criterion.

5) STAGE BUDGETS (table)
- Stage | Hard timeout | Degrade behavior
- Include extraction, retrieval, synthesis, roles, draft, verification.

6) EXECUTION ORDER
- Ordered list with dependencies.

7) ACCEPTANCE TESTS
- Build/type checks
- Functional smoke checks
- Performance checks (min 5 runs each flow, p50/p90)
- Anti-regression checks

8) FAILURE MODES
- Top 5 risks + mitigation each.

9) PLAN QUALITY SELF-CHECK
- Score yourself 0–10 against:
  - Constraint adherence
  - Measurability
  - Scope control
  - Latency realism
- If any score <9, revise plan before returning it.

Hard rules:
- If any required section above is missing, your output is invalid.
- If any non-negotiable is not explicitly represented in Requirement→File map and Acceptance Tests, your output is invalid.
- Ask max 2 clarifying questions only if absolutely blocking; otherwise make conservative defaults and proceed.
- Keep under 900 tokens.
```

## When This Works Best

- Multi-file implementation requests with strict quality requirements
- Work that has repeatedly suffered from planning drift
- Teams balancing correctness, speed, and token efficiency
- Any project where implementation should only start after a formal plan gate
