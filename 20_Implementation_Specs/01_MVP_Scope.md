# COS Implementation Specifications — MVP Scope

**Date:** June 15, 2026
**Author:** Chioma (Systems Architect)
**Reference:** [Smallest_Viable_COS_and_First_Workflow.md](../04_Workflows/Smallest_Viable_COS_and_First_Workflow.md) — Storyboard as first workflow

---

## 1. MVP Definition

**The MVP is a working Storyboard Creation system** — the Director provides a script or verbal pitch, and the system produces 5-15 storyboard panels with shot descriptions, camera notes, and timing annotations.

### Why Storyboard First

From Nessa's analysis (Part 2 of Smallest Viable COS):

| Reason | Detail |
|--------|--------|
| **Shortest dependency chain** | 4 capabilities (S02, S01, D01, FIL) vs 8+ for alternatives |
| **Lowest risk** | Storyboards are cheap. A bad board costs nothing to redo. |
| **Exercises the CIL** | The core COS innovation (intent translation) is fully exercised |
| **Unlocks all workflows** | Storyboard → Layout → Environment → Animation/Character → Cinematic Shot |
| **Immediately useful** | Storyboards are a legitimate creative deliverable |
| **Establishes the feedback loop** | Simplest setting to test generate-evaluate-iterate |

**Reference:** [Smallest_Viable_COS.md](../04_Workflows/Smallest_Viable_COS_and_First_Workflow.md) §Part 2 — Options Analysis, Recommendation: Storyboard Creation

### What the MVP Produces

| Element | Specification |
|---------|--------------|
| **Input** | Script text or verbal pitch (natural language) + direction (tone, style references, emotional beats) |
| **Output** | 5-15 storyboard panels per sequence, with shot descriptions, camera notes, and timing annotations |
| **Format** | JSON sequence + folder of generated panel images |
| **Quality criteria** | Silhouette readability, emotional beat clarity, narrative coherence, pacing/rhythm, tonal consistency |
| **Iteration model** | Exploration: 5 options per beat. Refinement: 2-4 iterations per selected option. |
| **Success signal** | Director can assemble a story reel that communicates the full narrative to a third party |

---

## 2. Capabilities for MVP

### 2.1 Agent Roles

From the 8 creative functions [COS_Architecture_v4.md](../01_Capability_Architecture/COS_Architecture_v4_Creativity_First.md) §3.3, the MVP uses these agents:

| Agent | Creative Function | What It Does in MVP |
|-------|------------------|---------------------|
| **Frame Agent** | Framing | Takes user's rough intent → structured Intent Token. Asks clarifying questions. |
| **Explore Agent** | Exploration | Generates 5 panel variations per story beat from the Intent Token |
| **Select Agent** | Selection | Presents options to user, records user's choice |
| **Realize Agent** | Realization | Produces the final storyboard panels for selected option |
| **Evaluate Agent** | Evaluation | Scores output against Intent Token. Provides structured feedback. |

### 2.2 Agent Composition via AGE^T Primitives

Each agent is composed from the 4 AGE^T primitives:

| Agent | Attend | Generate | Evaluate | Transform |
|-------|--------|----------|----------|-----------|
| **Frame** | Parse user input for key elements | Generate structured Intent Token from parsed input | Validate Intent Token completeness | Clarify gaps with user |
| **Explore** | Focus on relevant domain/constraints | Generate N conceptual variations | Score variations against Intent | (not used — exploration is not refinement) |
| **Select** | Present options for user attention | (not used — selection is user's generate) | (not used) | (not used — selection is a handoff point) |
| **Realize** | Focus on selected direction | Generate panel images from brief | Auto-check: does panel match brief? | Adjust generation parameters if match is poor |
| **Evaluate** | Attend to intent criteria | (not used) | Score output against all 5 quality criteria | Produce structured feedback |

**Reference:** [COS_v4_Adversarial_Review.md](../01_Capability_Architecture/COS_v4_Adversarial_Review.md) §6 — 4-Primitive Model composition table

### 2.3 What's Explicitly Excluded from MVP

| Feature | Why Excluded | When Added |
|---------|-------------|------------|
| All 8 functions | Only need Frame + Explore + Select + Realize + Evaluate | Phase 2+ |
| Full Capability Registry | Hardcode capability bindings for storyboard domain | Phase 2 |
| Multi-tool orchestration | Single tool (image generation API) for all panels | Phase 2 |
| Non-linear workflows | Storyboard is linear start→finish | Phase 2+ |
| Auto-approval | All outputs reviewed by Director | Phase 3 |
| Full Braintrust quality system | Single Evaluate agent with structured rubric | Phase 3 |
| Version/persistence database | JSON file storage | Phase 2 |
| Agent-to-agent handoff protocols | Sequential execution via orchestrator | Phase 2 |
| Characters, animation, VFX | Storyboard only | Phase 2-4 |

---

## 3. MVP Flow — High Level

```
User: "Create a storyboard for a fantasy quest opening scene..."

         ↓
[1] Frame Agent
    → Parses user intent
    → Asks clarifying questions ("What tone? Hero or anti-hero?")
    → Produces structured Intent Token
    
         ↓
[2] Explore Agent
    → Reads Intent Token
    → Generates 5 panel variations for each story beat
    
         ↓
[3] Select Agent  
    → Presents 5 panel options to user
    → User selects one direction
    
         ↓
[4] Realize Agent
    → Takes selected direction from Intent Token
    → Generates full storyboard panels (5-15 per sequence)
    
         ↓
[5] Evaluate Agent
    → Scores output against Intent Token
    → Produces quality report (0.0-1.0 per criterion)
    → Director reviews, provides feedback
    
         ↓
    [Iterate 2-4 times: feedback → Realize → Evaluate → approve]
    
         ↓
[6] Output
    → JSON sequence file
    → Panel image files
    → Intent Token with iteration history
```

**Reference:** [Smallest_Viable_COS.md](../04_Workflows/Smallest_Viable_COS_and_First_Workflow.md) §Part 2 — Storyboard MVP Specification

---

## 4. Success Criteria

| # | Criterion | Measure | Target |
|---|-----------|---------|--------|
| SC1 | End-to-end workflow completes | System produces storyboard panels from natural language input | 100% of test cases |
| SC2 | Output is recognizable as a storyboard | Panels communicate narrative sequence to a third party | Human judge assessment |
| SC3 | Iteration loop works | Feedback → adjustment cycle produces meaningful improvement | 2+ iterations per session |
| SC4 | Intent Token adds value | Output matches intent better than raw text prompt alone | +20% intent fidelity vs baseline |
| SC5 | Evaluate scores correlate | AI quality scores vs human judgment | r > 0.7 correlation |
| SC6 | Director can finish in reasonable time | Brief → final approved output | < 30 minutes |

---

*Next document: [02_Data_Models.md](02_Data_Models.md)*
