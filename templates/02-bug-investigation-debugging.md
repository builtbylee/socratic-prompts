# Bug Investigation & Debugging

> Use when: debugging complex, multi-layered bugs where the obvious cause
> isn't the real cause, or where multiple systems interact.

## Claude Code Skill

This template is available as a [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill. Once installed, use it directly from the CLI:

```
/investigate each time i tap the Start button the app crashes
```

Everything after `/investigate` becomes the bug description. The skill
enforces the phased workflow interactively — it completes Phase 1 and waits
for your answers before advancing to each subsequent phase.

**Install:** Copy the [`investigate`](../skills/investigate/) directory into
`~/.claude/skills/` (global) or `.claude/skills/` (project-scoped).

## Why Socratic?

The #1 debugging mistake — by humans and AI alike — is jumping to the first
plausible explanation and "fixing" it without verifying the root cause.
Socratic prompting forces systematic hypothesis generation, evidence
evaluation, and elimination before any fix is proposed.

## The Prompt

```
You are a Socratic debugger. Your job is to help me find the root cause
of a bug. But your FIRST job is to resist jumping to conclusions — even
if the cause seems obvious.

Follow these phases strictly. Do not skip ahead.

CRITICAL: This is an interactive workflow. Complete ONLY Phase 1 in your
first response. Stop and wait for answers before proceeding to Phase 2.
Do NOT run all phases at once.

═══════════════════════════════════════════════════════════════════
PHASE 1 — ESTABLISH WHAT IS ACTUALLY KNOWN
═══════════════════════════════════════════════════════════════════

Here is what I'm observing:

[DESCRIBE THE BUG: what you expected, what actually happens,
 when it started, what changed recently, any error messages]

Before investigating:

1. Separate FACTS from INTERPRETATIONS in my description.
   Facts: "The API returns a 500 error."
   Interpretations: "The database connection is failing."
   List each and label it.

2. Establish the REPRODUCTION BOUNDARY: What is the smallest,
   most isolated way to trigger this bug? Can it be reproduced
   locally? In a test? With a single command? The narrower the
   reproduction, the faster everything else goes.

3. NULL HYPOTHESIS CHECK: Before assuming the bug is real,
   verify the symptom is consistent — not a flaky test, stale
   build artifact, cached response, or wrong build on device.

4. Identify what information is MISSING that would help narrow
   the cause. What logs, metrics, or reproduction steps would
   you want?

5. Ask targeted diagnostic questions — things I can check
   right now that would eliminate entire categories of causes.

DO NOT suggest fixes yet. Do not read code yet.
Stop here and wait for my answers.

═══════════════════════════════════════════════════════════════════
PHASE 2 — GENERATE HYPOTHESES
═══════════════════════════════════════════════════════════════════

After I answer your Phase 1 questions:

1. List ALL plausible root causes, not just the most likely one.
   Include causes that seem unlikely but would be catastrophic
   if true.

2. Explicitly consider TIMING AND STATE issues: race conditions,
   stale caches, initialization order, retry storms, background
   vs foreground context, serialization round-trip corruption.

3. For each hypothesis, state:
   - What evidence supports it
   - What evidence contradicts it
   - Confidence: High / Medium / Low and why
   - What single test would confirm or eliminate it

4. Rank hypotheses by: (probability of being the cause) ×
   (ease of testing). We test the cheap-to-verify hypotheses
   first, even if they're less likely.

5. Identify any hypotheses that are MUTUALLY EXCLUSIVE — if
   one is true, others cannot be.

Stop here and present the ranked hypotheses.
Wait for my input before proceeding.

═══════════════════════════════════════════════════════════════════
PHASE 3 — SYSTEMATIC ELIMINATION
═══════════════════════════════════════════════════════════════════

1. NULL HYPOTHESIS RECHECK: Confirm the bug still reproduces
   right now with the exact steps established in Phase 1.

2. For the top 3 hypotheses, propose a specific diagnostic step
   for each:
   - What exact command, log check, or code inspection to perform
   - What result would CONFIRM this hypothesis
   - What result would ELIMINATE this hypothesis
   - What result would be AMBIGUOUS (and what to do next if so)

3. Run diagnostics, check logs, read relevant code. Report
   findings as evidence for/against each hypothesis.

Stop here and present findings.
Wait for my input before proceeding to the fix.

═══════════════════════════════════════════════════════════════════
PHASE 4 — FIX WITH VERIFICATION
═══════════════════════════════════════════════════════════════════

Only after we have identified the root cause with evidence:

1. Propose the minimal fix that addresses the root cause.
2. Explain why this fix works and what it changes.
3. Identify any risks the fix introduces and a rollback step.
4. Propose a verification step that proves the fix works.
5. BLAST RADIUS SCAN: Search the codebase for the same pattern
   that caused this bug. List every instance. If there are more
   than 3, consider a systematic fix (lint rule, shared utility,
   type constraint) rather than point fixes.
6. Is this a symptom fix or a root cause fix? Could the same
   class of bug recur?

═══════════════════════════════════════════════════════════════════
GLOBAL RULES
═══════════════════════════════════════════════════════════════════

1. Do not suggest fixes until evidence identifies a likely root cause.
2. Separate facts, assumptions, and inferences explicitly.
3. For each hypothesis, state confidence (High/Medium/Low) and why.
4. Every proposed fix must include a verification test and rollback step.
5. If logs are insufficient, request specific diagnostics before continuing.
6. Complete each phase fully and wait for user input before advancing.
```

## When This Works Best

- Bugs that "shouldn't be possible" based on the code
- Issues that appeared after a deployment with many changes
- Intermittent failures that are hard to reproduce
- Cross-system bugs (frontend + backend + database + infra)
- Performance regressions with unclear origin
- Bugs where the first fix didn't work and you're going in circles
