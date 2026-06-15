# Practicality Review — When to Stop Decomposing and Start Building

**Date:** June 15, 2026
**Context:** After four architecture iterations (v1→v2→v3→v4 → adversarial review → AGE^T), the trap is clear: infinite vertical descent into deeper abstractions.

## 1. The Infinite Descent Problem

AGE^T proposes 4 primitives: Attend, Generate, Evaluate, Transform.

But Praize correctly challenges:

```
Attend    → Evaluate(importance)      — "what matters?" IS a judgment
Transform → Generate(new from old)     — producing a new state IS generation
Generate  → Transform(mental state)    — generating IS changing what's in your head
```

This creates circularity. You can keep descending:

```
AGE^T → 2 primitives (Generate + Evaluate) 
  → 1 primitive (Information Processing)
    → 0 primitives (everything is the same thing)
```

At the bottom is **cognition** — one primitive that does everything. Which is useless for architecture design.

### The Stopping Rule

**Decomposition is complete when further reduction produces primitives that are indistinguishable in implementation.**

Apply the test:

| Pair | Theoretically Reducible? | Implemented Differently? | Should They Merge? |
|------|------------------------|------------------------|-------------------|
| Attend / Evaluate | Yes — Attend = Evaluate(importance) | YES — Attend selects what to process next. Evaluate produces a quality score. Different models, different data, different outputs. | NO |
| Transform / Generate | Yes — Transform = Generate(new from old) | YES — Generate creates from nothing. Transform takes existing input and modifies it. Different signatures. | NO |
| Generate / Transform(mental state) | Yes — both produce newness | Theoretically same but Generate produces external novelty; internal novelty isn't useful as an architectural primitive | Keep as Generate for external output |

**Verdict:** AGE^T is the stopping point. The 4 primitives are theoretically interrelated but practically distinct. Each maps to a different implementable behavior with a different input/output signature. Decomposing further (to "compute" or "process information") removes all architectural structure without adding explanatory power.

---

## 2. Assumptions Still Unverified

### Layer 1: Primitive Assumptions (AGE^T)

| # | Assumption | How to Verify |
|---|-----------|--------------|
| A1 | 4 primitives (AGE^T) are sufficient to model any creative act | Build one workflow through all 4 — see if any step can't be expressed |
| A2 | The primitives compose cleanly — output of one is valid input to another | Build an Attend→Generate cycle, an Evaluate→Transform cycle, a chain of all 4 |
| A3 | The distinction between primitives is meaningful at the agent level | If the same agent can handle Attend and Evaluate without reconfiguration, they're the same thing in practice |

### Layer 2: Composite Function Assumptions (8-Function Layer)

| # | Assumption | How to Verify |
|---|-----------|--------------|
| B1 | The 8 functions can be implemented as compositions of AGE^T | Build Frame = Attend + Generate(constraints). Realize = Generate↔Evaluate↔Transform loop. See if they emerge |
| B2 | Functions are recursive (any can call any) without infinite loops | Test: Realize calls Explore, which calls Evaluate, which calls Realize... does it converge? |
| B3 | Domain-specific variants of functions produce recognizably different behaviors | Build a Realize for 3D assets and a Realize for code. Do they look different? |

### Layer 3: Intent Token Assumptions

| # | Assumption | How to Verify |
|---|-----------|--------------|
| C1 | Structured intent (Intent Token) captures enough information to guide output | Build one Intent Token, feed it to Realize, check if output matches intent better than text prompt alone |
| C2 | Intent fidelity can be measured and tracked across function invocations | After each function call, ask Evaluate to score against Intent. Does the score degrade? Improve? |
| C3 | Intent Token survives handoffs between functions | Chain 3 functions. Check if the final Evaluate references the original Intent or a corrupted version |

### Layer 4: Implementation Assumptions

| # | Assumption | How to Verify |
|---|-----------|--------------|
| D1 | A capability registry can bridge creative functions to tool-specific actions | Register one capability ("generate low-poly mesh"). Bind it to a tool (Blender). Execute. |
| D2 | Function orchestration (recursive, not linear) produces more coherent output than a linear pipeline | Build both. Compare output quality for the same input. |
| D3 | An Evaluate agent can produce usefully accurate quality scores against Intent | Build Evaluate. Have it score 10 outputs against their Intents. Have a human score the same. Compare. |

---

## 3. Which Assumptions Require Implementation vs Research

### Answer Through Research (stop and think)

| Assumption | Why Research First |
|-----------|-------------------|
| A1 — Are 4 primitives sufficient? | Literature review of 10+ creativity models already done (June 15 research). Evidence supports AGE^T as a superset of BVSR (2) and Geneplore (2). Research is sufficient. |
| A3 — Are primitives distinct at agent level? | Agent architecture literature (Brooks subsumption, Minsky society of mind) suggests distinct agents are better than monolithic. Research supports the split. |
| C3 — Can intent survive handoffs? | This IS the telephone game problem. Research confirms it's the critical failure mode. But validation requires building. |

