# Socratic Prompts

Battle-tested Socratic prompt templates that force AI models to **interrogate problems before solving them**.

Standard prompts ask for answers. Socratic prompts force the model to surface hidden assumptions, define ambiguous terms, challenge its own reasoning, and earn the right to answer by first demonstrating it understands the question.

## Why Socratic Prompting?

| Standard Prompt | Socratic Prompt |
|---|---|
| Model jumps to an answer | Model interrogates the problem first |
| Hidden assumptions go unchecked | Assumptions are surfaced and validated |
| Confident but potentially wrong | Honest about certainty vs uncertainty |
| Single perspective | Multiple perspectives examined |
| No self-correction | Built-in adversarial self-review |

**Benchmark results** (SSR paper, Nov 2025): Socratic Self-Refine doubled accuracy on Mini-Sudoku (42% to 95%) and improved AIME 2025 scores by 68% relative to standard Chain-of-Thought.

## The Templates

Each template targets a specific use case where the gap between standard and Socratic prompting is largest.

| # | Template | Best For |
|---|---|---|
| 1 | [Architecture & System Design](templates/01-architecture-system-design.md) | Designing systems, choosing tech stacks, making architectural decisions |
| 2 | [Bug Investigation & Debugging](templates/02-bug-investigation-debugging.md) | Tracing root causes of complex, multi-layered bugs |
| 3 | [Product Strategy & Decisions](templates/03-product-strategy-decisions.md) | Go/no-go decisions, feature prioritization, market analysis |
| 4 | [Deep Research & Analysis](templates/04-deep-research-analysis.md) | Research where source quality and confidence calibration matter |
| 5 | [Code Review & Refactoring](templates/05-code-review-refactoring.md) | Reviewing PRs, planning refactors, evaluating code quality |
| 6 | [Risk Assessment & Threat Modeling](templates/06-risk-assessment-threat-modeling.md) | Security reviews, business risk analysis, failure mode identification |
| 7 | [Writing & Communication](templates/07-writing-communication.md) | Blog posts, docs, emails, proposals where audience and tone matter |
| 8 | [Learning & Concept Exploration](templates/08-learning-concept-exploration.md) | Understanding new concepts deeply through guided questioning |
| 9 | [Data Analysis & Interpretation](templates/09-data-analysis-interpretation.md) | Analyzing data where biases, methodology, and conclusions need scrutiny |
| 10 | [Project Planning & Estimation](templates/10-project-planning-estimation.md) | Sprint planning, roadmaps, effort estimation, dependency mapping |
| 11 | [Migration & Compliance Readiness](templates/11-migration-compliance-readiness.md) | Taking personal/internal projects to public release, app store, or compliance |

## How to Use

1. Pick the template that matches your use case
2. Copy the prompt and fill in the `[PLACEHOLDERS]` with your specific context
3. Paste as your opening message to Claude, GPT, or any capable LLM
4. **Answer the model's Phase 1 questions before it proceeds** — this is where the value comes from

## When NOT to Use These

Socratic prompting adds overhead. Skip it for:
- Simple factual questions ("What is the capital of France?")
- Well-defined code generation ("Write a function that sorts an array")
- Formatting or transformation tasks ("Convert this JSON to YAML")
- Tasks where you've already done the thinking and just need execution

Use it when: the problem is ambiguous, has hidden assumptions, involves tradeoffs, or requires the model to reason about things it might get wrong.

## Compatibility

Tested with:
- Claude Opus 4.6, Sonnet 4.5
- GPT-5.2, GPT-4.1
- Any model that follows structured instructions

Models with strong instruction-following and extended context windows produce the best results. Smaller models may skip phases or give shallow answers to the interrogation steps.

## References

- [Chang 2023 — Prompting LLMs With the Socratic Method](https://arxiv.org/abs/2303.08769)
- [SSR: Socratic Self-Refine (2025)](https://arxiv.org/html/2511.10621v1)
- [Princeton SocraticAI](https://princeton-nlp.github.io/SocraticAI/)
- [SocraticLM — NeurIPS 2024](https://openreview.net/forum?id=qkoZgJhxsA)
- [The Socratic Prompt — Lumnitz, Jan 2026](https://pub.towardsai.net/the-socratic-prompt-how-to-make-a-language-model-stop-guessing-and-start-thinking-07279858abad)

## License

MIT
