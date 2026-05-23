---
type: concept
created: 2026-05-24
updated: 2026-05-24
tags: [area/agents, multi-agent, debate, design-pattern]
sources: ["[[2026-05-24 tauric-tradingagents-paper]]", "[[2026-05-24 tradingagents-framework-mindmap]]"]
confidence: medium
---

# Bull-Bear Debate

> A dialectical multi-agent pattern: two researcher agents take opposing
> bullish vs bearish positions on a trading thesis and argue through
> `n` rounds before a facilitator selects the prevailing perspective.

## Summary

In the [[2026-05-24 tauric-tradingagents-paper|Tauric framework]] the
Research Team consists of:

- **Bullish Researcher** — advocates for the trade, highlights positive
  signals, growth potential, favorable conditions.
- **Bearish Researcher** — argues against, surfaces risks, unfavorable
  signals, downside scenarios.
- **Facilitator (debate moderator)** — decides how many rounds to run,
  reviews the debate history at the end, and records the prevailing
  perspective as a structured entry in the global agent state.

This is the only place in the framework where unconstrained natural-
language dialogue happens (per [[Structured Agent Communication]]).
Everywhere else, agents exchange typed reports.

## Key claims

- **Forcing both sides improves factuality.** Cited in the paper via
  Du et al. (2023), *Improving factuality and reasoning in language
  models through multiagent debate*. The act of constructing a strong
  counter-argument surfaces information a single agent wouldn't volunteer.
  → [[2026-05-24 tauric-tradingagents-paper]] §4.2
- **Sentiment classification accuracy improves under debate** per the
  related-work section (Xing 2024, TradingGPT) — debate-driven agents
  outperform single-pass agents on the same classification task.
- **Natural language is appropriate *inside* a debate, not across teams.**
  The debate state is recorded as a structured entry, not propagated as
  free text downstream — this contains the "telephone effect"
  ([[Structured Agent Communication]]).

## Mechanics (Tauric variant)

1. Both researchers query the shared AgentState for analyst reports.
2. Each forms an initial opinion independently.
3. Researchers exchange arguments in natural language for `n` rounds.
4. The facilitator agent reviews the full debate history, selects the
   prevailing perspective, and writes it as a typed entry.
5. The Trader reads the prevailing perspective + the analyst reports.

The Risk Management Team in the same paper uses a 3-way version of this
(Aggressive / Conservative / Neutral) with the same `n`-round + facilitator
structure.

## Known failure modes

- **Convergence to a shared prior.** Both Bull and Bear may be the same
  LLM with different system prompts; their "disagreement" may be more
  rhetorical than substantive. → Open question on
  [[Multi-Agent LLM Trading Systems]].
- **Rhetoric over evidence.** Without anchoring claims to specific
  source citations, a debate can degrade into eloquent unsupported
  argument.
- **Facilitator bias.** If the facilitator picks the more articulate
  side rather than the better-evidenced side, the debate produces worse
  outcomes than no debate.
- **Round count tuning.** `n=1` may not give enough back-and-forth;
  `n=5` may produce convergence theater. The paper doesn't ablate this.

## Open questions

- Does forcing each side to *cite* specific analyst report passages
  (rather than free-form arguing) improve outcomes?
- Could an adversarial-LLM setup (Bull = Claude, Bear = GPT-4) actually
  improve independence?
- Has anyone benchmarked Bull-Bear-debate vs single-agent-with-CoT on
  the same prediction task, controlling for compute?

## Related

- [[Multi-Agent LLM Trading Systems]] — debate is one component.
- [[Structured Agent Communication]] — natural language is contained
  *inside* the debate; the result is structured.
- [[Agent Role Specialization]] — the most extreme specialization
  (deliberately opposed roles).