**Research stop condition:** When the answer is "we need to build to find out." Continuing to research instead of building is avoidance.

### Answer Through Building (build to find out)

| Assumption | Smallest Build |
|-----------|---------------|
| B1 — Can 8 functions compose from 4? | One Intent → One Realize (composed of Attend+Generate+Evaluate+Transform) → Output |
| B2 — Does recursion converge? | Same as above. If it goes infinite, you'll know. |
| C1 — Does Intent Token work? | Build the Intent Token schema. Feed it to any capable model. Compare output quality vs raw prompt. |
| D1 — Can capability registry bridge to tools? | Register one capability. Implement it with one tool. Run it. |
| D3 — Can Evaluate score quality? | Build a Evaluate that compares output against Intent. Test on 10 examples. |

**Implementation start condition:** When the next question is "will this work?" and the only way to answer is to build it.

---

## 4. Smallest Experiment That Proves or Disproves the Architecture

### The Core Experiment

**Hypothesis:** An Intent Token + AGE^T primitives produces output that better matches user intent than a direct AI generation (text-to-asset).

**Single workflow, single function (Realize), single output.**

### Experiment Design

```
INPUT: "Weathered medieval sword, battle-worn, leather-wrapped handle, 
        low-poly game-ready, 5,000 triangle budget, warm ambient lighting"
        → Structured as Intent Token

BRANCH A (COS):
  Intent Token → 
    Realize agent (composing Attend+Generate+Evaluate+Transform) →
    Final output

BRANCH B (Baseline):
  Same text → Direct AI generation (Midjourney/Sora/3D gen) →
  Output

COMPARE:
  - Does COS output match Intent better? (Evaluate agent + human judge)
  - Is COS output more editable/modifiable?
  - Is COS output more predictable/controllable?
```

### What Proves the Architecture

- COS output scores >= 20% higher on intent fidelity than direct generation
- COS output is editable (change "leather wrap" → "metal wire wrap" without regenerating everything)
- The Evaluate agent's scores correlate with human judgment (r > 0.7)

### What Disproves the Architecture

- COS output is not better than direct generation
- The Intent Token adds overhead without adding value
- The function abstraction adds complexity without improving output
- Evaluate agent's scores are random or contradictory to human judgment

### Minimum Viable Prototype to Run This Experiment

**Requirements:**
1. Intent Token schema (30 lines of JSON)
2. One Realize agent that calls external models (text-to-3D, text-to-image) internally
3. One Evaluate agent that compares output against Intent Token
4. One integration that chains them

