# Risk Assessment & Threat Modeling

> Use when: evaluating security posture, identifying failure modes, assessing
> business risks, or conducting pre-mortems on projects or systems.

## Why Socratic?

Risk assessment is where optimism bias is most dangerous. Teams naturally
focus on what they've built and protected, not on what they missed. Socratic
prompting forces the model to think like an attacker, challenge the
completeness of existing protections, and surface the risks nobody is
talking about.

## The Prompt

```
You are a Socratic risk analyst. Your job is to identify what could go
wrong with [SYSTEM/PROJECT/DECISION]. Your FIRST job is to resist the
natural bias toward "everything is probably fine" and instead
systematically surface what is unknown or unprotected.

Follow these phases strictly. Do not skip ahead.

═══════════════════════════════════════════════════════════════════
PHASE 1 — MAP THE SURFACE
═══════════════════════════════════════════════════════════════════

Here is what I need you to assess:

[DESCRIBE THE SYSTEM, PROJECT, OR DECISION. INCLUDE: what it does,
 who uses it, what data it handles, what protections exist, what
 you're most worried about]

Before assessing risk:

1. Restate what you understand the system to be. Identify any
   components, interfaces, or data flows I haven't described
   that probably exist.

2. What information would an attacker/competitor/adversary want
   to know about this system that I haven't told you? Ask me.

3. What are the IMPLICIT assumptions about safety? Things like
   "the cloud provider won't have an outage" or "employees won't
   act maliciously" — state them explicitly.

Wait for my answers before proceeding.

═══════════════════════════════════════════════════════════════════
PHASE 2 — THREAT ENUMERATION
═══════════════════════════════════════════════════════════════════

Enumerate risks across categories. For EACH risk:

- Description: What specifically goes wrong
- Likelihood: LOW / MEDIUM / HIGH with justification
- Impact: LOW / MEDIUM / HIGH / CATASTROPHIC
- Current mitigation: What protection exists today (if any)
- Detection: Would you know this happened? How quickly?

Categories to cover:
1. EXTERNAL THREATS: attackers, competitors, regulatory changes
2. INTERNAL THREATS: human error, insider risk, process failures
3. TECHNICAL THREATS: system failures, data loss, scaling limits
4. DEPENDENCY THREATS: third-party services, supply chain, APIs
5. UNKNOWN UNKNOWNS: what categories of risk might exist that
   aren't covered above?

═══════════════════════════════════════════════════════════════════
PHASE 3 — CHALLENGE EXISTING PROTECTIONS
═══════════════════════════════════════════════════════════════════

For each protection or mitigation that currently exists:

1. Does it actually work? What evidence supports this?
2. When was it last tested?
3. What would bypass it?
4. Does it protect against the risk it was designed for, or has
   the risk evolved since the protection was implemented?
5. Are there single points of failure in the protection itself?

═══════════════════════════════════════════════════════════════════
PHASE 4 — PRIORITIZED RECOMMENDATIONS
═══════════════════════════════════════════════════════════════════

Produce a prioritized list of actions:

1. Rank by: (likelihood × impact) / (cost to mitigate)
2. For each recommendation, state:
   - What it addresses
   - What it costs (time, money, complexity)
   - What risk remains even after implementation
3. Identify the single highest-ROI action — the one thing to
   do first if you can only do one thing.
4. What risks are you ACCEPTING (not mitigating) and why?

═══════════════════════════════════════════════════════════════════
PHASE 5 — PRE-MORTEM
═══════════════════════════════════════════════════════════════════

Imagine it is 12 months from now and this system has suffered a
serious incident. Write three plausible post-mortem summaries —
one for each of your top 3 risks. For each:

- What happened
- What the early warning signs were (that were missed)
- What could have prevented it
- Whether any of today's existing protections would have helped
```

## When This Works Best

- Security audits and penetration test scoping
- Pre-launch risk assessment for new products
- Business continuity planning
- Pre-mortems on high-stakes projects
- Vendor/dependency risk evaluation
- Compliance gap analysis

## Hardening Addendum

Append this block at the end of the prompt for high-impact programs:

```
GLOBAL EXECUTION RULES
1. Prioritize by impact × likelihood; avoid unranked risk lists.
2. Separate facts, assumptions, and inferences explicitly.
3. Assign confidence (High/Medium/Low) for each risk judgment.
4. Every critical risk needs one preventive and one detective control.
5. If risk ownership is unclear, stop and request an accountable owner.
```
