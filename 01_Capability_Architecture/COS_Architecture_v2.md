# Creative Operating System (COS) — Architecture v2

**Document ID:** COS-01-CA-002
**Version:** 2.0 (Full Research Synthesis)
**Date:** June 14, 2026
**Status:** Complete
**Author:** COS Architecture Agent
**Scope:** System-level architecture — layers, specialists, decision systems, workflows, organizational model, roadmap
**Supersedes:** COS_Architecture_v1.md

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Architectural Principles (Revised)](#2-architectural-principles-revised)
3. [Layer Architecture Overview (Revised 9-Layer Model)](#3-layer-architecture-overview-revised-9-layer-model)
4. [Layer 1: Director Experience Layer (DEL)](#4-layer-1-director-experience-layer-del)
5. [Layer 2: Creative Intent Layer (CIL) — INTENT PRESERVATION](#5-layer-2-creative-intent-layer-cil--intent-preservation)
6. [Layer 3: Pipeline Orchestration Layer (POL) — GRAPH-BASED](#6-layer-3-pipeline-orchestration-layer-pol--graph-based)
7. [Layer 4: Knowledge & Quality Layer (KQL)](#7-layer-4-knowledge--quality-layer-kql)
8. [Layer 5: Asset & Production Management Layer (APML)](#8-layer-5-asset--production-management-layer-apml)
9. [Layer 6: Tool Abstraction Layer (TAL)](#9-layer-6-tool-abstraction-layer-tal)
10. [Layer 7: Feedback & Iteration Layer (FIL) — BRAINTRUST FEEDBACK](#10-layer-7-feedback--iteration-layer-fil--braintrust-feedback)
11. [Layer 8: Approval Layer (APL) — DIRECTOR APPROVAL](#11-layer-8-approval-layer-apl--director-approval)
12. [Layer 9: Competitive Intelligence & Learning Layer (CILL)](#12-layer-9-competitive-intelligence--learning-layer-cill)
13. [23 Specialist Agents Integrated into the Layer Stack](#13-23-specialist-agents-integrated-into-the-layer-stack)
14. [Decision Architecture: Feedback vs. Approval Separation](#14-decision-architecture-feedback-vs-approval-separation)
15. [Braintrust Pattern: Pure Feedback Layer](#15-braintrust-pattern-pure-feedback-layer)
16. [First Workflow: Storyboard Creation — Data Flow Through Architecture](#16-first-workflow-storyboard-creation--data-flow-through-architecture)
17. [MVP Architecture (8 Capabilities) vs. Full Architecture (23 Specialists)](#17-mvp-architecture-8-capabilities-vs-full-architecture-23-specialists)
18. [Hybrid Organizational Model Position Within the Architecture](#18-hybrid-organizational-model-position-within-the-architecture)
19. [Updated Interface Contracts](#19-updated-interface-contracts)
20. [Implementation Roadmap](#20-implementation-roadmap)

---

## 1. Executive Summary

The Creative Operating System (COS) is a **meta-orchestration layer** that sits ABOVE existing creative tools (Blender, Unreal Engine, Houdini, Nuke, Maya, Substance, etc.) to coordinate, guide, and enhance creative production. It does not replace any tool — it provides the intelligence, workflow management, quality evaluation, and feedback infrastructure that currently exists only inside the minds of the most experienced human creative teams.

**What changed from v1 to v2:**

| Dimension | v1 (Initial Draft) | v2 (Full Research Synthesis) |
|-----------|-------------------|-------------------------------|
| **Layer Count** | 7 layers | 9 layers (split FIL into FIL+APL; added CILL) |
| **FIL** | Combined feedback + implied approval | Pure feedback (Braintrust) — explicitly separated from approval |
| **Approval** | Implicit inside DEL | New Layer 8 (APL) — explicit approval authority gate |
| **Competitive Learning** | Not present | New Layer 9 (CILL) — learns from competitive landscape |
| **Specialist Agents** | 47 flat capabilities | 23 structured specialists in 4 tiers, mapped to layers |
| **POL State Machine** | Linear stage progression | Graph-based state machine supporting non-linear transitions |
| **Decision Architecture** | Not integrated | Full integration: feedback vs. approval separation, authority levels, quality gates |
| **Intent Preservation** | Not explicitly addressed | CIL elevated as critical layer — intent fidelity tracked across boundaries |
| **Organizational Model** | Single model assumed | Hybrid model (3 modes) position documented |
| **MVP** | Not defined | Explicit MVP (8 capabilities) vs. Full (23 specialists) documented |
| **First Workflow** | Not defined | Storyboard Creation documented as first workflow with full data flow |
| **Implementation Roadmap** | Not present | Multi-phase roadmap with decision gates |
| **Interface Contracts** | 19 contracts | Updated and expanded contracts reflecting new understanding |

**Architecture summary:** Nine layers organized into four functional stacks:

| Stack | Layers | Function |
|-------|--------|----------|
| **Creative Stack** | Director Experience (1), Creative Intent (2), Approval (8), Braintrust Feedback (7) | Human-COS interaction, intent communication, review cycles, approvals |
| **Orchestration Stack** | Pipeline Orchestration (3), Asset & Production Management (5) | Workflow coordination, state management, asset lifecycle |
| **Infrastructure Stack** | Knowledge & Quality (4), Tool Abstraction (6) | Domain expertise, quality signals, tool adapters |
| **Learning Stack** | Competitive Intelligence & Learning (9) | Cross-project learning, competitive analysis, tool evolution tracking |

---

## 2. Architectural Principles (Revised)

Updated from v1 based on the Architecture-Changing Discoveries research:

| # | Principle | Source | Revision from v1 |
|---|-----------|--------|------------------|
| 1 | **Invisible by design** — The measure of a good pipeline is how little the artist thinks about it | TDs, Pixar | Unchanged |
| 2 | **Feedback separated from authority** — The most candid feedback comes from people with no power to mandate changes | Pixar Braintrust | **ELEVATED** — now enforced by splitting FIL into two layers (FIL + APL) |
| 3 | **Enforce via automation, not documentation** — If a rule can be broken, it will be | TDs, ILM | Unchanged |
| 4 | **Protect creative intent above generated artifacts** — Intent preservation is the highest priority | ILM, TDs, v2 research | **STRENGTHENED** — intent fidelity tracked at every layer boundary |
| 5 | **Ship 80%, iterate live** — Perfect infrastructure designed in isolation will fail under real pressure | TDs, game studios | Unchanged |
| 6 | **Separate exploration from refinement** — Never refine before you've explored enough | Story/concept artists | Unchanged |
| 7 | **Loop, not line** — Production pipelines are fundamentally iterative, not sequential | VFX, games, Pixar | **STRENGTHENED** — POL is now graph-based, not linear stage machine |
| 8 | **Design for failure** — Assume network drops, disk failures, and software crashes | TDs | Unchanged |
| 9 | **Constraints are creative fuel** — The most creative work often comes from the tightest constraints | Story/concept, directors | Unchanged |
| 10 | **Platform-independent core** — The COS sits above all existing tools as an orchestration layer | Core requirement | Unchanged |
| 11 | **NEW: Intent fidelity degrades at layer boundaries** — Each translation layer must validate against persistent creative intent | v2 research: Architecture-Changing Discoveries (B5) | **NEW** — Intent loss is the real production killer |
| 12 | **NEW: Learn from everything** — The system must learn from competitive tools, postmortems, and cross-project patterns | v2 research: Competitive Landscape, CILL layer | **NEW** — Continuous learning is architectural |
| 13 | **NEW: The Braintrust model requires human expertise to start** — Automated feedback depends on learned credibility | v2 research: Architecture-Changing Discoveries (Finding 4) | **NEW** — Human-in-the-loop Braintrust first, automated FIL later |

---

## 3. Layer Architecture Overview (Revised 9-Layer Model)

### 3.1 Key Changes from v1 to v2

1. **Layer 7 (FIL) is now PURE FEEDBACK** — It no longer carries any implied approval authority. It is the Braintrust layer: it evaluates, recommends, and tracks — but NEVER approves.
2. **New Layer 8: Approval Layer (APL)** — Explicitly separates approval authority from both feedback (FIL) and director interaction (DEL). The Director exercises approval through this dedicated layer.
3. **New Layer 9: Competitive Intelligence & Learning Layer (CILL)** — A horizontal learning layer that monitors competitive tools, captures postmortem knowledge, and enables cross-project pattern recognition.
4. **POL (Layer 3) is now GRAPH-BASED** — Supports non-linear transitions between any two pipeline states, not just linear progression.
5. **CIL (Layer 2) elevated** — Now includes explicit intent preservation tracking across layer boundaries (Architecture-Changing Discoveries B5).

### 3.2 Layer Architecture Diagram

```
+---------------------------------------------------------------------+
|                        CREATIVE STACK                                |
|                                                                      |
|  +---------------------------+  +--------------------------------+  |
|  | Layer 1: Director         |  | Layer 8: Approval              |  |
|  | Experience Layer (DEL)    |  | Layer (APL)                    |  |
|  | - Communicate intent      |  | - Gate sign-offs               |  |
|  | - Review output           |  | - Final approvals              |  |
|  | - Configure system        |  | - Shot finalling               |  |
|  | - Observe status          |  | - Conditional approvals        |  |
|  +---------------------------+  +--------------------------------+  |
|                                                                      |
|  +---------------------------------------------------------------+  |
|  | Layer 7: Feedback & Iteration Layer (FIL) — PURE BRAINTRUST   |  |
|  | - Evaluate quality (no authority)                              |  |
|  | - Identify problems (not solutions)                            |  |
|  | - Track iterations                                             |  |
|  | - Surface feedback trends                                       |  |
|  | - RECOMMENDS but NEVER approves                                |  |
|  +---------------------------------------------------------------+  |
|                                                                      |
|  +---------------------------------------------------------------+  |
|  | Layer 2: Creative Intent Layer (CIL) — INTENT PRESERVATION    |  |
|  | - Intent decomposition (with fidelity tracking)                 |  |
|  | - Brief generation                                              |  |
|  | - Exploration/refinement modes                                  |  |
|  | - Constraint management                                         |  |
|  +---------------------------------------------------------------+  |
+---------------------------------------------------------------------+
                              |
                              v
+---------------------------------------------------------------------+
|                      ORCHESTRATION STACK                             |
|                                                                      |
|  +---------------------------------------------------------------+  |
|  | Layer 3: Pipeline Orchestration Layer (POL) — GRAPH-BASED     |  |
|  | - Graph-based workflow state machine (non-linear)               |  |
|  | - Stage transitions (any-to-any)                                |  |
|  | - Dependency resolution                                         |  |
|  | - Resource allocation                                           |  |
|  | - Quality gate triggering                                       |  |
|  +---------------------------------------------------------------+  |
|                                                                      |
|  +---------------------------------------------------------------+  |
|  | Layer 5: Asset & Production Management Layer (APML)            |  |
|  | - Asset versioning                                              |  |
|  | - Dependency graphs                                             |  |
|  | - Metadata management                                           |  |
|  | - Publishing/validation                                         |  |
|  | - Non-destructive layering (USD model)                          |  |
|  +---------------------------------------------------------------+  |
+---------------------------------------------------------------------+
                              |
                              v
+---------------------------------------------------------------------+
|                     INFRASTRUCTURE STACK                             |
|                                                                      |
|  +---------------------------------------------------------------+  |
|  | Layer 4: Knowledge & Quality Layer (KQL)                       |  |
|  | - Domain expertise encodings                                   |  |
|  | - Quality heuristics (empirically validated)                   |  |
|  | - Style guides / design principles                             |  |
|  | - Cost-of-change models                                        |  |
|  | - Postmortem knowledge                                         |  |
|  +---------------------------------------------------------------+  |
|                                                                      |
|  +---------------------------------------------------------------+  |
|  | Layer 6: Tool Abstraction Layer (TAL)                          |  |
|  | - Tool adapters (Blender, Unreal, Houdini, Nuke, Maya, etc.)  |  |
|  | - Cross-DCC format translation                                 |  |
|  | - Command routing                                              |  |
|  | - Tool capability registry                                     |  |
|  | - Execution environment management                             |  |
|  +---------------------------------------------------------------+  |
+---------------------------------------------------------------------+
                              |
                              v
+---------------------------------------------------------------------+
|                       LEARNING STACK                                |
|                                                                      |
|  +---------------------------------------------------------------+  |
|  | Layer 9: Competitive Intelligence & Learning Layer (CILL)      |  |
|  | - Competitive landscape monitoring                             |  |
|  | - Cross-project pattern recognition                            |  |
|  | - Postmortem knowledge accumulation                            |  |
|  | - Tool evolution tracking                                       |  |
|  | - Quality heuristic refinement (what can we learn from others?) |  |
|  +---------------------------------------------------------------+  |
+---------------------------------------------------------------------+
                              |
                              v
              +-------------------------------+
              | EXISTING TOOLS & ENGINES       |
              | Blender | Unreal | Houdini     |
              | Nuke    | Maya   | Substance   |
              | RenderMan | USD | ...          |
              +-------------------------------+
```

### 3.3 Layer Summary Table

| # | Layer | Abbreviation | Primary Function | Analogy | v1→v2 Change |
|---|-------|-------------|-----------------|---------|-------------|
| 1 | Director Experience Layer | DEL | Human-COS interaction | Director's chair — communicate, review | Unchanged |
| 2 | Creative Intent Layer | CIL | Intent-to-brief translation + intent preservation | Story/concept artist + intent guardian | **ELEVATED** — intent fidelity tracked |
| 3 | Pipeline Orchestration Layer | POL | Graph-based workflow coordination | Production manager with non-linear routing | **GRAPH-BASED** — linear→non-linear |
| 4 | Knowledge & Quality Layer | KQL | Domain expertise + quality heuristics | Pixar Braintrust wisdom + TD knowledge | Unchanged (heuristics need validation) |
| 5 | Asset & Production Management Layer | APML | Asset lifecycle | USD + ShotGrid — version, track, publish | Unchanged |
| 6 | Tool Abstraction Layer | TAL | Tool integration | Pipeline TD — adapters, translation, execution | Unchanged |
| 7 | Feedback & Iteration Layer | FIL | Pure Braintrust feedback | Braintrust — evaluates, recommends, NEVER approves | **SPLIT** — FIL is now pure feedback |
| 8 | Approval Layer | APL | Director approval authority | Director as gate — approves, rejects, conditional | **NEW** — separated from DEL and FIL |
| 9 | Competitive Intelligence & Learning Layer | CILL | Cross-project learning, competitive monitoring | Studio R&D + competitive analysis | **NEW** |

---

## 4. Layer 1: Director Experience Layer (DEL)

### 4.1 Responsibility

The Director Experience Layer is the **primary interface through which human users interact with the COS**. It provides a director-centric UX that supports:
- Communicating creative intent (vision, tone, emotional goals)
- Reviewing work produced by the system (assets, sequences, renders)
- Giving structured and unstructured feedback (routed to FIL)
- Making approval decisions (standard gates — routed to APL)
- Configuring production parameters (scope, schedule, quality targets)
- Observing production status and progress

**v2 change:** Feedback is routed to Layer 7 (FIL) for pure Braintrust processing. Approval decisions are routed to Layer 8 (APL) for explicit gate management. The DEL is the routing nexus but no longer conflates feedback with approval.

### 4.2 Inputs Received

| Input Type | Source | Description |
|-----------|--------|-------------|
| Creative Vision | Human director | Look books, tone packets, verbal/recorded direction, reference collections, mood boards |
| Feedback & Notes | Human director | Verbal notes, markup, structured critiques, approval/rejection signals |
| Approval Decisions | Human director | Gate sign-offs, shot finals, milestone approvals |
| Quality Reports | Layer 7 (FIL) | Evaluations from Braintrust (non-binding) |
| Status Reports | Layer 3 (POL) | Progress summaries, bottleneck alerts, schedule status |
| Configuration | Human director | Project parameters, quality targets, priority assignments |
| Competitive Insights | Layer 9 (CILL) | Learning from other tools, best practices |

### 4.3 Outputs Produced

| Output Type | Destination | Description |
|------------|-------------|-------------|
| Structured Briefs | Layer 2 (CIL) | Formalized creative briefs with constraints, goals, references |
| Feedback Records | Layer 7 (FIL) | Categorized notes for Braintrust processing |
| Approval Events | Layer 8 (APL) | Gate transitions, shot status changes, milestone completions |
| Configuration State | All layers | Production parameters, quality thresholds, tool preferences |
| Status Requests | Layer 3 (POL), Layer 5 (APML) | Progress queries, bottleneck reports, dependency checks |

### 4.4 Interface Contract

```yaml
layer: Director Experience Layer
input_contracts:
  - id: DEL-VISION
    type: Creative Vision Communication
    modalities: [look_books, tone_packets, verbal_direction, reference_collections, mood_boards, multi_modal]
    structural_rules:
      - "Must include emotional/aesthetic intent"
      - "May include specific constraints (must-haves)"
      - "May include open areas (creative freedom)"
    validation: "Vision must be evaluable — someone should be able to determine if output matches intent"
  - id: DEL-FEEDBACK
    type: Creative Feedback
    categories: [structural, surface, intent_clarification, comparative]
    routing:
      structural: Layer 7 (FIL) — triggers mode change evaluation
      surface: Layer 7 (FIL) — applied within current mode
      intent_clarification: Layer 2 (CIL) — returns for intent refinement
      comparative: Layer 7 (FIL) — influences interpretation weighting
    structural_rules:
      - "Structural feedback triggers re-entry into exploration mode in Layer 2"
      - "Surface feedback applies within current refinement mode"
      - "All feedback is non-binding — FIL evaluates, APL approves"
    validation: "Feedback must be traceable to specific entities (shot, asset, sequence)"
  - id: DEL-APPROVAL
    type: Creative Approval
    routing: Layer 8 (APL) — explicit approval gate
    modes: [standard_approval, override, conditional, delegation]
    structural_rules:
      - "Approval/rejection signals are authoritative for Layer 3 state transitions"
      - "Overrides are logged with rationale"
      - "Delegation is revocable at any time"
output_contracts:
  - id: DEL-BRIEF
    destination: Layer 2 (CIL)
    schema:
      creative_goal: string
      constraints: [Constraint]
      references: [Reference]
      quality_criteria: [Criterion]
      open_areas: [string]
      intent_fidelity_token: string  # NEW: tracks intent preservation
    validation: "Brief must contain at least one evaluable quality criterion"
  - id: DEL-APPROVAL
    destination: Layer 8 (APL)
    schema:
      entity_id: string
      entity_type: [shot, asset, milestone, gate]
      decision: [approved, rejected, revise, conditionally_approved]
      conditions: [string]
      override_rationale: string
    validation: "Approval decisions must be idempotent"
```

---

## 5. Layer 2: Creative Intent Layer (CIL) — INTENT PRESERVATION

### 5.1 Responsibility

The Creative Intent Layer is the **translation engine of the COS** — and now also the **intent preservation guardian**. It takes high-level, often ambiguous creative direction from the Director Experience Layer and decomposes it into structured, actionable production requirements.

**v2 elevation:** Based on Architecture-Changing Discoveries finding B5 — "The most critical bottleneck is not DigitalModeler but intent translation" — the CIL now includes explicit intent fidelity tracking. Every brief carries an `intent_fidelity_token` that downstream layers validate against. The CIL monitors how much creative intent is lost at each layer boundary.

Key responsibilities:
- **Intent decomposition:** Break "I want this scene to feel epic" into specific, evaluable criteria
- **Intent fidelity tracking:** Every output is validated against the original intent. Fidelity scores are tracked.
- **Brief formalization:** Convert director communication into structured briefs that downstream layers can act on
- **Exploration vs. refinement mode management:** Support divergent thinking (generate many options) and convergent thinking (narrow and polish) as distinct modes
- **Constraint extraction:** Identify hard constraints (must-haves), soft constraints (preferences), and open areas (creative freedom)
- **Generate-evaluate cycles:** Produce multiple interpretations/variations for review before committing to a direction
- **Strategic sacrifice identification:** When constraints conflict, identify which elements can be compromised
- **IKIWISI support:** When the director cannot articulate quality criteria upfront ("I'll Know It When I See It"), infer criteria from exploration feedback

### 5.2 Inputs Received

| Input Type | Source | Description |
|-----------|--------|-------------|
| Creative Vision | Layer 1 (DEL) | High-level aesthetic/emotional intent |
| Structured Briefs | Layer 1 (DEL) | Already-structured creative direction |
| Feedback Responses | Layer 7 (FIL) | Evaluations of generated interpretations (non-binding) |
| Context Knowledge | Layer 4 (KQL) | Domain expertise, style guides, quality signals |
| Asset Context | Layer 5 (APML) | Existing assets, reference materials, production history |
| Competitive Benchmarks | Layer 9 (CILL) | Best practices and patterns from competitive tools |

### 5.3 Outputs Produced

| Output Type | Destination | Description |
|------------|-------------|-------------|
| Formal Creative Briefs | Layer 3 (POL) | Structured brief with goals, constraints, quality criteria, references (with intent_fidelity_token) |
| Interpretation Variations | Layer 7 (FIL) | Multiple candidate interpretations for Braintrust evaluation |
| Constraint Specifications | Layer 3 (POL), Layer 4 (KQL) | Hard/soft constraints tagged to entities |
| Exploration Commands | Layer 3 (POL) | "Generate N variations of X within constraints Y" |
| Refinement Commands | Layer 3 (POL) | "Polish selected variation X toward quality criteria Y" |
| Intent Fidelity Reports | Layer 1 (DEL), Layer 4 (KQL) | Tracking of how much original intent survived translation |

### 5.4 Interface Contract

```yaml
layer: Creative Intent Layer
core_principle: "Intent fidelity is preserved across every layer boundary"
input_contracts:
  - id: CIL-VISION
    source: Layer 1 (DEL)
    type: Creative Intent
    processing: "Decompose into concrete, evaluable criteria"
    intent_fidelity:
      - "Generate intent_fidelity_token from original brief"
      - "Track cumulative fidelity score through all processing"
      - "Flag if fidelity drops below 0.8 threshold"
    output_modes: [exploration, refinement]
    mode_rules:
      exploration:
        - "Generate field of minimum N=5 initial interpretations"
        - "Treat all outputs as cheap — no commitment to any single direction"
        - "Deliberately include boundary cases to define design space edges"
      refinement:
        - "Accept narrowed direction from FIL"
        - "Apply constraints strictly within selected direction"
        - "Escalate if structural changes are needed (switch back to exploration)"
    ikiwisi_handling:
      - "If Director provides no explicit quality criteria, default to exploration mode"
      - "Infer criteria from Director's selection patterns in exploration feedback"
      - "Generate comparative evaluations ('which of these works better?') not absolute scores"
output_contracts:
  - id: CIL-BRIEF
    destination: Layer 3 (POL)
    schema:
      brief_id: string
      project_id: string
      creative_goal: string
      intent_fidelity_token: string  # Links back to original DEL brief
      domain: [animation, vfx, game_dev, composite, simulation, design]
      mode: [exploration, refinement]
      constraints:
        hard: [Constraint]
        soft: [Constraint]
        open_areas: [string]
      quality_criteria:
        required: [Criterion]
        aspirational: [Criterion]
      references:
        primary: [Reference]
        context: [Reference]
      cost_of_change_priority: number  # 1 = cheap to change now, 5 = very expensive
      specialist_requirements: [SpecialistID]  # Which specialists are needed
    validation:
      - "At least one required quality criterion must be evaluable by Layer 4"
      - "Hard constraints must be verifiable by Layer 6"
      - "intent_fidelity_token must match original DEL brief"
```

---

## 6. Layer 3: Pipeline Orchestration Layer (POL) — GRAPH-BASED

### 6.1 Responsibility

The Pipeline Orchestration Layer is the **central nervous system of the COS**. It manages the production workflow state machine, coordinates stage transitions, resolves dependencies, allocates resources, and enforces quality gates.

**v2 change:** The POL is now a **graph-based state machine** rather than a linear stage progression model. This supports non-linear creation paths, skipping stages, returning to earlier stages, and parallel execution branches. Based on Architecture-Changing Discoveries finding that "the pipeline metaphor is questioned before implementation begins" — every studio research document describes "loops not lines."

Key responsibilities:
- **Graph-based workflow state machine:** Maintain authoritative production state as a directed graph. Entities can transition between any two nodes.
- **Non-linear stage transitions:** Support progression, regression, skipping, and branching between any stages
- **Gate management:** Enforce milestone gates (concept approved, vertical slice complete, alpha, beta, final)
- **Dependency resolution:** Track and resolve inter-stage and inter-asset dependencies
- **Resource allocation:** Manage computational and attention resources across active work items
- **Revision loop handling:** Support bidirectional data flow — upstream changes must propagate downstream
- **Pipeline configuration:** Adapt the pipeline graph to project type (film, game, VFX, TV)
- **Subgraph instantiation:** For the Capability Network mode (Model B), instantiate subgraphs of specialists based on brief requirements

### 6.2 Inputs Received

| Input Type | Source | Description |
|-----------|--------|-------------|
| Creative Briefs | Layer 2 (CIL) | Formalized intent with specialist requirements |
| Approval Events | Layer 8 (APL) | Gate sign-offs, shot approvals |
| Asset Events | Layer 5 (APML) | Publish notifications, version updates |
| Quality Signals | Layer 4 (KQL) | Quality evaluations, "good enough" signals |
| Feedback Events | Layer 7 (FIL) | Iteration completion signals (non-binding recommendations) |
| Resource Status | Layer 6 (TAL) | Tool availability, compute capacity, adapter health |
| Learning Signals | Layer 9 (CILL) | Cross-project pattern recommendations |

### 6.3 Outputs Produced

| Output Type | Destination | Description |
|------------|-------------|-------------|
| Stage Commands | Layer 5 (APML), Layer 6 (TAL) | "Execute brief X in tool Y with parameters Z" |
| State Transitions | Layer 1 (DEL), Layer 7 (FIL) | Entity state change events |
| Dependency Events | Layer 5 (APML) | Dependency tracking updates, upstream change flags |
| Gate Events | Layer 1 (DEL), Layer 8 (APL) | Milestone reached/pending/blocked |
| Resource Requests | Layer 6 (TAL) | Compute allocation, tool instances, execution capacity |
| Status Reports | Layer 1 (DEL) | Progress summaries, bottleneck alerts, schedule status |

### 6.4 Interface Contract

```yaml
layer: Pipeline Orchestration Layer
architecture: graph_based  # v2 change from linear stage machine
state_machine:
  model: directed_graph
  entities: [project, sequence, shot, asset, task]
  states: [created, in_progress, pending_review, approved, rejected, revising, complete, blocked, stale]
  transitions:
    - type: any_to_any  # Non-linear transitions supported
      rules:
        - "All transitions from pending_review require FIL recommendation + APL approval"
        - "Structural feedback transitions: any state -> revising -> in_progress"
        - "Skip transitions allowed when: Director override + risk assessment"
        - "Branch transitions: single entity can fork into parallel workstreams"
    - subgraph:
        description: "For Model B (Capability Network), instantiate subgraphs dynamically"
        trigger: "Brief type + domain requirements"
        instantiation:
          - "Select nodes matching specialist_requirements from brief"
          - "Wire dependency edges based on capability dependency map"
          - "Activate quality gates at predefined checkpoints"
          - "Route feedback loops back to appropriate upstream nodes"
phase_model:
  # Configurable per project type
  pre_production:
    rules:
      - "Gate: Concept Approval required to enter Production"
      - "Vertical slice required before full production begins"
      - "Exploration mode is default in Layers 2 and 7"
  production:
    rules:
      - "Gate: Production Readiness required to enter Production"
      - "Ship 80% solutions, iterate live"
      - "Non-linear transitions enabled — can return to earlier stages"
  post_production:
    rules:
      - "Gate: Feature Complete required to enter Post-Production"
      - "Surface feedback only — structural changes require Director override"
      - "Tool chain is locked at Alpha gate"
```

---

## 7. Layer 4: Knowledge & Quality Layer (KQL)

### 7.1 Responsibility

The Knowledge & Quality Layer is the **persistent expertise layer** of the COS. It encodes domain knowledge, quality heuristics, design principles, and evaluative criteria. This layer is the COS's equivalent of Pixar's Braintrust wisdom, the TD's technical knowledge, and the director's aesthetic judgment — made persistent and queryable.

**v2 change:** Quality heuristics are now acknowledged as requiring empirical validation before full implementation (Architecture-Changing Discoveries Finding 5). A "quality signal validation sprint" is part of the roadmap. The layer also now receives continuous input from Layer 9 (CILL) for refining quality heuristics based on competitive analysis.

Key responsibilities:
- **Domain expertise encoding:** Store and serve knowledge about creative domains
- **Quality heuristics:** Provide evaluative criteria — validated against human expert ratings
- **Style guides:** Maintain persistent design language, color philosophy, shape language, and world-building rules per project
- **Cost-of-change models:** Provide economic models for changes at different pipeline stages
- **Postmortem knowledge:** Accumulate lessons learned from completed projects
- **Constraint validation:** Evaluate whether proposed work adheres to project and domain constraints
- **Reference library:** Store and index visual, technical, and conceptual references
- **Quality heuristic refinement:** Continuously improve heuristics based on FIL feedback patterns

---

## 8. Layer 5: Asset & Production Management Layer (APML)

(Unchanged from v1 — except now with explicit integration to Layer 9 CILL for cross-project asset pattern learning.)

The APML remains the **persistent data spine** of the COS, managing the entire lifecycle of creative assets.

---

## 9. Layer 6: Tool Abstraction Layer (TAL)

(Unchanged from v1 — the TAL adapter model is sound. The Build vs. Buy vs. Hack framework is preserved.)

Key addition for v2: The TAL now also reports tool capability gaps to Layer 9 (CILL), which monitors the competitive landscape for emerging tools that could fill those gaps.

---

## 10. Layer 7: Feedback & Iteration Layer (FIL) — BRAINTRUST FEEDBACK

### 10.1 Responsibility — PURIFIED TO PURE BRAINTRUST

The Feedback & Iteration Layer is the **Braintrust-inspired pure feedback engine** of the COS. It evaluates, recommends, identifies problems, and tracks iterations — but it **NEVER approves**. Approval authority is cleanly separated into Layer 8 (APL).

**v2 change:** In v1, FIL combined feedback with implied quality gate authority. Now FIL is PURE FEEDBACK — zero decision authority. This enforces the Braintrust pattern architecturally: the layer that evaluates quality cannot also control gates.

This is the most important architectural change in v2. It directly implements the core insight from Creative_Roles_as_Functions.md: "The Braintrust is a FEEDBACK function that is architecturally SEPARATE from the APPROVAL function."

Key responsibilities:
- **Pure feedback collection:** Accept feedback from multiple sources (director, automated quality evaluations, domain knowledge, comparative analysis)
- **Feedback categorization:** Distinguish structural feedback (requires returning to exploration) from surface feedback (applies within current refinement)
- **Problem identification, not solution prescription:** Identify WHAT is wrong, not HOW to fix it (Braintrust rule)
- **Iteration tracking:** Maintain iteration history for every entity
- **Feedback trend analysis:** Surface patterns in feedback data to KQL for learning
- **Dailies rhythm management:** Manage regular review cadence
- **Note management:** Track notes through resolution
- **Plussing protocol enforcement:** All critique follows the plussing structure (what works → what's wrong → why it matters → direction → encouragement)
- **Confidence scoring:** Each feedback item has a calibrated confidence score

### 10.2 Core Principle

> **The FIL evaluates and recommends. It does NOT decide.**
> **Feedback flows UP to the Director. Decisions flow DOWN from the Director.**
> **The feedback layer NEVER sends commands directly to the pipeline layer — only recommendations that the Director has approved (or that fall within delegated authority).**

### 10.3 Inputs Received

| Input Type | Source | Description |
|-----------|--------|-------------|
| Director Feedback | Layer 1 (DEL) | Structured notes, markup, verbal feedback (non-binding) |
| Quality Evaluations | Layer 4 (KQL) | Automated quality scores, heuristic evaluations |
| Asset Versions | Layer 5 (APML) | Work submitted for Braintrust evaluation |
| State Transitions | Layer 3 (POL) | Entity status changes that trigger review cadence |
| Feedback History | Layer 5 (APML) | Past feedback records for context |
| Iteration Limits | Layer 1 (DEL) | Max iteration counts, schedule constraints |
| Competitive Benchmarks | Layer 9 (CILL) | Comparative quality data from other tools/systems |

### 10.4 Outputs Produced

| Output Type | Destination | Description |
|------------|-------------|-------------|
| Structured Feedback | Layer 2 (CIL), Layer 1 (DEL) | Categorized notes with confidence scores. NON-BINDING. |
| Iteration Recommendations | Layer 3 (POL) | "Revise", "Proceed to next stage", "Return to exploration" — RECOMMENDATIONS only |
| Quality Scores | Layer 1 (DEL) | Dashboard data for director awareness |
| Iteration History | Layer 5 (APML) | Complete feedback-to-change traceability |
| "Done" Recommendations | Layer 8 (APL) | "Good enough" evaluation — APL makes the binding decision |
| Feedback Trend Analysis | Layer 4 (KQL) | Patterns in feedback data for heuristic refinement |

### 10.5 Interface Contract

```yaml
layer: Feedback & Iteration Layer
core_principle: "PURE BRAINTRUST — FIL evaluates and recommends, APL approves"
zero_authority_rule: "FIL MUST NOT own any gate, approval, or state transition decision"
feedback_types:
  - id: structural
    description: "Changes that require returning to exploration mode"
    effect: "TRIGGERS Layer 2 mode switch recommendation to exploration"
    cost_multiplier: "3-5x if late stage"
    confidence_required: "Must be STRONG_SIGNAL or higher"
  - id: surface
    description: "Changes that apply within current refinement mode"
    effect: "Applies within current refinement pass"
    cost_multiplier: "1x (stage-appropriate)"
  - id: intent_clarification
    description: "Creative direction needs refinement"
    effect: "Returns to Layer 2 for intent refinement"
  - id: comparative
    description: "Comparison against reference or alternatives"
    effect: "Influences interpretation weighting — does not trigger mode change alone"
plussing_protocol:
  steps:
    1: "Start with what works"
    2: "State the problem"
    3: "Explain why it matters"
    4: "Suggest a direction (not a solution)"
    5: "End on encouragement"
  prohibited:
    - "Saying 'this is bad' without constructive framing"
    - "Attacking the Director's judgment"
    - "Offering a single mandated solution"
    - "Framing feedback as final verdict"
review_rhythm:
  default: "Regular dailies — review at cadence, not just on submission"
  cadence_rules:
    pre_production: "Daily standup + weekly structured review"
    production: "Daily dailies + weekly milestone review"
    post_production: "Alternate-day reviews + milestone signoffs"
iteration_contract:
  max_iterations_before_escalation: number  # configurable per project
  escalation_path:
    - "FIL recommends escalation to DEL"
    - "DEL determines: continue iterating, change approach, or accept current state"
  iteration_tracking:
    required_fields:
      - entity_id
      - iteration_number
      - feedback_items: [feedback_id, category, source, summary, confidence]
      - changes_made: [change_description]
      - decision_recommendation: [continue, structural_restart, approve, abandon]
output_contracts:
  - id: FIL-FEEDBACK
    destination: Layer 2 (CIL), Layer 1 (DEL)
    disclaimer: "This is a BRAINTRUST RECOMMENDATION. It has NO approval authority."
    schema:
      entity_id: string
      feedback_items:
        - id: string
          category: [structural, surface, intent_clarification, comparative]
          source: [human_director, automated_quality, domain_knowledge, comparative_analysis]
          summary: string
          confidence: [STRONG_SIGNAL, PLAUSIBLE, MINOR_NOTE, UNSURE]
          plussing_formatted: string
          action_items: [string]
          priority: [critical, high, medium, low]
      recommendation: [revise, proceed, return_to_exploration, escalate]
      recommendation_confidence: number
    validation: "ALL output must include 'RECOMMENDATION — NOT APPROVAL' header"
```

---

## 11. Layer 8: Approval Layer (APL) — DIRECTOR APPROVAL

### 11.1 Responsibility — NEW LAYER

The Approval Layer is the **dedicated approval authority gate** of the COS. It receives approval decisions from the Director (via DEL) and translates them into binding state transition commands for the POL.

**Why a separate layer?** In v1, approval was conflated with both feedback (FIL) and director interaction (DEL). By making approval a separate architectural layer, we enforce the Braintrust separation at the structural level:
- FIL (Layer 7) evaluates and recommends — zero authority
- APL (Layer 8) approves and gates — full authority
- DEL (Layer 1) provides the human interface for both

This mirrors the real-world separation: the Braintrust advises, the Director decides, the pipeline executes.

Key responsibilities:
- **Gate management:** Enforce approval gates for state transitions
- **Authority level enforcement:** Map decisions to the correct authority level (L1-L5)
- **Override tracking:** Log all Director overrides with rationale and risk assessment
- **Auto-approval management:** Execute delegated authority within defined guardrails
- **Escalation routing:** When decisions exceed current authority level, escalate appropriately
- **Conflict resolution:** When feedback sources disagree, present structured tradeoffs to Director

### 11.2 Decision Authority Levels

| Level | Name | Description |
|-------|------|-------------|
| L5 | Director Must Decide | System cannot proceed without Director input. Irreversible decisions, final approvals. |
| L4 | Director Must Confirm | System recommends a course of action. Director must explicitly confirm or redirect. |
| L3 | Director Delegated | System decides within guardrails. Director notified and can override within review window. |
| L2 | System Decides, Director Can Review | System acts autonomously. Decision logged for review. Director can undo. |
| L1 | System Decides | Negligible decisions, routine maintenance, optimization within approved parameters. |

### 11.3 Inputs Received

| Input Type | Source | Description |
|-----------|--------|-------------|
| Approval Decisions | Layer 1 (DEL) | Director's approval/rejection/conditional signals |
| Quality Evaluations | Layer 7 (FIL) | Non-binding Braintrust recommendations (for awareness) |
| Quality Scores | Layer 4 (KQL) | Automated quality assessments (advisory) |
| State Transition Requests | Layer 3 (POL) | Requests to advance, hold, or return entities |
| Auto-Approval Configuration | Layer 1 (DEL) | Delegation guardrails from Director |
| Escalation Requests | Layer 3 (POL), Layer 7 (FIL) | Decisions exceeding current authority level |

### 11.4 Outputs Produced

| Output Type | Destination | Description |
|------------|-------------|-------------|
| Binding Approvals | Layer 3 (POL) | Authoritative state transition commands |
| Override Records | Layer 5 (APML) | Logged overrides with rationale and risk assessment |
| Delegation Config | Layer 3 (POL) | Auto-approval guardrails for delegated decisions |
| Escalation Responses | Layer 3 (POL), Layer 7 (FIL) | Resolved decisions from higher authority |

### 11.5 Interface Contract

```yaml
layer: Approval Layer
core_principle: "APL has ALL approval authority. FIL has ZERO. This separation is architecturally enforced."
decision_authority_levels:
  L5:
    name: Director Must Decide
    description: "System cannot proceed without Director input"
    applies_to:
      - "Irreversible decisions"
      - "New creative direction"
      - "Scope changes"
      - "Final approvals"
      - "Gate bypass overrides"
  L4:
    name: Director Must Confirm
    description: "System recommends, Director must confirm or redirect"
    applies_to:
      - "High-impact decisions"
      - "First-time decisions in a domain"
      - "Quality disputes"
  L3:
    name: Director Delegated
    description: "System decides within guardrails. Director notified."
    applies_to:
      - "Routine but meaningful decisions within established patterns"
      - "Intermediate stage transitions"
    guardrails:
      - "Must not alter creative intent"
      - "Director notified within 24h review window"
  L2:
    name: System Decides, Director Can Review
    description: "System acts autonomously. Director can undo."
    applies_to:
      - "Standard execution decisions"
      - "Low-impact tactical choices"
  L1:
    name: System Decides
    description: "System acts autonomously. No review needed."
    applies_to:
      - "Negligible decisions"
      - "Routine maintenance"
      - "Optimization within approved parameters"
gate_authority_matrix:
  concept_approval:
    gatekeeper: L5 (Director)
    auto_approval: Never
  exploration_complete:
    gatekeeper: L4 (Director Delegated)
    auto_approval: "If N>=5 and KQL confidence >= 0.8"
  refinement_complete:
    gatekeeper: L3/L4
    auto_approval: "If KQL good_enough + diminishing returns"
  vertical_slice:
    gatekeeper: L5 (Director)
    auto_approval: Never
  production_readiness:
    gatekeeper: L4 (Director)
    auto_approval: Never
  stage_transition:
    gatekeeper: L3 (Delegated)
    auto_approval: "If exit criteria met AND dependencies resolved"
  final_approval:
    gatekeeper: L5 (Director)
    auto_approval: Never
override_protocol:
  types:
    - type: approval_override
      description: "Director approves work flagged as not ready"
      audit: Full record + notification to future stages
    - type: rejection_override
      description: "Director rejects work flagged as ready"
      audit: Full record + feedback triggering rejection
    - type: gate_bypass
      description: "Director skips a gate"
      audit: Full record + risk assessment
    - type: delegation_revocation
      description: "Director rescinds auto-approval for a domain"
      audit: Record + confirmation of revocation
  override_record:
    schema:
      gate: string
      decision_overridden: string
      directors_decision: string
      rationale: string
      risk_assessment: string
      conditions: [string]
      timestamp: string (ISO 8601)
      review_date: string (if conditional)
```

---

## 12. Layer 9: Competitive Intelligence & Learning Layer (CILL)

### 12.1 Responsibility — NEW LAYER

The Competitive Intelligence & Learning Layer is the **continuous learning system** of the COS. It monitors the competitive landscape, captures cross-project patterns, accumulates postmortem knowledge, and refines quality heuristics based on what the system learns from other tools and its own production history.

**Why this layer exists:** The competitive landscape research (Competitive_Landscape.md) revealed that "No existing system does what COS does" — but the COS must continuously learn from the tools and frameworks that do exist. Every AI creative tool, game engine, pipeline tracker, and agent framework has strengths the COS should learn from. This layer makes learning architectural rather than ad-hoc.

Key responsibilities:
- **Competitive landscape monitoring:** Track developments in AI creative tools (Midjourney, Runway, Sora, etc.), game engines (Unreal, Unity), pipeline tools (ShotGrid, Ftrack), and agent frameworks (LangGraph, CrewAI)
- **Cross-project pattern recognition:** Analyze production data across projects to identify common bottlenecks, quality patterns, and efficiency opportunities
- **Postmortem knowledge accumulation:** Systematically capture "what to repeat" and "what to avoid" from every completed project
- **Quality heuristic refinement:** Continuously improve automated quality evaluation by comparing system scores with human expert ratings
- **Tool evolution tracking:** Monitor when new tools emerge that could replace or supplement existing TAL adapters
- **Capability gap identification:** Identify what the COS cannot do that competitive tools can — drive TAL adapter priorities
- **Benchmark maintenance:** Maintain a benchmark of creative outputs against which the COS can measure its own improvement

### 12.2 What the COS Can Learn from Other Tools

Based on the Competitive Landscape research:

| Tool/System | What COS Can Learn | How It Affects Architecture |
|------------|-------------------|----------------------------|
| **Midjourney** | Aesthetic quality tuning; human preference RL for creative output | Informs KQL quality heuristic training methodology |
| **Runway** | Camera control as a capability model; professional UX for creative tools | Informs TAL adapter design for AI video tools |
| **ComfyUI** | Node-based creative workflow graphs; reproducible workflow JSON | Informs POL subgraph model and capability bundle concept |
| **LangGraph** | Graph-based state machine with checkpointing; human-in-the-loop; conditional routing | Primary implementation pattern for POL |
| **ShotGrid/Flow** | Production tracking entity model; DCC integration patterns | Informs APML entity model and TAL integration patterns |
| **Unreal Engine** | MetaHuman character pipeline; PCG environment generation; Movie Render Graph | Informs capability encapsulation patterns for TAL adapters |
| **Unity** | AI-assisted creation tools (Muse); C# accessibility for pipeline development | Informs DEL assistant design and plugin architecture |
| **Adobe Flash** | NEVER be a single-vendor dependency; community is the moat | Informs architectural principle of open-architecture TAL |
| **Scratch** | Drag-and-drop creative programming for non-technical users | Informs DEL simplicity principles |
| **Pixar's USD** | Non-destructive layering; composition arcs | Already APML's core data model |

### 12.3 Inputs Received

| Input Type | Source | Description |
|-----------|--------|-------------|
| Competitive Landscape Data | External research | Documentation, releases, benchmarks from other tools |
| Project Postmortems | Layer 3 (POL), Layer 1 (DEL) | Completed project retrospectives |
| Feedback Trends | Layer 7 (FIL) | Patterns in feedback data across projects |
| Quality Evaluation Logs | Layer 4 (KQL) | Scores vs. human expert ratings for calibration |
| Tool Capability Gaps | Layer 6 (TAL) | Missing adapters or capabilities the system needs |
| User Satisfaction Data | Layer 1 (DEL) | Director satisfaction and friction points |

### 12.4 Outputs Produced

| Output Type | Destination | Description |
|------------|-------------|-------------|
| Refined Quality Heuristics | Layer 4 (KQL) | Updated evaluation criteria based on learning |
| Tool Integration Recommendations | Layer 1 (DEL) | Suggestions for new TAL adapters based on competitive analysis |
| Cross-Project Pattern Reports | Layer 1 (DEL), Layer 3 (POL) | Bottleneck warnings, efficiency opportunities |
| Benchmark Comparisons | Layer 1 (DEL) | How COS output compares to competitive tool output |
| Capability Gap Reports | Layer 6 (TAL), Layer 1 (DEL) | What the COS cannot do that users may need |
| Training Data | Layer 7 (FIL), Layer 4 (KQL) | Calibrated quality data for heuristic training |

---

## 13. 23 Specialist Agents Integrated into the Layer Stack

### 13.1 Specialist Hierarchy (from Specialist_Hierarchy.md)

The 47 original capabilities have been consolidated into 23 structured specialists across 4 tiers:

**Tier 1: Core Production Specialists (9)**
These are the bottleneck capabilities that MUST be independent:

| ID | Specialist | Domain | COS Layer | Why Independent |
|----|-----------|--------|-----------|-----------------|
| S01 | StoryArtist / Storyboard Artist | Story | L2 (CIL) | Narrative-to-visual translation; 6 downstream dependents |
| S02 | Screenwriter | Story | L2 (CIL) | Source node for all narrative work |
| C04 | DigitalModeler | Character | L3 (POL)/L6 (TAL) | #1 bottleneck — 10 connections; central geometry gateway |
| V04 | LayoutArtist / Previz | Visual | L3 (POL) | #2 bottleneck — 7 connections; 3D scene foundation |
| V05 | LightingTD / Lighting Artist | Visual | L3 (POL)/L6 (TAL) | #3 bottleneck — 7 connections; final look authority |
| A01 | Animator | Animation | L3 (POL)/L6 (TAL) | Performance creation; 6 dependents |
| D01 | FilmDirector / GameDirector | Direction | L1 (DEL)/L8 (APL) | Creative authority; 14 dependents |
| P04 | PipelineTD | Production | L6 (TAL) | Infrastructure backbone; ~47 connections |
| P05 | RenderingTD | Production | L3 (POL)/L6 (TAL) | Final output delivery; render farm interface |

**Tier 2: Integrated Production Specialists (6)**
These capabilities share knowledge bases and are merged:

| Merged Specialist | Original Capabilities | COS Layer | Merger Justification |
|------------------|----------------------|-----------|---------------------|
| M1: Surface & Material Artist | C06 TextureArtist + C07 ShadingTD + V08 Lookdev | L3 (POL)/L6 (TAL) | All surface appearance — same knowledge base; 30-40% iteration time reduction |
| M2: Simulation & Effects Artist | V07 FXArtist + A05 SimTD + C08 GroomingTD + C09 CreatureTD | L3 (POL)/L6 (TAL) | Physics simulation — shared solver knowledge; natural coupling |
| M3: Character Artist (Film) | C01 CharDesigner + C04 DigitalModeler + C02 Sculptor | L2 (CIL)/L3 (POL) | Character creation from concept through geometry |
| M4: Environment World-Builder | V01 EnvConcept + V03 EnvArtist | L2 (CIL)/L3 (POL) | Environment from concept to 3D — seamless handoff |
| M5: Game Asset Creator | C03 CharArtist + V03 EnvArtist (game path) | L3 (POL)/L6 (TAL) | Engine-optimized asset creation; shared optimization knowledge |
| M6: Production Coordinator | P02 ProdManager + P03 ProdCoord | L5 (APML) | Production tracking and coordination — natural hierarchy |

**Tier 3: Support Specialists (5)**

| ID | Specialist | Domain | COS Layer |
|----|-----------|--------|-----------|
| S03 | NarrativeDesigner (Game) | Story | L2 (CIL)/L3 (POL) |
| S04 | Visual Development Artist | Story | L2 (CIL) |
| V02 | Production Designer | Visual | L2 (CIL) |
| V06 | MattePainter | Visual | L3 (POL)/L6 (TAL) |
| A02 | AnimationTD | Animation | L3 (POL)/L6 (TAL) |
| A03 | Matchmove Artist | Animation | L3 (POL) |
| A04 | Motion CaptureTD | Animation | L3 (POL) |
| P07 | TechnicalArtist | Production | L6 (TAL) |
| P06 | Software Engineer | Production | L6 (TAL) |
| P08 | RenderWrangler | Production | L5 (APML) |
| P11 | AssetManager | Production | L5 (APML) |
| D09 | ArtDirector | Direction | L2 (CIL)/L4 (KQL) |
| D06 | VFXSupervisor | Direction | L1 (DEL)/L3 (POL) |
| D07 | CG Supervisor | Direction | L3 (POL) |

**Tier 4: Direction & Quality Specialists (3)**

| ID | Specialist | Domain | COS Layer |
|----|-----------|--------|-----------|
| Q01 | Braintrust | Quality | L7 (FIL) |
| Q03 | QA/QC Specialist | Quality | L4 (KQL) |
| Q04 | Postmortem Facilitator | Quality | L9 (CILL) |
| D04 | CreativeDirector (Game) | Direction | L2 (CIL) |
| D11 | Animation Supervisor | Direction | L2 (CIL)/L3 (POL) |
| D08 | Compositing Supervisor | Direction | L3 (POL) |
| D10 | Technical Director | Direction | L3 (POL)/L6 (TAL) |

### 13.2 Specialists Mapped to Layers

```
L1 (DEL) — Director Layer
  D01 FilmDirector / GameDirector (also L8 for approval)
  D06 VFXSupervisor (also L3)

L2 (CIL) — Creative Intent Layer
  S01 StoryArtist
  S02 Screenwriter
  S03 NarrativeDesigner (also L3)
  S04 VisualDevelopmentArtist
  M3 CharacterArtist (Film) [concept phase]
  M4 Environment World-Builder [concept phase]
  D04 CreativeDirector
  D09 ArtDirector (also L4)
  D11 AnimationSupervisor (also L3)

L3 (POL) — Pipeline Orchestration Layer
  C04 DigitalModeler (also L6)
  V04 LayoutArtist
  V05 LightingTD (also L6)
  A01 Animator (also L6)
  P05 RenderingTD (also L6)
  M1 Surface & Material Artist (also L6)
  M2 Simulation & Effects Artist (also L6)
  M3 CharacterArtist [production phase] (also L6)
  M4 Environment World-Builder [production phase] (also L6)
  M5 Game Asset Creator (also L6)
  V06 MattePainter (also L6)
  A02 AnimationTD (also L6)
  A03 MatchmoveArtist
  A04 MotionCaptureTD
  D07 CGSupervisor
  D08 CompositingSupervisor
  D11 AnimationSupervisor (also L2)

L4 (KQL) — Knowledge & Quality Layer
  Q03 QA/QC Specialist
  D09 ArtDirector (also L2)

L5 (APML) — Asset & Production Management Layer
  M6 Production Coordinator
  P08 RenderWrangler
  P11 AssetManager

L6 (TAL) — Tool Abstraction Layer
  C04 DigitalModeler (adapter)
  V05 LightingTD (adapter)
  A01 Animator (adapter)
  A02 AnimationTD
  P04 PipelineTD
  P05 RenderingTD (adapter)
  P06 SoftwareEngineer
  P07 TechnicalArtist
  P10 SystemsEngineer
  P09 ResearchScientist
  M1 Surface & Material Artist (adapter)
  M2 Simulation & Effects Artist (adapter)
  M3 CharacterArtist [3D phase] (adapter)
  M4 Environment World-Builder [3D phase] (adapter)
  M5 Game Asset Creator (adapter)
  V06 MattePainter (adapter)
  D10 TechnicalDirector (also L3)

L7 (FIL) — Feedback & Iteration Layer (Pure Braintrust)
  Q01 Braintrust

L8 (APL) — Approval Layer
  D01 FilmDirector / GameDirector (exercises approval via DEL)

L9 (CILL) — Competitive Intelligence & Learning Layer
  Q04 Postmortem Facilitator
```

---

## 14. Decision Architecture: Feedback vs. Approval Separation

### 14.1 The Central Architectural Principle

The most important insight from the full research program (Creative_Roles_as_Functions.md, Decision_Architecture.md, Creative_Decision_Systems.md) is the **architectural separation of feedback from approval**.

In most systems, feedback and approval are conflated — a reviewer both suggests changes AND blocks merging. The COS enforces this separation at the layer level:

``` 
                         FEEDBACK PATH                        APPROVAL PATH
                     (Non-binding, Braintrust)              (Binding, Director)
                             |                                    |
    Layer 7 (FIL)            |       Layer 8 (APL)                |
  +--------------------------+    +-----------------------------+ |
  | Pure Braintrust:         |    | Director Approval Gate:     | |
  | - Evaluates quality      |    | - Approves/rejects shots    | |
  | - Identifies problems    |    | - Signs off milestones      | |
  | - Makes recommendations  |    | - Manages auto-approval     | |
  | - Tracks iterations      |    | - Logs overrides            | |
  | - ZERO authority         |    | - FULL authority            | |
  +--------------------------+    +-----------------------------+ |
           |                                    |                 |
           | (recommendations)                  | (decisions)     |
           v                                    v                 |
    Layer 3 (POL) ←←←←←←←←←←←←←←←←←←←←←←←←←←←←←←                  |
    (Executes on approved decisions only)                          |
```

**The critical rule:** Feedback flows UP to the Director (via DEL → FIL). Decisions flow DOWN from the Director (via DEL → APL → POL). The feedback layer never sends commands directly to the pipeline layer — only recommendations that the Director has approved through the APL.

### 14.2 How Feedback Sources Interact with Approval

| Feedback Source | Weight | Authority | Routes To | Can Block? |
|----------------|--------|-----------|-----------|------------|
| Director (DEL) | VETO / FINAL | Full creative authority | Layer 7 (FIL) for categorization; Layer 8 (APL) for execution | YES |
| Braintrust (FIL) | Variable (recommendations) | ZERO | Layer 1 (DEL) for director awareness | NO |
| Quality Heuristics (KQL) | High (0.7-0.9) | Advisory | Layer 7 (FIL) for evaluation aggregation | NO |
| Domain Knowledge (KQL) | Medium (0.5-0.7) | Advisory | Layer 2 (CIL) for intent guidance | NO |
| Competitive Analysis (CILL) | Low-Medium (0.3-0.5) | Advisory | Layer 4 (KQL) for heuristic refinement | NO |

### 14.3 Decision Authority Flow

```
1. Director provides creative vision (DEL)
         │
2. CIL decomposes intent, generates brief (L2)
         │
3. POL orchestrates execution (L3)
         │
4. TAL executes via tool adapters (L6)
         │
5. Work published to APML (L5)
         │
6. FIL evaluates quality (L7) ──→ RECOMMENDATION (non-binding)
         │
7. DEL presents evaluation to Director (L1)
         │
8. Director makes decision (L1)
         │
9. APL executes the decision (L8) ──→ BINDING COMMAND
         │
10. POL advances state machine (L3)
```

---

## 15. Braintrust Pattern: Pure Feedback Layer

### 15.1 Braintrust Architecture in the COS

The Braintrust pattern from Pixar is implemented as Layer 7 (FIL) with strict architectural enforcement:

**The Braintrust (FIL) is:**
- A pure feedback signal generator
- Zero write authority to any production system
- Read-only with respect to creative artifacts
- Composed of peer evaluators (AI agents that have been "through the process")
- Focused on problems, not solutions

**The Braintrust (FIL) is NOT:**
- A decision maker
- An approval gate
- A blocker
- A command authority

### 15.2 Braintrust Functions

| Function | Description | Invocation |
|----------|-------------|------------|
| evaluateCreativeWork | Assess work against quality criteria and creative intent | On submission for review |
| identifyProblems | Surface what is wrong — NOT how to fix it | Output of evaluation |
| suggestDirections | Propose high-level resolution vectors (not specific solutions) | Output of problem identification |
| headlineFeedback | Synthesize feedback into prioritized summary: "what to blow up, what to love" | Post-processing |
| maintainCompact | Enforce candor norms, prohibit personal attacks, ensure zero authority leakage | Meta-function — always active |
| trackIterations | Monitor iteration history and diminishing returns | Continuous |

### 15.3 The Plussing Protocol (Enforced by FIL)

1. **Start with what works.** "The composition here is strong — the rule of thirds draws the eye naturally."
2. **State the problem.** "However, the color temperature shifts abruptly between frames 24 and 36."
3. **Explain why it matters.** "This will feel jarring to the audience."
4. **Suggest a direction (not a solution).** "What if we tried a gradual temperature transition?"
5. **End on encouragement.** "The intent is clear and strong — the execution just needs smoothing."

### 15.4 Braintrust Interface (Read-Only)

```typescript
interface Braintrust {
    // Core evaluation — produces non-binding recommendations
    evaluate(input: {
        workInProgress: Artifact,
        creativeIntent: CreativeBrief,
        productionContext: ProductionPhase
    }): Promise<FeedbackPackage>;

    // Read-only retrieval
    getLatestFeedback(projectId: ProjectID): FeedbackPackage;
    getFeedbackHistory(projectId: ProjectID): FeedbackPackage[];
}

type FeedbackPackage = {
    sessionId: string;
    artifacts: {
        problems: Problem[];          // What is wrong
        directions: Direction[];      // How to fix (high-level)
        headline: {                   // "Blow up" / "Love"
            critical: string[];
            positive: string[];
        };
        confidence: Map<ProblemID, ConfidenceLevel>;
    };
    meta: {
        participants: AgentID[];
        compactViolations?: number;
    };
};
```

---

## 16. First Workflow: Storyboard Creation — Data Flow Through Architecture

### 16.1 Workflow Summary

Based on Smallest_Viable_COS_and_First_Workflow.md, the first workflow to master is **Storyboard Creation** — translating a script into sequential visual panels with shot descriptions, camera notes, and timing annotations.

**Input:** Script text or verbal pitch + direction (tone, style references, emotional beats)
**Output:** 5-15 storyboard panels per sequence
**Capabilities:** S02 (Screenwriter) + S01 (StoryArtist) + D01 (Director) + FIL (Quality)
**Tools:** 1 primary — image generation adapter (via TAL)

### 16.2 Data Flow Through the 9-Layer Architecture

```
STEP 1: DIRECTOR PROVIDES INTENT
──────────────────────────────────
Layer 1 (DEL):
  Director provides: Script text + verbal pitch + style references + emotional beats
  DEL routes to: Layer 2 (CIL) for intent decomposition
  DEL generates: intent_fidelity_token for tracking

STEP 2: INTENT DECOMPOSITION
──────────────────────────────
Layer 2 (CIL):
  Activity: Decompose script into story beats, identify key emotional moments
  Activity: Extract constraints (must-show scenes, character requirements)
  Activity: Generate intent_fidelity_token linked to original brief
  Outputs to Layer 3 (POL): Structured brief with:
    - Scene breakdown (N scenes, M beats per scene)
    - Character list and visual references
    - Tone/emotional arc specification
    - Quality criteria (emotional beat clarity, narrative coherence, pacing, silhouette readability)
    - Mode: EXPLORATION (generate 5 options per beat)

STEP 3: ORCHESTRATION
──────────────────────
Layer 3 (POL):
  Activity: Receive brief from CIL
  Activity: Instantiate subgraph: S02 (Screenwriter) → S01 (StoryArtist)
  Activity: Queue work items: "Generate storyboard panel sequence"
  Activity: Route to Layer 6 (TAL) for tool execution
  Activity: Register entities in Layer 5 (APML) for tracking

STEP 4: SPECIALIST EXECUTION
─────────────────────────────
Layer 6 (TAL):
  Activity: Invoke Screenwriter capability (S02) — parse script into story beats
  Activity: Invoke StoryArtist capability (S01) — generate visual panels
  Activity: Image generation adapter creates 5 panel options per beat
  Outputs to Layer 5 (APML): Published storyboard panels with metadata

STEP 5: ASSET MANAGEMENT
─────────────────────────
Layer 5 (APML):
  Activity: Store version 1 of all panels
  Activity: Register dependencies (panel → beat → scene → script)
  Activity: Notify Layer 3 (POL) that work is ready for review

STEP 6: PURE BRAINTRUST EVALUATION
────────────────────────────────────
Layer 7 (FIL):
  Activity: Retrieve panels from Layer 5 (APML)
  Activity: Evaluate against quality criteria:
    - Silhouette readability: Does each panel communicate clearly?
    - Emotional beat clarity: Does the sequence convey the intended emotion?
    - Narrative coherence: Do panels flow logically?
    - Pacing/rhythm: Is the panel count appropriate per beat?
  Activity: Apply plussing protocol to all findings
  Activity: Generate FeedbackPackage:
    - Problems identified (NOT solutions)
    - High-level directions for improvement
    - Confidence scores per evaluation
  Activity: Send to Layer 1 (DEL) for director awareness
  KEY: This output is PURELY RECOMMENDATORY. Zero approval authority.

STEP 7: DIRECTOR REVIEW
────────────────────────
Layer 1 (DEL):
  Activity: Present 5 panel options per beat to Director
  Activity: Show Braintrust evaluations (Layer 7) alongside panels
  Activity: Director selects preferred options
  Activity: Director provides feedback (structural or surface)

STEP 8: APPROVAL OR REVISION
─────────────────────────────
Layer 8 (APL):
  If Director APPROVES:
    - APL sends binding "approved" signal to Layer 3 (POL)
    - POL advances state: pending_review → approved
    - Panels are finalized in Layer 5 (APML)
  If Director selects + gives FEEDBACK:
    - APL sends "revise with notes" signal to Layer 3 (POL)
    - POL advances state: pending_review → revising
    - Feedback is routed through Layer 7 (FIL) for categorization
    - If structural: triggers Layer 2 (CIL) mode switch back to exploration
    - If surface: stays in refinement mode

STEP 9: ITERATION LOOP
───────────────────────
  Repeat Steps 3-8 for each iteration:
    - Each iteration produces new panel versions in Layer 5 (APML)
    - Layer 7 (FIL) tracks iteration history and diminishing returns
    - After N iterations (configurable), FIL recommends "good enough" or escalate
    - Director decides via Layer 8 (APL)

STEP 10: LEARNING
──────────────────
Layer 9 (CILL):
  Activity: After project completion, capture postmortem
  Activity: Cross-project pattern analysis (storyboard workflows only)
  Activity: Feed quality evaluation data back to Layer 4 (KQL) for heuristic refinement
  Activity: Monitor competitive AI image tools for new capabilities
```

### 16.3 Intent Fidelity Tracking in Storyboard Flow

```
Step 1: Original brief → intent_fidelity_token = "1.0" (perfect fidelity)
Step 2: CIL decomposition → first fidelity check (CIL validates against original brief)
Step 3: POL routing → second check (are the right specialists selected?)
Step 4: TAL execution → third check (did the tool produce what was briefed?)
Step 6: FIL evaluation → fourth check (does output match creative intent?)
Step 7: Director review → FINAL check (does the Director agree?)

If any fidelity check scores < 0.8, the system raises a flag and returns to the
previous layer for correction before proceeding.
```

---

## 17. MVP Architecture (8 Capabilities) vs. Full Architecture (23 Specialists)

### 17.1 MVP: 8 Capabilities

Based on Smallest_Viable_COS_and_First_Workflow.md, the absolute minimum viable system requires 8 capability units:

| # | Capability | COS Role | Layer |
|---|-----------|----------|-------|
| 1 | D01: Director / User | Provides vision, reviews, approves | L1 (DEL) + L8 (APL) |
| 2 | S04: Visual Development Artist | Establishes visual language, style | L2 (CIL) |
| 3 | V01: Environment Concept Artist | Designs environment mood, atmosphere | L2 (CIL) |
| 4 | V03: Environment Artist | Creates 3D environment meshes | L3 (POL)/L6 (TAL) |
| 5 | V05: Lighting TD | Places lights, configures render | L3 (POL)/L6 (TAL) |
| 6 | P05: Rendering TD | Manages render execution | L3 (POL)/L6 (TAL) |
| 7 | FIL (Integrated) | Quality evaluation, iteration tracking | L7 (FIL) |
| 8 | P04: Pipeline TD | Tool adapters, automation | L6 (TAL) |

**MVP Layer Mapping:**

```
L1 (DEL) ─── D01 — intent input, review, configuration
L2 (CIL) ─── S04 + V01 — intent translation, exploration, brief creation
L3 (POL) ─── V03 + V05 + P05 — workflow orchestration
L4 (KQL) ─── Integrated quality heuristics (basic: silhouette, tonal consistency, reference grounding)
L5 (APML) ── Basic file versioning (minimal — stubbed for expansion)
L6 (TAL) ─── P04 — Blender adapter, data translation, execution
L7 (FIL) ─── Integrated feedback loop — iteration tracking, quality scoring
L8 (APL) ─── D01 exercises approval here (minimal gate management)
L9 (CILL) ── Not present in MVP
```

**What the MVP does:**
- Produces static environment renders
- Full feedback loop: brief → options → select → refine → approve
- Exploration → refinement mode management
- Basic quality evaluation heuristics
- Single tool (Blender) via TAL

**What the MVP does NOT do:**
- No characters, no animation, no narrative
- No simulation, no VFX
- No multi-tool orchestration
- No collaborative review
- No schedule/budget tracking
- No automated Braintrust (FIL is manual evaluation only)

### 17.2 Full Architecture: 23 Specialists

The full architecture adds:

**Additional layers active in full:**
- L9 (CILL) — Competitive learning and cross-project knowledge

**Additional specialists beyond MVP:**

| Domain | Specialists Added | What They Enable |
|--------|------------------|------------------|
| Story | S01 StoryArtist, S02 Screenwriter, S03 NarrativeDesigner | Storyboards, scripts, interactive narrative |
| Character | M3 CharacterArtist (C01+C04+C02), C05 Rigger, M1 Surface&Material (C06+C07+V08) | Character creation, rigging, surfacing |
| Animation | A01 Animator, A02 AnimationTD, A03 Matchmove, A04 MocapTD, M2 Sim&FX (V07+A05+C08+C09) | Character performance, motion, simulation |
| Visual | V04 LayoutArtist, V06 MattePainter, M4 EnvWorldBuilder (V01+V03), V02 ProdDesigner | Layout, matte painting, production design |
| Direction | D04 CreativeDir, D06 VFXSup, D07 CGSup, D08 CompSup, D09 ArtDir, D10 TechDir, D11 AnimSup | Department leads, supervisors, quality oversight |
| Quality | Q01 Braintrust (automated), Q03 QA/QC, Q04 Postmortem | Automated quality evaluation, QA testing, learning |
| Production | M6 ProdCoord (P02+P03), P06 SoftwareEng, P07 TechArtist, P08 RenderWrangler, P11 AssetManager | Production management, tooling, rendering infrastructure |

### 17.3 Capability Expansion Path

```
Phase 1 (MVP):  Environment Render
  8 capabilities, 1 tool, static output
  ├── S04, V01, V03, V05, P05, P04, D01, FIL

Phase 2: Storyboard Creation
  +4 capabilities, +1 tool (image generation)
  ├── S02, S01, expanded FIL, expanded DEL
  └── Unlocks: narrative workflows, upstream pipeline

Phase 3: Layout & Camera
  +1 capability (V04 LayoutArtist), +3D tool expansion
  ├── Storyboard → 3D layout pipeline
  └── Unlocks: shot composition, camera motion

Phase 4: Character Pipeline
  +4 capabilities (M3, C05, M1, M2)
  ├── Character design, modeling, rigging, surfacing
  ├── Requires: DigitalModeler (C04) integrated in Phase 3
  └── Unlocks: animation, character-driven content

Phase 5: Animation
  +2 capabilities (A01, A02)
  ├── Character performance, animation tools
  └── Unlocks: cinematic shots, full narrative animation

Phase 6: Full Pipeline Integration
  +4 capabilities (M2, V06, D08, P08)
  ├── VFX simulation, compositing, rendering farm
  └── Unlocks: cinematic-quality final output

Phase 7: Competitive Learning & Multi-Project
  +3 capabilities (Q01 automated, Q03, Q04, CILL)
  ├── Automated Braintrust quality evaluation
  ├── Cross-project learning, quality heuristic refinement
  └── Unlocks: continuous improvement, institutional knowledge
```

---

## 18. Hybrid Organizational Model Position Within the Architecture

### 18.1 Three Organizational Models (from Three_Organizational_Models.md)

| Model | Name | Control | Automation | Complexity | Metaphor |
|-------|------|---------|------------|------------|----------|
| A | Director + Specialists | Maximum user control | Minimum automation | Simple for system, demanding on user | Freelance director hiring artists |
| B | Capability Network | Minimum user involvement | Maximum automation | Complex to build, invisible once running | Self-routing neural network |
| C | Hierarchical Studio | Balanced | Moderate automation | Moderate complexity, familiar structure | Film/TV production studio |

### 18.2 Recommended: Hybrid Layered Model

The COS implements a **hybrid model** that overlays all three modes across the 9-layer architecture, with Mode C (Hierarchical Studio) as the default and Mode A (Direct Invocation) and Mode B (Capability Network) as selectable modes:

```
                         LAYER ARCHITECTURE
┌─────────────────────────────────────────────────────────────────┐
│  L1 (DEL)                     Mode A, C: Director communicates  │
│  L2 (CIL)                     Mode A, C: Intent decomposition   │
│  L3 (POL)                     Mode B: Graph routing engine      │
│  L4 (KQL)                     All modes: Knowledge queries      │
│  L5 (APML)                    All modes: Asset management       │
│  L6 (TAL)                     All modes: Tool abstraction       │
│  L7 (FIL)                     All modes: Braintrust feedback    │
│  L8 (APL)                     All modes: Approval gates         │
│  L9 (CILL)                    All modes: Learning               │
└─────────────────────────────────────────────────────────────────┘

                  MODE SELECTION (configurable per project)
┌─────────────────────────────────────────────────────────────────┐
│  Mode A (Direct + Specialists):  L3 bypasses graph routing     │
│    - Director invokes specialists directly through DEL          │
│    - POL acts as stateless dispatcher, not graph router         │
│    - Best for: small projects, expert users, rapid prototyping  │
│                                                                  │
│  Mode B (Capability Network - DEFAULT):  L3 is graph router    │
│    - Brief defines subgraph; POL routes work tokens             │
│    - Automatic dependency resolution, parallel execution        │
│    - Best for: large productions, automated pipelines           │
│                                                                  │
│  Mode C (Hierarchical Studio):  L2+L3 with department leads    │
│    - Department leads mediate Director↔Specialist communication │
│    - M6 (ProdCoord) manages cross-department handoffs           │
│    - Best for: complex projects, multi-user teams               │
└─────────────────────────────────────────────────────────────────┘
```

### 18.3 Where Each Mode Lives in the Architecture

**Mode A (Director + Specialists):**
- Primary layers: L1 (DEL), L2 (CIL), L6 (TAL)
- L3 (POL) is bypassed — Director manages dependencies manually
- Each specialist is independently addressable via TAL
- Director acts as the dependency graph

**Mode B (Capability Network — DEFAULT):**
- Primary layers: L3 (POL), L2 (CIL), L6 (TAL)
- POL contains the graph router that instantiates subgraphs
- Work tokens propagate through graph automatically
- L7 (FIL) quality gates provide feedback signals

**Mode C (Hierarchical Studio):**
- Primary layers: L1 (DEL), L2 (CIL), L5 (APML)
- Department leads (specialists at L2) mediate communication
- M6 (Production Coordinator at L5) manages cross-department handoffs
- Director communicates with leads, not individual specialists

### 18.4 Implementation Phasing for Hybrid Model

| Phase | Mode | What Gets Built | When |
|-------|------|-----------------|------|
| v1.0 | Mode A | Director + Specialists (MVP) | Phase 1 |
| v2.0 | Mode A + Department structure | Mode A with conceptual department grouping | Phase 2-3 |
| v3.0 | Mode C (default) | Hierarchical Studio with department leads, PMO | Phase 4-5 |
| v4.0 | Mode B (optional stretch goal) | Capability Network graph router | Phase 6+ (decision gate) |

**Decision Gate at Phase 3:** "Do we need Capability Network (Model B) or can we extend Hierarchical Studio (Model C)?" Model B has 10/10 Implementation Difficulty and is marked as a stretch goal.

---

## 19. Updated Interface Contracts

### 19.1 New Interface Contracts (Not in v1)

| Contract ID | Source → Destination | Description | New/Updated |
|------------|---------------------|-------------|-------------|
| IC-01 | DEL → CIL | Brief Submission | Updated — intent_fidelity_token added |
| IC-02 | CIL → POL | Formal Brief | Updated — specialist_requirements, intent_fidelity_token added |
| IC-03 | FIL → CIL | Feedback with Mode Trigger | Updated — confidence scoring added |
| IC-04 | POL → APML | Asset Command | Updated — graph-based transitions |
| IC-05 | POL → TAL | Execution Command | Updated — specialist routing |
| **IC-06** | **FIL → APL** | **Quality Recommendation** | **NEW** — FIL recommends to APL, not to POL directly |
| **IC-07** | **APL → POL** | **Binding Approval Command** | **NEW** — APL issues binding state transitions |
| **IC-08** | **CILL → KQL** | **Heuristic Refinement Data** | **NEW** — competitive learning feeds quality heuristics |
| **IC-09** | **CILL → DEL** | **Competitive Insights Report** | **NEW** — learnings from other tools presented to Director |
| **IC-10** | **CIL → CILL** | **Intent Fidelity Logs** | **NEW** — intent preservation data for learning |
| IC-11 | DEL → APL | Approval Decision | Updated — now explicit routing |
| IC-12 | POL → FIL | Work for Evaluation | Updated |
| IC-13 | KQL → FIL | Quality Evaluation | Updated |
| IC-14 | APML → FIL | Asset for Review | Updated |
| IC-15 | TAL → APML | Published Asset | Updated |
| IC-16 | FIL → KQL | Feedback Trends | Updated |
| IC-17 | POL → KQL | Cost Estimate Request | Updated |
| IC-18 | DEL → KQL | Style Guide Config | Updated |
| IC-19 | CIL → KQL | Domain Guidance Request | Updated |
| **IC-20** | **POL → CILL** | **Project Postmortem Data** | **NEW** |
| **IC-21** | **TAL → CILL** | **Tool Capability Gap Report** | **NEW** |

### 19.2 Key Updated Contracts

#### IC-06: FIL → APL (Quality Recommendation)

```yaml
interface_id: IC-06
source: Feedback & Iteration Layer (Layer 7)
destination: Approval Layer (Layer 8)
direction: unidirectional
call_type: asynchronous
disclaimer: "This is a BRAINTRUST RECOMMENDATION. It has NO approval authority."
description: "FIL's quality evaluation and gate recommendation to the approval authority"
schema:
  entity_id: string
  evaluation_summary:
    overall_score: number
    confidence: number
    "good_enough": boolean
    diminishing_returns_detected: boolean
  recommendation:
    action: [advance, revise, return_to_exploration, hold, escalate]
    rationale: string
    risks: [RiskAssessment]
    alternatives: [AlternativeAction]
  feedback_highlights: [string]
validation:
  - "Output MUST NOT contain binding language ('approved', 'rejected', 'final')"
  - "Must include one or more alternative actions if main recommendation is not accepted"
```

#### IC-07: APL → POL (Binding Approval Command)

```yaml
interface_id: IC-07
source: Approval Layer (Layer 8)
destination: Pipeline Orchestration Layer (Layer 3)
direction: unidirectional
call_type: synchronous
authority: BINDING — POL MUST execute this command
description: "Authoritative approval decision from Director for state machine transition"
schema:
  approval_id: string
  entity_id: string
  decision: [approved, rejected, revise, conditionally_approved, override]
  approved_transition:
    from_state: string
    to_state: string
  authority_level: [L1, L2, L3, L4, L5]
  conditions: [Condition]  # For conditional approvals
  based_on_recommendation: string  # Reference to FIL recommendation ID (if any)
  override_of: string  # If this overrides a gate
  director_notes: string
validation:
  - "Must include authority_level matching the decision domain"
  - "override_of must include risk_assessment if present"
  - "APL commands are authoritative — POL must not question them"
```

#### IC-08: CILL → KQL (Heuristic Refinement Data)

```yaml
interface_id: IC-08
source: Competitive Intelligence & Learning Layer (Layer 9)
destination: Knowledge & Quality Layer (Layer 4)
direction: unidirectional
call_type: event-driven (periodic)
description: "Refined quality heuristics and competitive benchmarks for KQL"
schema:
  refinement_batch_id: string
  timestamp: string (ISO 8601)
  heuristic_updates:
    - heuristic_id: string
      new_weight: number
      new_threshold: number
      evidence: [string]  # Competitive or cross-project evidence
      confidence: number
  new_heuristics:
    - id: string
      domain: string
      description: string
      source: [competitive_analysis, postmortem, cross_project_pattern]
  benchmark_data:
    tool: string
    metric: string
    score: number
    comparison: string  # "COS_score vs tool_score"
validation:
  - "All heuristic updates must include evidence and confidence"
  - "New heuristics must include source attribution"
```

### 19.3 Full Layer Interface Map

```
DEL (1)  ←→  CIL (2)   via Briefs & Feedback (IC-01)
DEL (1)  ←→  POL (3)   via Status Requests & State Events
DEL (1)  →   FIL (7)   via Director Feedback Records
DEL (1)  →   APL (8)   via Approval Decisions (IC-11)
DEL (1)  ←→  KQL (4)   via Style Guides & Configuration (IC-18)
DEL (1)  ←→  APML (5)  via Asset Status & Recovery
DEL (1)  ←  CILL (9)   via Competitive Insights Reports (IC-09)
CIL (2)  →   POL (3)   via Formal Briefs (IC-02)
CIL (2)  →   FIL (7)   via Interpretation Variations (for Braintrust review)
CIL (2)  ←→  KQL (4)   via Domain Guidance & Constraint Queries (IC-19)
CIL (2)  →   CILL (9)  via Intent Fidelity Logs (IC-10)
POL (3)  →   APML (5)  via Asset Commands & Dependency Declarations (IC-04)
POL (3)  →   TAL (6)   via Execution Commands & Resource Requests (IC-05)
POL (3)  →   FIL (7)   via State Transitions & Work for Evaluation (IC-12)
POL (3)  ←→  KQL (4)   via Cost Estimates & Quality Signals (IC-17)
POL (3)  ←  APL (8)   via Binding Approval Commands (IC-07)
POL (3)  →   CILL (9)  via Project Postmortem Data (IC-20)
APML (5) ←→  TAL (6)   via Asset Publishing & Retrieval (IC-15)
APML (5) →   FIL (7)   via Asset for Review (IC-14)
TAL (6)  →   APML (5)  via Published Asset Data
TAL (6)  →   CILL (9)  via Tool Capability Gap Reports (IC-21)
KQL (4)  →   FIL (7)   via Quality Evaluations (IC-13)
KQL (4)  ←  CILL (9)  via Heuristic Refinement Data (IC-08)
FIL (7)  →   CIL (2)   via Structured Feedback (with mode triggers) (IC-03)
FIL (7)  →   APL (8)   via Quality Recommendations (IC-06)
FIL (7)  →   KQL (4)   via Feedback Trends & Quality Data (IC-16)
APL (8)  →   POL (3)   via Binding Approval Commands (IC-07)
CILL (9) →   KQL (4)   via Heuristic Refinement Data (IC-08)
CILL (9) →   DEL (1)   via Competitive Insights Reports (IC-09)
```

---

## 20. Implementation Roadmap

### 20.1 Roadmap Overview

The implementation roadmap incorporates all findings from the research program:

1. **Storyboard first, environment second** (Smallest_Viable_COS.md Finding 1)
2. **Graph-based POL, not linear** (Architecture-Changing Discoveries Finding 2)
3. **DigitalModeler integration spike in Phase 1** (Finding 3)
4. **Human-in-the-loop Braintrust first, automated FIL later** (Finding 4)
5. **Quality signal validation sprint before KQL engine** (Finding 5)
6. **Model B as stretch goal** (Finding 6)

### 20.2 Phase 1: Storyboard MVP (Weeks 1-8)

**Goal:** Working storyboard creation system with human-in-the-loop feedback

**Capabilities:**
- S02 Screenwriter (parse script → story beats)
- S01 StoryArtist (generate storyboard panels)
- D01 Director (vision, review, approval)
- P04 PipelineTD (image generation adapter)

**Layers Active:**
- L1 (DEL) — Minimal director interface (brief input, panel review, approval)
- L2 (CIL) — Brief decomposition, exploration mode (generate N=5 options)
- L3 (POL) — Simple state machine (linear for MVP)
- L5 (APML) — Basic version storage
- L6 (TAL) — Image generation adapter (Stable Diffusion / Midjourney)
- L7 (FIL) — Human-in-the-loop Braintrust (manual evaluation, structured feedback templates)
- L8 (APL) — Basic approval routing

**Deliverables:**
- Director can input script + direction → receive 5 storyboard options
- Director can give structured feedback → receive revised panels
- Director can approve panels → panels saved with metadata
- Basic iteration tracking (version history, feedback log)

**Milestone: Storyboard MVP Demo** — End of Week 8

### 20.3 Phase 2: Storyboard Production + Environment MVP (Weeks 9-16)

**Capabilities Added:**
- S04 VisDev (visual style guidance)
- V01 EnvConcept (environment concept art)
- V03 EnvArtist (3D environment creation)
- V05 LightingTD (lighting and rendering)
- P05 RenderingTD (render execution)
- M4 Environment World-Builder (V01+V03 merged)

**Layers Active:**
- L3 (POL) — Graph-based state machine (non-linear transitions)
- L6 (TAL) — Blender adapter added
- L4 (KQL) — Quality signal validation sprint (Weeks 12-14)
- L7 (FIL) — Feedback templates for visual quality

**Deliverables:**
- Full storyboard → layout → environment pipeline
- Non-linear POL (skip stages, return to exploration)
- Validated quality heuristics for visual output
- Basic style guide persistence in KQL

**Milestone: Dual Workflow Demo** — End of Week 16

### 20.4 Phase 3: Character Pipeline (Weeks 17-24)

**Capabilities Added:**
- M3 CharacterArtist (C01+C04+C02 — character concept to geometry)
- C05 Rigger (character rigging)
- M1 Surface & Material Artist (C06+C07+V08 — texturing, shading, lookdev)

**Integration Work:**
- DigitalModeler integration spike (resolves #1 bottleneck)
- Character asset pipeline through APML
- Rig validation and quality evaluation

**Organizational Model:**
- Mode A (Direct) for character workflow
- Department structure conceptual grouping begins (CIL routes by domain)

**Deliverables:**
- Character design → model → rig pipeline
- Validated rig quality evaluation
- Character assets managed in APML with dependency tracking

**Milestone: Character Pipeline Demo** — End of Week 24

### 20.5 Phase 4: Animation (Weeks 25-32)

**Capabilities Added:**
- A01 Animator (character performance)
- A02 AnimationTD (animation tools and workflow)

**Layers Expanded:**
- L7 (FIL) — First automated Braintrust evaluations (learn from Phase 1-3 feedback patterns)
- L4 (KQL) — Quality heuristics refined using Phase 2 validation data

**Deliverables:**
- Rigged character + layout → animated performance
- Animation quality evaluation
- Automated FIL for structural feedback classification

**Milestone: Animation Pipeline Demo** — End of Week 32

### 20.6 Phase 5: VFX + Compositing (Weeks 33-40)

**Capabilities Added:**
- M2 Simulation & Effects Artist (V07+A05+C08+C09 — FX, sim, groom, creature)
- V06 MattePainter (2D/3D environment projections)
- D08 Compositing Supervisor (final image integration)
- P08 RenderWrangler (render farm management)

**Layers Expanded:**
- L6 (TAL) — Render farm adapter, multi-tool orchestration (Blender + Houdini + Nuke)
- L4 (KQL) — Full quality heuristics suite
- L8 (APL) — Auto-approval delegation rules

**Deliverables:**
- Full production pipeline: story → layout → character → animation → FX → lighting → render → comp
- Multi-tool orchestration via TAL
- Automated quality gates with human override

**Milestone: Cinematic Shot Pipeline** — End of Week 40

### 20.7 Phase 6: Full System + Learning (Weeks 41-52)

**Capabilities Added:**
- Q01 Braintrust (fully automated)
- Q03 QA/QC Specialist (automated testing)
- Q04 Postmortem Facilitator (automated retrospective)
- L9 CILL (Competitive Intelligence & Learning Layer)

**Organizational Model Decision Gate:**
- Evaluate: Build Model B (Capability Network graph router) or extend Model C?
- Decision based on: production complexity, user feedback, automation requirements

**Deliverables:**
- Fully automated Braintrust (quality evaluation + problem identification + iteration tracking)
- Cross-project learning (postmortem knowledge accumulation, quality heuristic refinement)
- Competitive landscape monitoring (new tool detection, capability gap identification)
- Full 23-specialist hierarchy active
- Multi-project orchestration support

**Milestone: COS v2.0 Release** — End of Week 52

### 20.8 Phase 7: Stretch Goals (Weeks 53+)

**Stretch Goals (Not Committed — Decision Gate Required):**
- Model B (Capability Network) — Full graph routing with dynamic subgraph instantiation
- Multi-user collaborative workflows (multiple directors, client review)
- Real-time virtual production integration (Unreal Engine LED wall pipeline)
- AI training pipeline (fine-tune specialist agents on COS production data)
- Public API / Capability SDK for third-party adapter development

### 20.9 Roadmap Summary Table

| Phase | Duration | Capabilities | Key Milestone | Risk |
|-------|----------|-------------|---------------|------|
| 1: Storyboard MVP | 8 weeks | 4 (S02, S01, D01, P04) | Storyboard MVP Demo | Low — simplest workflow |
| 2: Environment MVP | 8 weeks | +5 (S04, V01, V03, V05, P05) | Dual Workflow Demo | Medium — BLENDER integration complexity |
| 3: Character Pipeline | 8 weeks | +3 (M3, C05, M1) | Character Pipeline Demo | High — C05 Rigger bottleneck |
| 4: Animation | 8 weeks | +2 (A01, A02) | Animation Pipeline Demo | Medium — performance quality hard |
| 5: VFX + Compositing | 8 weeks | +4 (M2, V06, D08, P08) | Cinematic Shot Pipeline | High — multi-tool orchestration |
| 6: Full System + Learning | 12 weeks | +4 (Q01, Q03, Q04, CILL) | COS v2.0 Release | Medium — learning system unproven |
| 7: Stretch Goals | Ongoing | Model B, multi-user, etc. | Decision Gate Required | Very High — Model B complexity |

### 20.10 Risk Mitigation in the Roadmap

| Risk | Mitigation | Phase |
|------|-----------|-------|
| Quality heuristics unvalidated | Quality signal validation sprint in Phase 2 before KQL engine | Phase 2 |
| Braintrust lacks credibility | Human-in-the-loop Braintrust first; automated FIL only in Phase 4+ | Phase 1-3 |
| DigitalModeler bottleneck unknown | DigitalModeler integration spike in Phase 1 to assess complexity | Phase 1 |
| Linear POL creates tech debt | Build graph-based POL from Phase 1 (can default to linear transitions) | Phase 1 |
| Model B too complex | Stretch goal with decision gate at Phase 3 | Phase 7 |
| Multi-tool orchestration fragile | Single tool (Blender) in MVP; expand gradually | All phases |
| Intent loss across layers | Intent fidelity tracking from Phase 1 (CIL elevation) | Phase 1 |

---

*End of COS Architecture v2 — Full Research Synthesis*
*Supersedes: COS_Architecture_v1.md*
*Date: June 14, 2026*