**No need for:**
- All 8 functions (just Realize)
- All 4 primitives separately (they're composed inside Realize)
- Capability registry (hardcode one capability)
- Multiple tools (use one external model)

**This can be built in 5-10 days.**

---

## 5. 30-Day Prototype Plan

### Goal
Build ONE Intent → ONE Function → ONE Output loop. Prove the architecture works for a single use case.

### Scope
**Single domain:** Game-ready 3D asset generation
**Single function:** Realize (composed of AGE^T internally)
**Single evaluation:** Evaluate against Intent Token
**Single output:** glTF/OBJ file + screenshot

### Week 1: Intent Token + Realize Agent
- Build Intent Token schema (domain, subject, mood, style, quality_bar, constraints)
- Build Realize agent skeleton — takes Intent, calls external generation model
- Output: Intent Token parser + Realize calls external API and returns whatever it gets

### Week 2: Realize + Evaluate Loop
- Build Evaluate agent — takes Intent + Output, produces quality scores (intent_fidelity, technical_quality, aesthetic_score)
- Connect Realize → Evaluate cycle
- Output: A system that generates, evaluates against intent, and can flag if quality is low

### Week 3: Controlled Output
- Add Transform sub-primitive inside Realize: re-generate with adjusted parameters based on Evaluate feedback
- Output: System that iterates up to 3 times to improve quality

### Week 4: Baseline Comparison + Demo
- Run Branch A (COS) vs Branch B (direct generation) on 10 test prompts
- Measure: intent fidelity scores, iteration count, user preference
- Record: what works, what breaks, what's missing
- Output: Comparison report + working prototype

### Success Criteria
- [ ] COS output scores higher on intent fidelity than direct generation
- [ ] Evaluate agent scores correlate with human judgment
- [ ] The architecture demonstrably adds value over "just call an AI"
- [ ] Clear list of what to build next (not what to research next)

---

## 6. 90-Day Prototype Plan

### Goal
Two creative functions (Realize + Evaluate + Refine loop). Feedback cycle. Single domain. Measurable improvement over baseline.

### Month 1 (30-day prototype above)
Intent → Realize → Evaluate → Refine → Output

### Month 2: Add Second Function + Handoff

**Add Frame function at the front:**
- User gives rough intent → Frame agent structures it into Intent Token
- Frame agent asks clarifying questions when intent is ambiguous
- Frame agent validates Intent Token before passing to Realize

**Add Explore before Select before Realize:**
- Intent → Explore (generate 3 concept variations) → Select (pick one) → Realize (produce from selection)
- Test whether the Explore→Select→Realize chain produces better output than Realize alone

**Milestone:** 3-function chain (Frame, Realize, Evaluate) working end-to-end.

### Month 3: Recursive Composition + Test Suite

**Build one recursive composition:**
- Realize calls Explore internally
- Prove that recursion converges (doesn't infinite loop)

**Test suite:**
- 20 test intents across 3 domains (game assets, environment, character)
- Automated scoring against human-labeled benchmarks
- Regression tests: does adding a function improve or degrade quality?

**Capability registry v0:**
- Registry with 10 capabilities
- Each capability maps: Function → AGE^T primitives → Tool actions
- Test: can a capability be executed through 3 different tool mappings?

### 90-Day Exit Criteria

- COS prototype demonstrably outperforms direct AI generation for game-ready assets
- Architecture survives 20 test cases without fundamental changes
- Clear migration path from prototype to production
- No remaining "we need to research this" blocks — everything is "we need to build this better"

---

## 7. What Must Be Built Next

### The sequence, in order:

**Day 1-3: Intent Token Schema** — A JSON schema. 30 lines. Zero dependencies. Test it by writing 10 Intent Tokens by hand and seeing if they capture what matters.

**Day 4-10: Realize Agent** — One agent. Takes Intent Token. Calls an external generation model (any model). Returns whatever the model gives you. It doesn't need to be smart yet — just prove the interface works.

**Day 11-15: Evaluate Agent** — Second agent. Takes Intent Token + Output. Produces 3 scores: intent_fidelity (0-1), technical_quality (0-1), aesthetic_score (0-1). Test against 5 human judgments to calibrate.

**Day 16-20: Realize → Evaluate Loop** — Chain them. Generate, evaluate, if score is low, flag for human review. This is the smallest meaningful COS system: one intent, one output, one quality check.

**Day 21-25: Baseline Comparison** — Run 10 intents through COS and through direct generation. Compare. Write the comparison report. This is where you decide: does the architecture add value or not?

**Day 26-30: Demo + Decision** — Working prototype. Decision point: scale or pivot.

### What NOT to build yet

- Don't build all 8 functions (build Realize only)
- Don't build the full capability registry (hardcode 1-2 capabilities)
- Don't build agent-to-agent handoff protocols (chain them in sequence)
- Don't build the tool abstraction layer (one tool is fine)
- Don't build the full Intent persistence system (just save/load from JSON)

---

## 8. The Stopping Point

The rule for when to stop decomposing:

| Level | Stop Here? | Reason |
|-------|-----------|--------|
| 8 functions (v4) | NO — not primitive | Functions are composites, proven by adversarial review |
| 4 primitives (AGE^T) | **YES — good enough for implementation** | Each primitive maps to a different implementable behavior. Further decomposition produces circular definitions. |
| 2 primitives (Generate + Evaluate) | NO — too abstract | BVSR is correct but insufficient for system design. "Generate" alone doesn't distinguish creating from transforming. |
| 1 primitive (Cognition) | NO — useless | Everything is a special case of everything else. No architectural guidance. |

**The test for AGE^T:** Can you implement 4 different agent types, each with a different job description, different success criteria, and different outputs? If yes — and you can — then the decomposition is granular enough to build with.

**Answer:** Yes. An Attend agent, a Generate agent, an Evaluate agent, and a Transform agent would each need different code, different prompts, different metrics, and different interfaces. They are architecturally distinct even if they're cognitively interrelated.

**Decomposition is complete. Start building.**

---

## Summary

| Question | Answer |
|----------|--------|
| Is AGE^T the absolute bottom? | Probably not. But further descent produces circular definitions that are indistinguishable in implementation. |
| What assumptions still need verification? | 12 assumptions across 4 layers. Only 2 require research. 10 require building. |
| Smallest experiment? | Intent → Realize → Evaluate → Output. One workflow. 5-10 days. |
| 30-day prototype? | One Intent→Realize→Evaluate→Refine loop. Game-ready asset domain. Baseline comparison. |
| 90-day prototype? | 3 functions (Frame + Realize + Evaluate). Recursive composition. 20-test suite. Capability registry v0 with 10 entries. |
| What to build next? | Intent Token schema (Day 1-3). Realize agent (Day 4-10). Evaluate agent (Day 11-15). Chain them (Day 16-20). Compare to baseline (Day 21-25). |
| What NOT to build? | All 8 functions, full registry, handoff protocols, tool abstraction, full persistence. Only what's needed to prove or disprove. |
| **The decision:** | **Stop decomposing. Start building.** The next discovery won't come from another document. It will come from running code producing an output that you can judge against an intent. |
