# COS Implementation Specifications — System Overview

**Date:** June 15, 2026
**Author:** Chioma (Systems Architect)
**Status:** Implementation-Ready Specification
**Builder Target:** Antigravity

---

## 1. Architecture Summary

The Creative Operating System (COS) converts creative intent into finished output through orchestrated agent primitives. It is **not** a linear pipeline — it is a recursive function graph driven by an Intent Token.

### Core Primitives (AGE^T)

From Nessa's adversarial review: [COS_Architecture_v4_Creativity_First.md](../01_Capability_Architecture/COS_Architecture_v4_Creativity_First.md) and [COS_v4_Adversarial_Review.md](../01_Capability_Architecture/COS_v4_Adversarial_Review.md)

| Primitive | Signature | Description |
|-----------|-----------|-------------|
| **Attend** | `(context) → focus` | Determine what matters. Direct cognitive resources. |
| **Generate** | `(focus, constraints) → options` | Produce novelty. Ideas, forms, variations. |
| **Evaluate** | `(options, criteria) → scores` | Judge against intent and quality criteria. |
| **Transform** | `(options, evaluation) → refined` | Change existing forms based on evaluation. |

**Stopping Rule** (from [COS_Practicality_Review.md](../01_Capability_Architecture/COS_Practicality_Review.md)): AGE^T is the stopping point. Further decomposition (to BVSR's 2 primitives or to 1 "cognition" primitive) removes architectural structure without adding explanatory power. Each primitive maps to a different implementable behavior with different I/O signatures.

### The Chain of Production

```
Founder (User)
  ↓  Creative intent
Nessa (Research Lead)
  ↓  Validated research, architecture discoveries
Chioma (Systems Architect)
  ↓  Implementation-ready specifications
Antigravity (Builder)
  ↓  Working code
```

### Reference Map

Every specification below references the Nessa research document that supports it. Traceability is mandatory — if a decision cannot be traced to research, it is an assumption.

---

## 2. Core Principles

### P1: Research is validated input
Chioma does not re-research. Missing knowledge creates a research request back to Nessa.

**Reference:** [COS_Practicality_Review.md](../01_Capability_Architecture/COS_Practicality_Review.md) — "The next discovery won't come from another document. It will come from running code."

### P2: Implement, don't expand
Before proposing a new architectural layer:
1. Can the existing architecture solve it?
2. Prefer extending existing systems
3. Prefer simplification over expansion
4. New layers require strong justification

**Reference:** [COS_Practicality_Review.md](../01_Capability_Architecture/COS_Practicality_Review.md) — "Stop decomposing. Start building."

### P3: Intent is the spine
The Intent Token is the system's first-class data structure. Every function invocation reads from it, writes state updates, and validates output against it.

**Reference:** [COS_Architecture_v4_Creativity_First.md](../01_Capability_Architecture/COS_Architecture_v4_Creativity_First.md) §6.3

### P4: Feedback separated from authority
The Braintrust pattern: feedback evaluates and recommends. It does NOT decide. The Director retains full approval authority.

**Reference:** [Creative_Roles_as_Functions.md](../06_Agent_Architecture/Creative_Roles_as_Functions.md) §1 — "FEEDBACK != APPROVAL"

### P5: Recursive, not linear
Any function can invoke any other function. The architecture is a recursive function graph, not a linear pipeline.

**Reference:** [COS_Architecture_v4_Creativity_First.md](../01_Capability_Architecture/COS_Architecture_v4_Creativity_First.md) §6.2

### P6: Default to simplest implementation
Each build decision should answer: "What is the simplest thing that validates the architecture?" Single workflow, single function, single output for MVP.

**Reference:** [Smallest_Viable_COS_and_First_Workflow.md](../04_Workflows/Smallest_Viable_COS_and_First_Workflow.md) — Storyboard as first workflow

---

## 3. Assumptions & Risks

### Verified Assumptions (high confidence)

| # | Assumption | Source | Status |
|---|-----------|--------|--------|
| A1 | Technical skill is the current creative bottleneck | Project brief + 3 pipeline studies | ✓ Verified |
| A2 | Production studios operate as specialist networks | All 6 research docs | ✓ Verified |
| A3 | Specialist roles have distinct knowledge & decision processes | All 6 research docs | ✓ Verified |
| A4 | AGE^T 4 primitives are sufficient to model creative acts | COS v4 Adversarial Review | ✓ Verified (composites of BVSR, Geneplore) |

### Questionable Assumptions (need implementation to validate)

| # | Assumption | Source | Confidence | Validation Method |
|---|-----------|--------|-----------|------------------|
| B1 | Storyboard workflow (4 capabilities) is the right first build | Smallest_Viable_COS.md | 45% | Build it. If storyboard → layout → environment expansion path works, validated. |
| B2 | Intent Token adds value over raw text prompt | COS v4 Architecture | 50% | Comparison test: Intent Token vs raw prompt on same output. |
| B3 | An Evaluate agent can produce useful quality scores | Decision_Architecture.md | 35% | Build Evaluate. Test against 10 human judgments. Target: r > 0.7 correlation. |
| B4 | Recursive function composition converges (no infinite loops) | COS v4 Architecture | 60% | Build one recursive composition (Realize calls Explore internally). If it halts, validated. |
| B5 | Feedback separated from authority works with AI agents | Creative_Roles_as_Functions.md | 40% | Test: does the Director accept/reject AI feedback at useful rates? |

### Risks

| # | Risk | Likelihood | Impact | Mitigation |
|---|------|-----------|--------|------------|
| R1 | Intent degradation across agent handoffs | Medium | High | Intent Token validation at every handoff. Evaluate against original intent before forward. |
| R2 | AI quality evaluation doesn't correlate with human judgment | High | Medium | Start with human-in-the-loop. Defer automated evaluation to Phase 3+. |
| R3 | Storyboard output quality too low to validate the architecture | Medium | Medium | Set quality bar at "narrative clarity," not "visual polish." Storyboards are intentionally rough. |
| R4 | Recursive function calls produce infinite loops or exponential blowup | Low | High | Implement depth limit (max 5 nested levels) and iteration limit (max 10 cycles). |
| R5 | Director cognitive load too high | Medium | High | Default to Model C (Hierarchical Studio) with Department Leads buffering the Director. |

---

## 4. Implementation Philosophy for Antigravity

1. **Single workflow first.** Build the storyboard workflow end-to-end before adding any second workflow.
2. **Hardcoded capabilities.** MVP starts with hardcoded capability mappings. The Capability Registry is not built until Phase 2.
3. **JSON files as persistent state.** No database in MVP. Intent Tokens are JSON files. Work state is JSON files.
4. **Single AI model provider.** Don't abstract model providers in MVP. Pick one and hardcode the integration.
5. **Human-in-the-loop for evaluation.** Evaluate agent recommends. Director decides. No auto-approval in MVP.
6. **Test with real intents.** 10+ storyboard briefs. Measure: intent fidelity, iteration count, user satisfaction.

---

*Next document: [01_MVP_Scope.md](01_MVP_Scope.md)*
