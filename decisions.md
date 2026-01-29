# Engineering decisions and trade-offs – Vânia

This document captures architecture-level decisions behind the Vânia technology.
It is intentionally implementation-agnostic and does not include source code.

Decision 001 – Introduce an API mediation layer between UI and LLM provider

Context
Direct integration between UI and LLM providers tends to increase coupling, security exposure, and long-term maintenance cost.

Decision
Adopt an API as the single trusted entry point between chat interfaces and the LLM provider.

Rationale
- Centralizes governance of prompts, rules, and context.
- Enables provider replacement without UI changes.
- Reduces sensitive exposure in client-side layers.

Trade-offs
- Introduces an additional component to deploy and operate.
- Requires a minimal access-control strategy.

Decision 002 – Treat context as a first-class, versioned artifact

Context
LLM behavior is largely determined by contextual content rather than code.

Decision
Maintain corporate context as structured, versioned artifacts outside application code.

Rationale
- Enables review, audit, and controlled evolution.
- Separates content governance from software lifecycle.

Trade-offs
- Context growth must be actively managed.

Decision 003 – Context packaging strategy based on model window and cost

Context
Larger model context windows allow richer knowledge but typically increase cost and latency.

Decision
Adopt a flexible context packaging strategy:
- compact mode for small contexts and low cost
- wide-window mode when justified
- selective mode for large contexts, sending only relevant sections

Rationale
- Scales across small and large clients.
- Aligns quality with operational cost constraints.

Trade-offs
- Selective strategies introduce additional governance complexity.

Decision 004 – Explicit behavioral constraints and prompt-injection resistance

Decision
Enforce explicit behavioral rules and grounding constraints at the API layer.

Rationale
Predictability and safety are product requirements, not optional features.

Decision 005 – Minimal perimeter access control as initial security posture

Decision
Start with simple perimeter access control and evolve toward stronger authentication only when necessary.

Trade-offs
- Simplicity vs. fine-grained security.
