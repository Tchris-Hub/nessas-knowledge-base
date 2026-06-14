# Creative Operating System (COS) — Architecture v1

**Document ID:** COS-01-CA-001  
**Version:** 1.0 (First Draft)  
**Date:** June 14, 2026  
**Status:** Draft for Review  
**Author:** COS Architecture Agent  
**Scope:** System-level architecture — layers, interfaces, data flow, dependencies  

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Architectural Principles](#2-architectural-principles)
3. [Patterns Extracted from Specialist Research](#3-patterns-extracted-from-specialist-research)
4. [Layer Architecture Overview](#4-layer-architecture-overview)
5. [Layer 1: Director Experience Layer (DEL)](#5-layer-1-director-experience-layer-del)
6. [Layer 2: Creative Intent Layer (CIL)](#6-layer-2-creative-intent-layer-cil)
7. [Layer 3: Pipeline Orchestration Layer (POL)](#7-layer-3-pipeline-orchestration-layer-pol)
8. [Layer 4: Knowledge & Quality Layer (KQL)](#8-layer-4-knowledge--quality-layer-kql)
9. [Layer 5: Asset & Production Management Layer (APML)](#9-layer-5-asset--production-management-layer-apml)
10. [Layer 6: Tool Abstraction Layer (TAL)](#10-layer-6-tool-abstraction-layer-tal)
11. [Layer 7: Feedback & Iteration Layer (FIL)](#11-layer-7-feedback--iteration-layer-fil)
12. [Interface Contracts Between Layers](#12-interface-contracts-between-layers)
13. [Data Flow Architecture](#13-data-flow-architecture)
14. [Dependency Graph](#14-dependency-graph)
15. [Concepts Mapped from Specialist Research](#15-concepts-mapped-from-specialist-research)
16. [Architectural Decision Records (ADRs)](#16-architectural-decision-records-adrs)
17. [Open Questions and Future Work](#17-open-questions-and-future-work)

---

## 1. Executive Summary

The Creative Operating System (COS) is a **meta-orchestration layer** that sits ABOVE existing creative tools (Blender, Unreal Engine, Houdini, Nuke, Maya, Substance, etc.) to coordinate, guide, and enhance creative production. It does not replace any tool — it provides the intelligence, workflow management, quality evaluation, and feedback infrastructure that currently exists only inside the minds of the most experienced human creative teams.

**The COS answers one question:** *What if every creative production had the equivalent of Pixar's Braintrust, an elite VFX pipeline TD team, a game studio's iterative playtest loop, and an experienced director's creative judgment — built into the infrastructure itself?*

**Architecture summary:** Seven layers organized into three functional stacks:

| Stack | Layers | Function |
|-------|--------|----------|
| **Creative Stack** | Director Experience (1), Creative Intent (2), Feedback & Iteration (7) | Human-COS interaction, intent communication, review cycles |
| **Orchestration Stack** | Pipeline Orchestration (3), Asset & Production Management (5) | Workflow coordination, state management, asset lifecycle |
| **Infrastructure Stack** | Knowledge & Quality (4), Tool Abstraction (6) | Domain expertise, quality signals, tool adapters |

The architecture is **platform-independent** — the Tool Abstraction Layer (Layer 6) insulates all upper layers from any specific DCC tool or engine. The feedback model is **Braintrust-inspired** — Layer 7 separates feedback from approval authority to encourage candor. The orchestration model is **TD-inspired** — invisible by design, enforcing rules through automation rather than documentation.

---

## 2. Architectural Principles

Extracted from the six specialist research documents, these principles govern every architectural decision:

| # | Principle | Source | Implication |
|---|-----------|--------|-------------|
| 1 | **Invisible by design** — The measure of a good pipeline is how little the artist thinks about it | TDs, Pixar | All layers must default to background operation. The Director Experience Layer is the only explicit interface. |
| 2 | **Feedback separated from authority** — The most candid feedback comes from people with no power to mandate changes | Pixar Braintrust | The Feedback & Iteration Layer must operate independently from the Pipeline Orchestration Layer. |
| 3 | **Enforce via automation, not documentation** — If a rule can be broken, it will be | TDs, ILM | Validation, constraints, and quality gates must be baked into the layer interfaces, not written in manuals. |
| 4 | **Protect creative intent above generated artifacts** — Losing a render is annoying; losing a scene file is catastrophic | ILM, TDs | Asset Management must prioritize versioning of creative decisions and intent over generated outputs. |
| 5 | **Ship 80%, iterate live** — Perfect infrastructure designed in isolation will fail under real pressure | TDs, game studios | Layers must support incremental deployment. Core functionality ships first; refinement happens under real use. |
| 6 | **Separate exploration from refinement** — Never refine before you've explored enough | Story/concept artists | The Creative Intent Layer must support divergent (generate fields) and convergent (narrow and polish) modes. |
| 7 | **Loop, not line** — Production pipelines are fundamentally iterative, not sequential | VFX, games, Pixar | All layers must support revision loops. Data flows bidirectionally. Upstream changes propagate downstream. |
| 8 | **Design for failure** — Assume network drops, disk failures, and software crashes | TDs | Every interface must validate, every handoff must have a recovery path, every layer must fail gracefully. |
| 9 | **Constraints are creative fuel** — The most creative work often comes from the tightest constraints | Story/concept, directors | The COS should surface and enforce creative constraints, not just technical ones. |
| 10 | **Platform-independent core** — The COS sits above all existing tools as an orchestration layer | Core requirement | No layer above the Tool Abstraction Layer may depend on any specific DCC tool, engine, or file format. |

---

## 3. Patterns Extracted from Specialist Research

### 3.1 Pixar Production Pipeline

| Pattern | COS Application |
|---------|----------------|
| 9-stage pipeline (Story → Modeling → Rigging → Surfaces → Layout → Animation → Simulation → Lighting → Rendering) | Stage model for the Pipeline Orchestration Layer. Each stage is a distinct expertise domain with its own interface contract. |
| Braintrust (feedback with no authority) | Core architectural pattern for Layer 7 (Feedback & Iteration). Feedback evaluation runs independently from production authority. |
| "Four legs" model (Creative + Technical + Production + Business) | Four equal functional domains in the COS. No single domain dominates the system. |
| Director has final creative authority | The Director Experience Layer is the approval gate. No layer may override a director's creative decision. |
| USD as non-destructive data backbone | Reference architecture for Layer 5 (Asset & Production Management). Layered, non-destructive composition of contributions. |
| Dailies (daily iterative review) | Rhythm model for Layer 7. Feedback cadence is regular, not event-driven. |
| TD "casting" system (rotation across films) | Knowledge transfer mechanism for Layer 4. Expertise should rotate across projects. |
| "Story is never done — you just run out of time and money" | Quality signal for Layer 7. "Done" is defined by schedule and purpose, not perfection. |

### 3.2 VFX House Pipeline

| Pattern | COS Application |
|---------|----------------|
| 18-stage pipeline with three phases (Pre-Production, Production, Post-Production) | Phase model for Layer 3. Different orchestration rules apply to each phase. |
| VFX Supervisor as central authority | Authority pattern: one person (or AI equivalent) holds creative/technical authority for the project. |
| Client-driven production | Requirement for Layer 6: external tool adapters must be parameterizable by client/delivery specs. |
| Pipeline is a loop, not a straight line | Core assumption for Layer 3. Shots cycle through review-feedback-revision multiple times at each stage. |
| Pipeline TD as "central nervous system" | Role pattern: the COS itself acts as the Pipeline TD for the entire production. |
| Build vs. Buy vs. Hack decision framework | Decision model for Layer 6 tool selection. The COS must evaluate whether to build adapters, use existing integrations, or create temporary workarounds. |
| CG Supervisor bridges creative intent and technical execution | Integration pattern between Layer 2 (Creative Intent) and Layer 6 (Tool Abstraction). |
| 80/20 rule: 80% grounded in reference, 20% original | Quality heuristic for Layer 4. Acceptable novelty must be grounded in recognizable reference. |

### 3.3 Game Studio Pipeline

| Pattern | COS Application |
|---------|----------------|
| Nested macro/micro pipelines | Orchestration model for Layer 3. Pipelines contain sub-pipelines (e.g., a rigging micro-pipeline within the overall asset pipeline). |
| Playtest-driven feedback loops | Validation model for Layer 7. Feedback should come from actual use/play, not just expert review. |
| Game Director owns creative vision | Authority pattern: the COS must recognize one ultimate creative decision-maker per project. |
| Vertical slice as quality target | Milestone model for Layer 3. The first major gate is a playable/seeable slice that proves the vision works. |
| Technical Artist as bridge role | Role pattern between Layer 2 and Layer 6. The COS must perform this bridging function internally. |
| Alpha/Beta/Polish gates | Gate model for Layer 3. Feature-complete, content-complete, quality-complete as distinct states. |
| "A delayed game is eventually good, but a rushed game is forever bad" | Quality philosophy for Layer 4. Quality gates should be flexible on schedule, rigid on quality. |

### 3.4 Directors & Creative Leadership

| Pattern | COS Application |
|---------|----------------|
| Layered communication system (look books, tone packets, storyboards, verbal direction) | Input model for Layer 1. The COS must accept multiple communication modalities, not just text. |
| Strategic sacrifice framework (calculated losses) | Decision model for Layer 2. When constraints conflict, the COS must identify what to sacrifice. |
| Five leadership types (Visionary, Technical, Collaborative, Producer-Driven, Auteur) | Persona model for Layer 1. The Director Experience Layer must adapt to different leadership styles. |
| "I'll Know It When I See It" (IKIWISI) problem | Interaction model for Layer 7. The COS must support convergent search without a clearly defined target. |
| Reduce ambiguity → communicate constraints → iterate toward vision | Workflow model for Layer 2. Intent translation follows this sequence. |
| The director hires artists for their interpretive ability, not their obedience | Principle for Layer 2 and Layer 6. The COS should interpret intent, not blindly execute instructions. |

### 3.5 Story & Concept Artists

| Pattern | COS Application |
|---------|----------------|
| Generate-evaluate cycles (fundamental cognitive unit) | Process model for Layer 2. Creative work is a recursive generate-evaluate loop. |
| Thumbnail philosophy (cheap, fast, multiple options) | Output model for Layer 2. Early stages produce many cheap options, not one polished answer. |
| Exploration vs. Refinement as distinct cognitive modes | Mode model for Layers 2 and 7. The COS must know which mode it's in and apply different rules to each. |
| 3-5x cost ratio (changes at final stage cost 3-5x more than at sketch stage) | Economic model for Layer 3. The orchestration layer must prioritize early detection of problems. |
| Brief as starting point, not blueprint | Interpretation model for Layer 2. The COS must treat creative briefs as generative constraints, not executable instructions. |
| Quality signals for "done" (silhouette reads, emotional beats land, design solves brief problem) | Evaluation model for Layer 4. The COS needs learned heuristics for quality. |
| Structural feedback vs. surface feedback | Feedback model for Layer 7. The COS must distinguish between changes that require returning to exploration and changes that are within refinement scope. |

### 3.6 Technical Directors & Pipeline Engineers

| Pattern | COS Application |
|---------|----------------|
| Pipeline as "living system of connected decisions" | Definitional model: the COS is a pipeline for creative decisions, not just data. |
| Modular micro-pipelines with clean interfaces | Architecture model for all layers. Each layer has a well-defined input, output, and failure mode. |
| The "watchmaker mindset" (entire production as single interconnected machine) | Systems thinking requirement for Layer 3. The orchestration layer must see the whole production. |
| "The bug stops with the TD" | Ownership model for the COS. The system must own failures end-to-end. |
| Naming conventions encode metadata | Principle for Layer 5. All entities should be self-describing. |
| Bake validation into every data transfer point | Quality assurance model for all interface contracts. |
| Render farm as compute bottleneck exemplar | Resource management model for Layer 3. The COS must manage compute constraints. |
| Three production phases from pipeline perspective (pre-pro, production, finalling) | Phase model for Layer 3 with different rules per phase. Lock tools in finalling. |
| "Shotgun under the desk" (emergency recovery tools) | Resilience requirement for all layers. Every layer must have a bulletproof recovery path. |

---

## 4. Layer Architecture Overview

```
+---------------------------------------------------------------------+
|                        CREATIVE STACK                                |
|                                                                      |
|  +---------------------------+------------------------------------+  |
|  | Layer 1: Director         | Layer 7: Feedback &                |  |
|  | Experience Layer (DEL)    | Iteration Layer (FIL)              |  |
|  | - Communicate intent      | - Braintrust evaluations           |  |
|  | - Review output           | - Dailies rhythm                   |  |
|  | - Approve gates           | - Note tracking                    |  |
|  | - Configure system        | - Quality signals                  |  |
|  +---------------------------+------------------------------------+  |
|                                                                      |
|  +---------------------------------------------------------------+  |
|  | Layer 2: Creative Intent Layer (CIL)                           |  |
|  | - Intent decomposition                                         |  |
|  | - Brief generation                                             |  |
|  | - Exploration/refinement modes                                 |  |
|  | - Constraint management                                        |  |
|  +---------------------------------------------------------------+  |
+---------------------------------------------------------------------+
                              |
                              v
+---------------------------------------------------------------------+
|                      ORCHESTRATION STACK                             |
|                                                                      |
|  +---------------------------------------------------------------+  |
|  | Layer 3: Pipeline Orchestration Layer (POL)                    |  |
|  | - Workflow state machine                                       |  |
|  | - Stage transitions                                            |  |
|  | - Dependency resolution                                        |  |
|  | - Resource allocation                                          |  |
|  | - Gate management                                              |  |
|  +---------------------------------------------------------------+  |
|                                                                      |
|  +---------------------------------------------------------------+  |
|  | Layer 5: Asset & Production Management Layer (APML)            |  |
|  | - Asset versioning                                             |  |
|  | - Dependency graphs                                            |  |
|  | - Metadata management                                          |  |
|  | - Publishing/validation                                        |  |
|  | - Non-destructive layering                                     |  |
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
|  | - Quality heuristics                                           |  |
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
              +-------------------------------+
              | EXISTING TOOLS & ENGINES       |
              | Blender | Unreal | Houdini     |
              | Nuke    | Maya   | Substance   |
              | RenderMan | USD | ...          |
              +-------------------------------+
```

### Layer Summary Table

| # | Layer | Abbreviation | Primary Function | Analogy |
|---|-------|-------------|-----------------|---------|
| 1 | Director Experience Layer | DEL | Human-COS interaction | Director's chair — communicate, review, approve |
| 2 | Creative Intent Layer | CIL | Intent-to-brief translation | Story/concept artist — generate, evaluate, refine |
| 3 | Pipeline Orchestration Layer | POL | Workflow coordination | Production manager — track stage, manage handoffs |
| 4 | Knowledge & Quality Layer | KQL | Domain expertise | Pixar Braintrust + TD knowledge — what "good" means |
| 5 | Asset & Production Management Layer | APML | Asset lifecycle | USD + ShotGrid — version, track, publish |
| 6 | Tool Abstraction Layer | TAL | Tool integration | Pipeline TD — adapters, translation, execution |
| 7 | Feedback & Iteration Layer | FIL | Review cycles | Braintrust + Dailies — evaluate, note, iterate |

---

## 5. Layer 1: Director Experience Layer (DEL)

### 5.1 Responsibility

The Director Experience Layer is the **only interface through which human users interact with the COS**. It provides a director-centric UX that supports:
- Communicating creative intent (vision, tone, emotional goals)
- Reviewing work produced by the system (assets, sequences, renders)
- Giving structured and unstructured feedback
- Making approval decisions (gate sign-offs, final approvals)
- Configuring production parameters (scope, schedule, quality targets)
- Observing production status and progress

The DEL implements the **director UX model** — the entire system is designed to feel like working with a director's creative team, not like operating software.

### 5.2 Inputs Received

| Input Type | Source | Format | Description |
|-----------|--------|--------|-------------|
| Creative Vision | Human director | Look books, tone packets, verbal/recorded direction, reference collections, mood boards | High-level emotional and aesthetic intent |
| Briefs & Instructions | Human director | Structured briefs, verbal notes, annotated references | Specific creative direction for a task |
| Feedback & Notes | Human director | Verbal notes, markup, structured critiques, approval/rejection signals | Evaluative responses to produced work |
| Approval Decisions | Human director | Gate sign-offs, shot finals, milestone approvals | Authority decisions that advance production |
| Configuration | Human director | Project parameters, quality targets, priority assignments, constraint definitions | Production setup and ongoing tuning |
| Contextual Questions | Human director | Queries about status, options, trade-offs, history | Requests for system knowledge |

### 5.3 Outputs Produced

| Output Type | Destination | Format | Description |
|------------|-------------|--------|-------------|
| Structured Briefs | Layer 2 (CIL) | Formalized creative briefs with constraints, goals, references, quality criteria | Machine-readable version of director intent |
| Approval Events | Layer 3 (POL), Layer 7 (FIL) | Gate transitions, shot status changes, milestone completions | Signals that advance workflow state |
| Feedback Records | Layer 7 (FIL) | Categorized notes (structural vs. surface), intent clarifications, evaluation criteria | Tracked feedback items for iteration |
| Configuration State | All layers | Production parameters, quality thresholds, tool preferences, schedule constraints | Persistent configuration |
| Status Requests | Layer 3 (POL), Layer 5 (APML) | Progress queries, bottleneck reports, dependency checks | Dashboard and monitoring data |

### 5.4 Interface Contract

```yaml
layer: Director Experience Layer
input_contracts:
  - id: DEL-VISION
    type: Creative Vision Communication
    modalities: [look_books, tone_packets, verbal_direction, reference_collections, mood_boards]
    structural_rules:
      - "Must include emotional/aesthetic intent"
      - "May include specific constraints (must-haves)"
      - "May include open areas (creative freedom)"
    validation: "Vision must be evaluable — someone should be able to determine if output matches intent"
  - id: DEL-FEEDBACK
    type: Creative Feedback
    categories: [structural, surface, approval, rejection, intent_clarification]
    structural_rules:
      - "Structural feedback triggers re-entry into exploration mode in Layer 2"
      - "Surface feedback applies within current refinement mode"
      - "Approval/rejection signals are authoritative for Layer 3 state transitions"
    validation: "Feedback must be traceable to specific entities (shot, asset, sequence)"
output_contracts:
  - id: DEL-BRIEF
    destination: Layer 2 (CIL)
    schema:
      creative_goal: string
      constraints: [Constraint]
      references: [Reference]
      quality_criteria: [Criterion]
      open_areas: [string]
    validation: "Brief must contain at least one evaluable quality criterion"
  - id: DEL-APPROVAL
    destination: Layer 3 (POL), Layer 7 (FIL)
    schema:
      entity_id: string
      entity_type: [shot, asset, milestone, gate]
      decision: [approved, rejected, revise, conditionally_approved]
      conditions: [string]
    validation: "Approval decisions must be idempotent"
```

---

## 6. Layer 2: Creative Intent Layer (CIL)

### 6.1 Responsibility

The Creative Intent Layer is the **translation engine of the COS**. It takes high-level, often ambiguous creative direction from the Director Experience Layer and decomposes it into structured, actionable production requirements. This layer emulates the cognitive process of story artists and concept artists — it does not execute, it *interprets*.

Key responsibilities:
- **Intent decomposition:** Break "I want this scene to feel epic" into specific, evaluable criteria
- **Brief formalization:** Convert director communication into structured briefs that downstream layers can act on
- **Exploration vs. refinement mode management:** Support divergent thinking (generate many options) and convergent thinking (narrow and polish) as distinct modes
- **Constraint extraction:** Identify hard constraints (must-haves), soft constraints (preferences), and open areas (creative freedom) from director communication
- **Generate-evaluate cycles:** Produce multiple interpretations/variations for review before committing to a direction
- **Strategic sacrifice identification:** When constraints conflict, identify which elements can be compromised

### 6.2 Inputs Received

| Input Type | Source | Format | Description |
|-----------|--------|--------|-------------|
| Creative Vision | Layer 1 (DEL) | High-level aesthetic/emotional intent | Raw director communication |
| Structured Briefs | Layer 1 (DEL) | Formal briefs with constraints | Already-structured creative direction |
| Feedback Responses | Layer 7 (FIL) | Evaluations of generated interpretations | Signal to adjust intent decomposition |
| Context Knowledge | Layer 4 (KQL) | Domain expertise, style guides, quality signals | Knowledge to inform interpretation |
| Asset Context | Layer 5 (APML) | Existing assets, reference materials, production history | Context for generating new briefs |

### 6.3 Outputs Produced

| Output Type | Destination | Format | Description |
|------------|-------------|--------|-------------|
| Formal Creative Briefs | Layer 3 (POL) | Structured brief with goals, constraints, quality criteria, references | Machine-readable intent for execution |
| Interpretation Variations | Layer 7 (FIL) | Multiple candidate interpretations for director review | Exploration outputs |
| Constraint Specifications | Layer 3 (POL), Layer 4 (KQL) | Hard/soft constraints tagged to entities | Constraints that guide production decisions |
| Exploration Commands | Layer 3 (POL) | "Generate N variations of X within constraints Y" | Instructions for broad exploration |
| Refinement Commands | Layer 3 (POL) | "Polish selected variation X toward quality criteria Y" | Instructions for focused refinement |

### 6.4 Interface Contract

```yaml
layer: Creative Intent Layer
input_contracts:
  - id: CIL-VISION
    source: Layer 1 (DEL)
    type: Creative Intent
    processing: "Decompose into concrete, evaluable criteria"
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
output_contracts:
  - id: CIL-BRIEF
    destination: Layer 3 (POL)
    schema:
      brief_id: string
      project_id: string
      creative_goal: string
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
    validation:
      - "At least one required quality criterion must be evaluable by Layer 4"
      - "Hard constraints must be verifiable by Layer 6"
```

---

## 7. Layer 3: Pipeline Orchestration Layer (POL)

### 7.1 Responsibility

The Pipeline Orchestration Layer is the **central nervous system of the COS**. It manages the production workflow state machine, coordinates stage transitions, resolves dependencies, allocates resources, and enforces production gates. This layer embodies the TD's "watchmaker mindset" — seeing the entire production as a single interconnected machine.

Key responsibilities:
- **Workflow state machine:** Maintain authoritative production state — what stage is active, what entities are in what state
- **Stage transitions:** Manage handoffs between pipeline stages with validation, dependency checking, and notification
- **Gate management:** Enforce milestone gates (concept approved, vertical slice complete, alpha, beta, final)
- **Dependency resolution:** Track and resolve inter-stage and inter-asset dependencies
- **Resource allocation:** Manage computational and attention resources across active work items
- **Revision loop handling:** Support bidirectional data flow — upstream changes must propagate downstream
- **Pipeline configuration:** Adapt the pipeline structure to project type (film, game, VFX, TV)

### 7.2 Inputs Received

| Input Type | Source | Format | Description |
|-----------|--------|--------|-------------|
| Creative Briefs | Layer 2 (CIL) | Formalized intent | What to produce and under what constraints |
| Approval Events | Layer 1 (DEL) | Gate sign-offs, shot approvals | Authority decisions that advance workflow |
| Asset Events | Layer 5 (APML) | Publish notifications, version updates | Data state changes requiring orchestration |
| Quality Signals | Layer 4 (KQL) | Quality evaluations, "done" signals | Quality-based state change triggers |
| Feedback Events | Layer 7 (FIL) | Iteration completion signals | Feedback-driven workflow advancement |
| Resource Status | Layer 6 (TAL) | Tool availability, compute capacity, adapter health | Infrastructure state for allocation decisions |

### 7.3 Outputs Produced

| Output Type | Destination | Format | Description |
|------------|-------------|--------|-------------|
| Stage Commands | Layer 5 (APML), Layer 6 (TAL) | "Execute brief X in tool Y with parameters Z" | Work instructions for asset creation |
| State Transitions | Layer 1 (DEL), Layer 7 (FIL) | Entity state change events | Notifications of work progress |
| Dependency Events | Layer 5 (APML) | Dependency tracking updates, upstream change flags | Coordination signals for asset management |
| Gate Events | Layer 1 (DEL), Layer 7 (FIL) | Milestone reached/pending/blocked | Production rhythm notifications |
| Resource Requests | Layer 6 (TAL) | Compute allocation, tool instances, execution capacity | Infrastructure demands |
| Status Reports | Layer 1 (DEL) | Progress summaries, bottleneck alerts, schedule status | Dashboard data |

### 7.4 Pipeline Stage Model (Default)

The default pipeline stage model combines Pixar's 9-stage structure with VFX and game pipeline insights, designed to be configurable per project type:

```
Phase 1: CONCEPT & PRE-PRODUCTION
  1. Story & Intent Development
  2. Concept & Visual Development
  3. Technical Planning & R&D

Phase 2: PRODUCTION
  4. Asset Creation (Modeling, Surfacing, Rigging)
  5. Layout & Blocking
  6. Animation & Performance
  7. Effects & Simulation

Phase 3: POST-PRODUCTION & FINALLING
  8. Lighting & Rendering
  9. Compositing & Integration
  10. Quality Control & Delivery

Cross-cutting: FEEDBACK & ITERATION (active in all stages)
```

### 7.5 Interface Contract

```yaml
layer: Pipeline Orchestration Layer
state_machine:
  entities: [project, sequence, shot, asset, task]
  states: [created, in_progress, pending_review, approved, rejected, revising, complete, blocked]
  transitions:
    - from: created
      to: in_progress
      trigger: "Brief assigned + resources available"
    - from: in_progress
      to: pending_review
      trigger: "Work submitted for review"
    - from: pending_review
      to: approved
      trigger: "Layer 1 (DEL) approval"
    - from: pending_review
      to: revising
      trigger: "Layer 7 (FIL) structural feedback"
    - from: revising
      to: in_progress
      trigger: "Revision brief issued"
    - from: pending_review
      to: rejected
      trigger: "Layer 1 (DEL) rejection"
    # ... additional transitions in full spec
phase_model:
  pre_production:
    rules:
      - "Gate: Concept Approval required to enter Production"
      - "Vertical slice required before full production begins"
      - "R&D testing accounts for 12-18% of phase budget"
      - "Exploration mode is default in Layers 2 and 7"
  production:
    rules:
      - "Gate: Production Readiness required to enter Production"
      - "Ship 80% solutions, iterate live"
      - "Revision loops are expected and designed for"
      - "Tool chain is locked at Alpha gate"
  post_production:
    rules:
      - "Gate: Feature Complete required to enter Post-Production"
      - "Lock tools — no upgrades, no breaking changes"
      - "Surface feedback only — structural changes require Director override"
      - "Every change tracked with reversibility and approval"
```

---

## 8. Layer 4: Knowledge & Quality Layer (KQL)

### 8.1 Responsibility

The Knowledge & Quality Layer is the **persistent expertise layer** of the COS. It encodes the domain knowledge, quality heuristics, design principles, and evaluative criteria that guide creative production. This layer is the COS's equivalent of Pixar's Braintrust wisdom, the TD's technical knowledge, and the director's aesthetic judgment — made persistent and queryable.

Key responsibilities:
- **Domain expertise encoding:** Store and serve knowledge about creative domains (animation, VFX, game dev, compositing, etc.)
- **Quality heuristics:** Provide evaluative criteria for determining when work is "good enough" — learned from expert practice
- **Style guides:** Maintain persistent design language, color philosophy, shape language, and world-building rules per project
- **Cost-of-change models:** Provide economic models that quantify the cost of changes at different pipeline stages
- **Postmortem knowledge:** Accumulate lessons learned from completed projects — top 5 to repeat and top 5 to avoid
- **Constraint validation:** Evaluate whether proposed work adheres to project and domain constraints
- **Reference library:** Store and index visual, technical, and conceptual references

### 8.2 Inputs Received

| Input Type | Source | Format | Description |
|-----------|--------|--------|-------------|
| Domain Knowledge | External | Encoded expertise from specialist research, practitioner knowledge | Base knowledge about creative domains |
| Project Style Guide | Layer 1 (DEL) | Design language, color palette, world rules | Project-specific creative constraints |
| Quality Signals | Layer 7 (FIL) | Approval patterns, feedback history, "done" events | Learned quality heuristics from production |
| Postmortems | Layer 3 (POL) | Completed project retrospectives | Accumulated wisdom from past work |
| Reference Materials | Layer 1 (DEL), Layer 2 (CIL) | Visual references, tone references, technical references | Ground truth for creative direction |
| Constraint Definitions | Layer 2 (CIL) | Hard and soft constraints | Rules that creative work must satisfy |

### 8.3 Outputs Produced

| Output Type | Destination | Format | Description |
|------------|-------------|--------|-------------|
| Quality Evaluations | Layer 7 (FIL) | Assessments of work against quality criteria | Structured quality feedback |
| "Good Enough" Signals | Layer 3 (POL), Layer 7 (FIL) | Diminishing returns evaluations | Triggers for stage completion |
| Style Compliance Reports | Layer 3 (POL) | Adherence to project design language | Constraint satisfaction reports |
| Cost Estimates | Layer 3 (POL) | Predicted cost of proposed changes | Economic guidance for iteration decisions |
| Domain Guidance | Layer 2 (CIL) | Best practices, common patterns, production constraints | Knowledge to inform intent translation |
| Reference Recommendations | Layer 2 (CIL) | Suggested references based on creative goals | Knowledge-informed suggestion |
| Failure Prevention Warnings | Layer 3 (POL) | Early warnings of approaching failure modes | Proactive bottleneck prevention |

### 8.4 Interface Contract

```yaml
layer: Knowledge & Quality Layer
knowledge_domains:
  - animation_principles
  - composition_theory
  - color_theory
  - lighting_psychology
  - narrative_structure
  - character_design
  - environment_design
  - simulation_physics
  - rendering_optimization
  - pipeline_best_practices
  - project_management
quality_heuristics:
  - id: silhouette_readability
    domain: character_design
    evaluation: "Design must be recognizable in silhouette alone"
    weight: high
  - id: emotional_beat_clarity
    domain: narrative_structure
    evaluation: "Sequence must communicate intended emotional arc without dialogue"
    weight: high
  - id: diminishing_returns
    domain: general
    evaluation: "Signal when further refinement adds <5% improvement"
    weight: medium
  - id: reference_grounding
    domain: general
    evaluation: "Output should be 80% grounded in reference, 20% original spin"
    weight: medium
  - id: constraint_satisfaction
    domain: general
    evaluation: "Work meets all hard constraints and acceptable% of soft constraints"
    weight: high
output_contracts:
  - id: KQL-QUALITY-EVAL
    destination: Layer 7 (FIL)
    schema:
      entity_id: string
      criteria_evaluations:
        - criterion_id: string
          score: number  # 0.0 to 1.0
          confidence: number
          details: string
      overall_score: number
      "good_enough": boolean
      recommended_action: [approve, revise, structural_revision, reject]
    validation: "All required quality criteria must be evaluated"
  - id: KQL-COST-ESTIMATE
    destination: Layer 3 (POL)
    schema:
      change_type: [structural, surface, exploratory]
      current_stage: string
      estimated_cost: number  # relative to baseline (1.0 = stage-appropriate cost)
      cost_multiplier_explanation: string
      alternatives: [CostAlternative]
    validation: "Cost estimates must be stage-aware (3-5x multiplier for late-stage changes)"
```

---

## 9. Layer 5: Asset & Production Management Layer (APML)

### 9.1 Responsibility

The Asset & Production Management Layer is the **persistent data spine** of the COS. It manages the entire lifecycle of creative assets — versions, dependencies, metadata, publishing, and archival. Inspired by Pixar's USD (Universal Scene Description) and ShotGrid, and by Weta and ILM's storage architectures, this layer ensures that creative intent is never lost and that all contributions are traceable.

Key responsibilities:
- **Asset versioning:** Every asset has a version history. Versions are immutable once created.
- **Dependency graphs:** Track which assets depend on which. When an upstream asset changes, notify all downstream consumers.
- **Metadata management:** Every entity is self-describing. Metadata includes creator, creation time, dependencies, approval status, and creative intent references.
- **Publishing pipeline:** Formal publish process with validation, version bump, and downstream notification.
- **Non-destructive layering:** Multiple contributions to the same asset can coexist in layers (USD composition arc model).
- **Storage tier management:** Hot (active production), warm (recently active), nearline (reference), archival (completed).
- **Irreplaceable data protection:** Creative intent artifacts (briefs, decisions, feedback) are protected at highest tier. Reproducible artifacts (renders, caches) at lower tier.

### 9.2 Inputs Received

| Input Type | Source | Format | Description |
|-----------|--------|--------|-------------|
| Asset Creation Commands | Layer 3 (POL) | "Create new asset X in category Y" | Asset instantiation requests |
| Publish Events | Layer 6 (TAL) | Completed work ready for publishing | Versioned asset submissions |
| Dependency Declarations | Layer 3 (POL), Layer 6 (TAL) | Asset dependency specifications | Graph edge definitions |
| Metadata Updates | Layer 1 (DEL), Layer 2 (CIL) | Asset annotations, status changes, approval records | Entity metadata modifications |
| Recovery Requests | Layer 3 (POL) | Rollback/restore commands | Version recovery operations |
| Storage Configuration | Layer 1 (DEL) | Tier policies, retention rules, backup schedules | Storage lifecycle parameters |

### 9.3 Outputs Produced

| Output Type | Destination | Format | Description |
|------------|-------------|--------|-------------|
| Asset Versions | Layer 6 (TAL) | Versioned asset data with metadata | Consumable creative assets |
| Dependency Notifications | Layer 3 (POL) | Upstream change alerts | Coordination signals |
| Asset Status | Layer 1 (DEL), Layer 3 (POL) | Version history, dependency health, approval state | Asset lifecycle information |
| Validation Results | Layer 3 (POL), Layer 7 (FIL) | Integrity checks, naming compliance, metadata completeness | Quality gates for publishing |
| Backup/Recovery State | Layer 3 (POL) | Backup health, recovery point objectives, latest clean versions | Infrastructure status |

### 9.4 Interface Contract

```yaml
layer: Asset & Production Management Layer
entity_types: [project, sequence, shot, asset, task, version, dependency, metadata_record]
asset_lifecycle:
  states: [draft, in_progress, pending_review, approved, published, deprecated, archived]
  transitions:
    - from: draft
      to: in_progress
      trigger: "First edit saved"
    - from: in_progress
      to: pending_review
      trigger: "Submit for review command"
    - from: pending_review
      to: published
      trigger: "Approval event from Layer 1"
    - from: published
      to: deprecated
      trigger: "New version published"
    - from: published
      to: archived
      trigger: "Project completion + retention period elapsed"
publishing_contract:
  required_metadata:
    - asset_id
    - version_number
    - creator_or_source
    - creation_timestamp
    - dependencies: [asset_id, version_range]
    - approval_status
    - creative_intent_ref: "Reference to originating CIL brief"
    - checksum
  validation_gates:
    - "Naming convention compliance"
    - "Geometry integrity (no degenerate polygons, valid normals)"
    - "Texture path validity"
    - "Dependency version compatibility"
    - "Metadata completeness"
  storage_tiers:
    - id: hot
      performance: high
      use: active production
      protection: "Redundant, daily backup"
    - id: warm
      performance: medium
      use: recently active
      protection: "Redundant, weekly backup"
    - id: nearline
      performance: low
      use: reference assets
      protection: "Single copy, monthly backup"
    - id: archival
      performance: offline
      use: completed projects
      protection: "Glacier-style, quarterly verification"
  irreplaceable_vs_reproducible:
    protected_at_highest_tier: [briefs, feedback_records, approval_decisions, source_scene_files, animation_setups, shader_definitions]
    protected_at_lower_tier: [rendered_frames, simulation_caches, intermediate_exports, playblasts]
```

---

## 10. Layer 6: Tool Abstraction Layer (TAL)

### 10.1 Responsibility

The Tool Abstraction Layer is the **integration boundary** between the COS and all existing creative tools. It provides a unified adapter-based interface that insulates all upper layers from any specific DCC (Digital Content Creation) tool, game engine, or renderer. This is the layer that makes the COS platform-independent.

Key responsibilities:
- **Tool adapters:** Each supported tool has a driver/adapter that translates COS commands into tool-specific actions
- **Cross-DCC format translation:** Managed conversion between file formats (FBX, USD, Alembic, EXR, etc.) with data integrity checks
- **Command routing:** Dispatch COS commands to the correct tool based on capability registry
- **Tool capability registry:** Maintain a registry of what each tool can do, its version, available plugins, and performance characteristics
- **Execution environment management:** Launch/manage tool instances, monitor resource usage, handle crashes
- **Build vs. Buy vs. Hack decisions:** Framework for deciding when to build a custom adapter, use an existing connector, or create a temporary workaround

### 10.2 Inputs Received

| Input Type | Source | Format | Description |
|-----------|--------|--------|-------------|
| Execution Commands | Layer 3 (POL) | "Execute task X with parameters Y in appropriate tool Z" | Work instructions |
| Asset Data | Layer 5 (APML) | Versioned assets for consumption or modification | Data to operate on |
| Tool Capability Queries | Layer 3 (POL), Layer 2 (CIL) | "What tools can do X?" "Is tool Y available?" | Capacity and capability inquiries |
| Adapter Registration | External | Tool adapter packages | New tool integration |
| Configuration | Layer 1 (DEL) | Tool preferences, render settings, quality presets | Environment parameters |

### 10.3 Outputs Produced

| Output Type | Destination | Format | Description |
|------------|-------------|--------|-------------|
| Completed Work | Layer 5 (APML) | Published assets with metadata | Finished creative output |
| Tool Status | Layer 3 (POL) | Availability, load, error rates | Infrastructure telemetry |
| Capability Responses | Layer 2 (CIL), Layer 3 (POL) | Available tools for task X | Dispatch guidance |
| Execution Logs | Layer 3 (POL), Layer 7 (FIL) | Operation records, errors, warnings | Audit trail for quality evaluation |
| Resource Metrics | Layer 3 (POL) | Compute usage, render times, memory consumption | Performance data for orchestration |

### 10.4 Interface Contract

```yaml
layer: Tool Abstraction Layer
adapter_model:
  required_methods:
    - create_asset(asset_type, parameters) -> asset_id
    - execute_task(task_spec, asset_ref) -> result_ref
    - render(render_spec, asset_ref) -> render_result
    - preview(preview_spec, asset_ref) -> preview_result
    - get_capabilities() -> capability_list
    - get_status() -> status_report
    - validate_asset(asset_ref) -> validation_report
    - convert_format(source_ref, target_format) -> converted_ref
  adapter_contract:
    - "Must implement all required methods OR explicitly declare unsupported"
    - "Must report errors with COS error taxonomy, not tool-native errors"
    - "Must accept and return COS standard data formats, converting internally"
    - "Must be version-pinned — adapters specify exact tool version compatibility"
    - "Must include a health check endpoint"
supported_tool_categories:
  - modeling: [Blender, Maya, Houdini, ZBrush]
  - texturing_surfacing: [Substance Painter, Substance Designer, Mari, Photoshop]
  - rigging: [Maya, Blender, Houdini]
  - animation: [Blender, Maya, Houdini, Unreal]
  - fx_simulation: [Houdini, Blender, Maya]
  - lighting: [Blender, Katana, Maya, Houdini]
  - rendering: [RenderMan, Arnold, V-Ray, Cycles, Unreal]
  - compositing: [Nuke, Fusion, After Effects, Blender]
  - game_engine: [Unreal, Unity, Godot]
  - tracking_matchmove: [3DEqualizer, PFTrack, Syntheyes]
  - audio: [Wwise, FMOD, Reaper]
format_translation:
  primary_interchange: "OpenUSD (Universal Scene Description)"
  secondary_formats: [FBX, Alembic, OBJ, EXR, PNG, HDR, WAV]
  translation_rules:
    - "Maintain data integrity checksum on every conversion"
    - "Log lossy conversions with specific warnings about lost data"
    - "Prefer lossless conversion paths where available"
build_vs_buy_framework:
  decision_factors:
    - time_to_solution
    - maintenance_burden
    - customization_need
    - integration_depth
    - strategic_value
    - show_specific_need
  build_triggers:
    - "Core competitive advantage"
    - "No commercial solution exists at required scale"
    - "Integration depth requires full control"
  buy_triggers:
    - "Common, well-solved problem"
    - "Not strategic to differentiate on"
    - "Mature commercial solution exists"
  hack_triggers_acceptable:
    - "One-off shot requirement"
    - "Temporary workaround for known bug with patch date"
    - "Bridge solution while permanent adapter is built"
  hack_triggers_unacceptable:
    - "Pipeline infrastructure"
    - "Version control or data management"
    - "Anything with implicit dependencies"
```

---

## 11. Layer 7: Feedback & Iteration Layer (FIL)

### 11.1 Responsibility

The Feedback & Iteration Layer is the **Braintrust-inspired quality engine** of the COS. It manages the full lifecycle of creative feedback — from collection through evaluation to iteration — while maintaining the critical separation of feedback from approval authority that makes Pixar's Braintrust so effective.

Key responsibilities:
- **Feedback collection:** Accept feedback from multiple sources (director, automated quality evaluations, domain knowledge, comparative analysis)
- **Feedback categorization:** Distinguish structural feedback (requires returning to exploration) from surface feedback (applies within current refinement)
- **Feedback-authority separation:** The feedback layer evaluates and recommends but does NOT have approval authority. Only Layer 1 (Director) approves.
- **Iteration tracking:** Maintain iteration history for every entity — what feedback drove each change, what versions were produced, what decisions were made
- **Dailies rhythm:** Manage regular review cadence, not just event-driven reviews
- **Note management:** Track notes through resolution, with responsibility assignment and deadline
- **Quality signal integration:** Use Layer 4's quality heuristics to supplement human feedback
- **"I'll Know It When I See It" support:** Enable convergent search by showing variations and collecting preference signals

### 11.2 Inputs Received

| Input Type | Source | Format | Description |
|-----------|--------|--------|-------------|
| Director Feedback | Layer 1 (DEL) | Structured notes, markup, verbal feedback, approval/rejection | Human evaluative input |
| Quality Evaluations | Layer 4 (KQL) | Automated quality scores, heuristic evaluations | Machine evaluative input |
| Asset Versions | Layer 5 (APML) | Work submitted for review | Artifacts under evaluation |
| State Transitions | Layer 3 (POL) | Entity status changes (in_progress, pending_review) | Workflow events that trigger review |
| Feedback History | Layer 5 (APML) | Past feedback records | Context for current evaluation |
| Iteration Limits | Layer 1 (DEL) | Max iteration counts, schedule constraints | Boundary conditions for iteration loops |

### 11.3 Outputs Produced

| Output Type | Destination | Format | Description |
|------------|-------------|--------|-------------|
| Structured Feedback | Layer 2 (CIL), Layer 3 (POL) | Categorized notes with action items | Guidance for revision |
| Quality Scores | Layer 1 (DEL) | Evaluations against criteria | Dashboard data for director |
| Iteration Recommendations | Layer 3 (POL) | "Revise", "Proceed to next stage", "Return to exploration" | Workflow state change suggestions |
| Iteration History | Layer 5 (APML) | Complete feedback-to-change traceability | Audit trail for quality tracking |
| "Done" Recommendations | Layer 3 (POL), Layer 1 (DEL) | "Good enough" evaluation for stage completion | Quality gate recommendations |
| Feedback Trend Analysis | Layer 4 (KQL) | Patterns in feedback data | Knowledge accumulation |

### 11.4 Interface Contract

```yaml
layer: Feedback & Iteration Layer
core_principle: "Feedback separated from authority — FIL evaluates and recommends, Layer 1 approves"
feedback_types:
  - id: structural
    description: "Changes that require returning to exploration mode"
    example: "The character's silhouette doesn't read as the intended personality"
    effect: "Triggers Layer 2 mode switch to exploration"
    cost_multiplier: "3-5x if late stage"
  - id: surface
    description: "Changes that apply within current refinement mode"
    example: "The character's hair color should be a shade darker"
    effect: "Applies within current refinement pass"
    cost_multiplier: "1x (stage-appropriate)"
  - id: approval
    description: "Authorization to advance to next stage"
    effect: "Triggers Layer 3 state transition"
  - id: rejection
    description: "Work does not meet quality bar"
    effect: "Returns to in_progress with revision brief"
  - id: intent_clarification
    description: "Creative direction needs refinement"
    effect: "Returns to Layer 2 for intent refinement"
review_rhythm:
  default: "Regular dailies — review at cadence, not just on submission"
  cadence_rules:
    pre_production: "Daily standup + weekly structured review"
    production: "Daily dailies + weekly milestone review"
    post_production: "Alternate-day reviews + milestone signoffs"
iteration_contract:
  max_iterations_before_escalation: number  # configurable per project
  escalation_path:
    - "FIL recommends escalation to Layer 1"
    - "Layer 1 determines: continue iterating, change approach, or accept current state"
  iteration_tracking:
    required_fields:
      - entity_id
      - iteration_number
      - feedback_items: [feedback_id, category, source, summary]
      - changes_made: [change_description]
      - decision: [continue, structural_restart, approve, abandon]
output_contracts:
  - id: FIL-FEEDBACK
    destination: Layer 2 (CIL), Layer 3 (POL)
    schema:
      entity_id: string
      feedback_items:
        - id: string
          category: [structural, surface, approval, rejection, intent_clarification]
          source: [human_director, automated_quality, domain_knowledge, comparative]
          summary: string
          action_items: [string]
          priority: [critical, high, medium, low]
          deadline: timestamp
      recommendation: [revise, proceed, return_to_exploration, escalate]
      recommendation_confidence: number
    validation: "Structural feedback must include trigger for Layer 2 mode switch"
```

---

## 12. Interface Contracts Between Layers

### 12.1 Layer Interface Map

```
DEL (1)  ←→  CIL (2)   via Briefs & Feedback
DEL (1)  ←→  POL (3)   via Approvals & Status
DEL (1)  ←→  FIL (7)   via Feedback & Quality Reports
DEL (1)  ←→  KQL (4)   via Style Guides & Configuration
DEL (1)  ←→  APML (5)  via Asset Status & Recovery
CIL (2)  →   POL (3)   via Formal Briefs
CIL (2)  →   FIL (7)   via Interpretation Variations (for review)
CIL (2)  ←→  KQL (4)   via Domain Guidance & Constraint Queries
POL (3)  →   APML (5)  via Asset Commands & Dependency Declarations
POL (3)  →   TAL (6)   via Execution Commands & Resource Requests
POL (3)  →   FIL (7)   via State Transitions & Workflows
POL (3)  ←→  KQL (4)   via Cost Estimates & Quality Signals
APML (5) ←→  TAL (6)   via Asset Publishing & Retrieval
APML (5) ←→  FIL (7)   via Asset Context & Feedback History
TAL (6)  ←→  FIL (7)   via Execution Logs & Error Reports
KQL (4)  →   FIL (7)   via Quality Evaluations
FIL (7)  →   CIL (2)   via Structured Feedback (with mode triggers)
FIL (7)  →   POL (3)   via Iteration Recommendations
FIL (7)  →   KQL (4)   via Feedback Trends & Quality Data
```

### 12.2 Standardized Interface Contract Template

Every interface between layers follows this contract template:

```yaml
interface_contract:
  id: string  # Unique identifier
  source_layer: string
  destination_layer: string
  direction: [unidirectional, bidirectional]
  call_type: [synchronous, asynchronous, event, streaming]
  data_format: string  # e.g., "JSON with schema X", "USD layer", "protobuf"
  schema_ref: string  # Reference to the full schema definition
  reliability:
    delivery_guarantee: [at_most_once, at_least_once, exactly_once]
    retry_policy: "Exponential backoff, max 3 retries"
    timeout: number  # milliseconds
  validation_rules: [string]  # List of rules that must pass
  error_handling:
    error_taxonomy_ref: string  # Reference to error taxonomy
    fallback_behavior: string
  security:
    authentication: string
    authorization_level: string
```

### 12.3 Key Interface Contracts (Detail)

#### Contract: DEL → CIL (Brief Submission)

```yaml
interface_id: IC-01
source: Director Experience Layer (Layer 1)
destination: Creative Intent Layer (Layer 2)
direction: unidirectional
call_type: asynchronous
data_format: "COS Brief Schema v1"
description: "Director submits creative direction for interpretation"
schema:
  brief_id: string (uuid)
  timestamp: string (ISO 8601)
  director_id: string
  project_id: string
  communication_modality: [look_book, tone_packet, verbal_transcript, reference_collection, mood_board, text]
  content:
    # Modality-specific content
    creative_goal: string
    emotional_intent: string
    references: [url or path]
    hard_constraints: [string]
    soft_constraints: [string]
    open_areas: [string]
    quality_aspirations: [string]
  context:
    existing_briefs: [brief_id]
    stage: string
    priority: [critical, high, normal, low]
validation:
  - "creative_goal must be non-empty"
  - "At least one reference OR one quality aspiration must be provided"
  - "Hard constraints must be mutually consistent"
```

#### Contract: CIL → POL (Formal Brief)

```yaml
interface_id: IC-02
source: Creative Intent Layer (Layer 2)
destination: Pipeline Orchestration Layer (Layer 3)
direction: unidirectional
call_type: synchronous
data_format: "COS Formal Brief Schema v1"
description: "Translated creative intent ready for production execution"
schema:
  brief_id: string
  derived_from: string  # Original DEL brief ID
  project_id: string
  mode: [exploration, refinement]
  execution_goal: string  # Concrete, executable goal
  domain: string
  constraints:
    hard:
      - id: string
        description: string
        verifiable_by: [kql, tal, apml]
    soft:
      - id: string
        description: string
        weight: number
  quality_criteria:
    required:
      - id: string
        criterion: string
        evaluation_method: [automated, human_review, comparative]
        threshold: number
    aspirational:
      - id: string
        criterion: string
  cost_of_change_priority: number
  references:
    primary: [url or path]
    secondary: [url or path]
validation:
  - "All hard constraints must reference a verifiable evaluation method"
  - "At least one quality criterion must reference KQL quality heuristic"
  - "Mode must be consistent with current pipeline phase"
```

#### Contract: FIL → CIL (Feedback with Mode Trigger)

```yaml
interface_id: IC-03
source: Feedback & Iteration Layer (Layer 7)
destination: Creative Intent Layer (Layer 2)
direction: unidirectional
call_type: asynchronous (event-driven or cadence-driven)
data_format: "COS Feedback Schema v1"
description: "Evaluative feedback that may trigger mode changes"
schema:
  entity_id: string
  feedback_batch_id: string
  items:
    - id: string
      category: [structural, surface, approval, rejection, intent_clarification]
      source: [human, automated_kql, comparative]
      summary: string
      severity: [critical, high, medium, low, info]
      triggers_mode_change: boolean
      recommended_action: string
      affected_constraints: [constraint_id]
      affected_criteria: [criterion_id]
  aggregate:
    structural_count: number
    surface_count: number
    overall_recommendation: [revise_proceed, return_to_exploration, escalate]
    confidence: number
validation:
  - "If structural_count > 0 AND entity is in refinement mode, trigger mode switch to exploration"
  - "Each structural feedback item must be accompanied by at least one alternative suggestion"
```

#### Contract: POL → APML (Asset Command)

```yaml
interface_id: IC-04
source: Pipeline Orchestration Layer (Layer 3)
destination: Asset & Production Management Layer (Layer 5)
direction: unidirectional
call_type: synchronous
data_format: "COS Asset Commands Schema v1"
description: "Orchestration commands for asset lifecycle management"
schema:
  command_id: string
  command_type: [create, publish, rollback, archive, lock, unlock, add_dependency, remove_dependency]
  timestamp: string
  origin_brief_id: string
  entity:
    type: [asset, shot, sequence, project]
    id: string (may be empty for create commands)
    parent_id: string
  parameters:
    # Command-specific parameters
    version_comment: string (for publish)
    rollback_target: string (version_id, for rollback)
    dependency_spec: (for add/remove_dependency)
      depends_on: entity_spec
      relationship_type: [requires, references, extends]
      version_constraint: string
  metadata:
    creator: string
    creative_intent_ref: string
validation:
  - "Create commands must include metadata sufficient for file naming convention"
  - "Publish commands must pass APML validation gates before acceptance"
  - "Rollback commands must reference an existing version in the asset's history"
```

#### Contract: POL → TAL (Execution Command)

```yaml
interface_id: IC-05
source: Pipeline Orchestration Layer (Layer 3)
destination: Tool Abstraction Layer (Layer 6)
direction: unidirectional
call_type: synchronous
data_format: "COS Execution Command Schema v1"
description: "Work execution instruction routed to appropriate tool"
schema:
  execution_id: string
  origin_brief_id: string
  task_type: string  # e.g., "model_character", "simulate_cloth", "render_shot"
  tool_preference: [string]  # Ordered list of preferred tools
  execution_parameters:
    input_assets: [asset_ref]
    output_spec:
      format: string
      resolution: string
      framerate: number
    quality_presets: string
    time_budget: duration
    compute_budget: string
  failure_handling:
    retry_count: number
    fallback_tool: string
    degradation_acceptable: boolean
validation:
  - "At least one preferred tool must be in the TAL capability registry"
  - "Input assets must be in published state in APML"
  - "Time and compute budgets must be realistic given tool capability"
```

---

## 13. Data Flow Architecture

### 13.1 Primary Creative Flow (Happy Path)

```
Director (Human)
    |
    | [1] Creative Vision (look books, tone packets, verbal direction)
    v
Layer 1: DEL  ──►  Layer 2: CIL
    |                 |
    |                 | [2] Decompose intent, generate interpretations
    |                 | [3] Send variations to FIL for review
    |                 v
    |              Layer 7: FIL  ──►  Layer 1: DEL
    |                                    |
    | [4] Director selects direction     |
    |◄───────────────────────────────────|
    v
Layer 2: CIL
    |
    | [5] Formal brief generated
    v
Layer 3: POL
    |
    | [6] Orchestrate: determine stage, allocate resources
    | [7] Send execution commands
    ├────► Layer 5: APML (asset tracking)
    └────► Layer 6: TAL (tool execution)
              |
              | [8] Tool produces work
              v
Layer 5: APML (asset published)
    |
    | [9] Published asset available for review
    v
Layer 7: FIL
    |
    | [10] Evaluate against quality criteria (KQL)
    | [11] Send feedback to director
    v
Layer 1: DEL
    |
    | [12] Director reviews, gives feedback, or approves
    v
[Loop back to step 5 for revision OR proceed to next stage]
```

### 13.2 Feedback Loop Flow (Core Iteration)

```
Layer 1: DEL (Director Feedback)
    |
    v
Layer 7: FIL
    |
    |─ Categorize: Structural or Surface?
    |─ If structural: trigger Layer 2 mode switch to exploration
    |─ If surface: route to Layer 2 refinement or Layer 6 direct edit
    |─ Add to iteration tracking
    |─ Check: Max iterations reached?
    |   ├── Yes: Escalate to Layer 1 for decision
    |   └── No: Route feedback to appropriate layer
    v
Layer 2: CIL (revised brief) OR Layer 6: TAL (direct tool execution)
    |
    | [New work produced]
    v
Layer 5: APML (new version)
    |
    v
Layer 7: FIL (re-evaluate)
    |
    v
Layer 1: DEL (review again)
```

### 13.3 Knowledge Flow (Learning)

```
Layer 7: FIL
    |
    | [Feedback history, quality scores, iteration patterns]
    v
Layer 4: KQL
    |
    |─ Update quality heuristics
    |─ Recognize patterns in feedback
    |─ Refine "good enough" thresholds
    |─ Accumulate postmortem knowledge
    |─ Update cost-of-change models
    v
[Knowledge available for future projects via Layer 4 query]
```

### 13.4 Dependency Propagation Flow

```
Layer 3: POL detects upstream asset change
    |
    v
Layer 5: APML queries dependency graph
    |
    | [Find all downstream entities affected]
    v
Layer 3: POL
    |
    |─ Notify affected entities
    |─ Flag as "stale" or "needs_revision"
    |─ Re-enter affected entities into pipeline
    |─ Check: Can automated propagation resolve?
    |   ├── Yes: Dispatch auto-update via TAL
    |   └── No: Escalate to Layer 1 for creative decision
    v
Layer 1: DEL (Director notified of cascade)
```

---

## 14. Dependency Graph

### 14.1 Layer Dependency Matrix

```
Layer  ↓ depends on →   DEL(1)  CIL(2)  POL(3)  KQL(4)  APML(5) TAL(6)  FIL(7)
─────────────────────────────────────────────────────────────────────────────
DEL(1)                   ─       No      No      Config   Read     No      No
CIL(2)                   Read    ─       No      Read     Read    Capabil. Read
POL(3)                   Read    Read    ─       Read     Read     Read    Read
KQL(4)                   Config  No      No      ─       Read     No      Read
APML(5)                  Read    Read    Read    No      ─       Read    Read
TAL(6)                   No      No      Read    No      Read    ─       No
FIL(7)                   Read    Write   Write   Read    Read     Read    ─
```

**Legend:**
- `Read` = Layer reads data from the column layer
- `Write` = Layer sends data to the column layer
- `Config` = Layer reads configuration from the column layer
- `Capabil.` = Layer queries capabilities from the column layer
- `No` = No direct dependency
- `─` = Self (not applicable)

### 14.2 Critical Paths

The following dependency paths are the most latency-critical for the COS:

1. **Director review path:** DEL(1) → FIL(7) → KQL(4) → APML(5) → TAL(6) — The path from director feedback to tool execution
2. **Brief-to-execution path:** DEL(1) → CIL(2) → POL(3) → [APML(5), TAL(6)] — The path from creative vision to production
3. **Feedback loop back:** TAL(6) → APML(5) → FIL(7) → [CIL(2), DEL(1)] — The path from tool output back to creative decision
4. **Quality evaluation path:** APML(5) → FIL(7) → KQL(4) → FIL(7) → DEL(1) — The path from published asset to quality assessment

### 14.3 Dependency Rules

```
RULE 1: No layer above Layer 6 (TAL) may directly depend on any specific tool, engine, or file format.
  - This is THE fundamental architecture rule.
  - All tool-specific knowledge is encapsulated in Layer 6 adapters.

RULE 2: Layer 7 (FIL) must NOT have approval authority.
  - The Braintrust pattern: FIL evaluates and recommends. Only DEL (Director) approves.
  - This prevents feedback from becoming a command, maintaining psychological safety.

RULE 3: Layer 3 (POL) must maintain a complete, authoritative state of all entities.
  - No other layer may override POL state.
  - APML tracks data state; POL tracks workflow state.

RULE 4: Layer 4 (KQL) is read-mostly for all layers except Layer 7.
  - Most layers query knowledge. Only Layer 7 writes new knowledge (feedback trends).
  - Director writes configuration (style guides) via DEL.

RULE 5: Layer 5 (APML) is the single source of truth for asset data.
  - All asset creation, modification, publishing, and retrieval goes through APML.
  - No layer caches asset data without APML invalidation protocol.

RULE 6: Layer 1 (DEL) is the ONLY entry point for human interaction.
  - No other layer has a direct human interface.
  - This ensures all human input is routed through the director UX model.
```

---

## 15. Concepts Mapped from Specialist Research

### 15.1 Role-to-Layer Mapping

| Human Role | Primary COS Layer | Why |
|------------|------------------|-----|
| Film Director / Game Director / Showrunner | Layer 1 (DEL) | They communicate intent, review work, give feedback, and approve. This IS the director UX model. |
| Story Artist / Concept Artist | Layer 2 (CIL) | They translate vision into visual briefs, generate exploration options, and refine into production-ready direction. |
| Production Manager / Producer | Layer 3 (POL) | They manage workflow, stage transitions, resources, and gates. |
| VFX/CG Supervisor | Layer 3 (POL) + Layer 7 (FIL) | They coordinate technical execution AND evaluate quality. |
| Pipeline TD / Technical Director | Layer 6 (TAL) + Layer 5 (APML) | They build the adapter infrastructure, manage data flow, and enforce pipeline rules. |
| Pixar Braintrust | Layer 7 (FIL) + Layer 4 (KQL) | They provide feedback (FIL) based on accumulated wisdom (KQL) without authority to mandate changes. |
| Animation Supervisor / Department Lead | Layer 7 (FIL) | They are the first quality filter — approving internal rounds before director review. |
| Rendering TD / Render Wrangler | Layer 6 (TAL) | They manage the render farm and tool execution infrastructure. |
| R&D / Research Scientist | Layer 4 (KQL) | They push the frontiers of knowledge that the system uses for quality evaluation. |

### 15.2 Pipeline Stage Mapping

| Pixar Stage | COS Stage | Primary Layer |
|-------------|-----------|---------------|
| Story & Art | 1. Story & Intent Development | Layer 2 (CIL), Layer 7 (FIL) |
| Modeling | 4. Asset Creation (Modeling) | Layer 6 (TAL) via Layer 3 (POL) |
| Rigging | 4. Asset Creation (Rigging) | Layer 6 (TAL) via Layer 3 (POL) |
| Surfaces | 4. Asset Creation (Surfacing) | Layer 6 (TAL) via Layer 3 (POL) |
| Sets & Cameras | 5. Layout & Blocking | Layer 6 (TAL) via Layer 3 (POL) |
| Animation | 6. Animation & Performance | Layer 6 (TAL) via Layer 3 (POL) |
| Simulation | 7. Effects & Simulation | Layer 6 (TAL) via Layer 3 (POL) |
| Lighting | 8. Lighting & Rendering | Layer 6 (TAL) via Layer 3 (POL) |
| Rendering | 8. Lighting & Rendering | Layer 6 (TAL) via Layer 3 (POL) |

### 15.3 Key Pattern Implementations

| Pattern | Where in COS | Implementation |
|---------|-------------|---------------|
| Braintrust | Layer 7 (FIL) | Feedback evaluation runs independently from authority. FIL cannot approve; only DEL can. |
| Dailies | Layer 7 (FIL) + Layer 1 (DEL) | Regular review cadence. FIL aggregates work for review; DEL reviews at rhythm. |
| Generate-Evaluate | Layer 2 (CIL) + Layer 7 (FIL) | CIL generates multiple interpretations; FIL evaluates against quality signals from KQL. |
| Thumbnail Philosophy | Layer 2 (CIL) | Exploration mode produces many cheap, fast options. No commitment to any until director selects. |
| 3-5x Cost Ratio | Layer 4 (KQL) + Layer 3 (POL) | KQL provides cost models; POL uses them to prioritize early exploration. |
| Strategic Sacrifice | Layer 2 (CIL) | When constraints conflict, CIL identifies which elements can be compromised. |
| 80/20 Solution | Layer 3 (POL) | Production mode ships 80% solutions and iterates live. |
| Modular Micro-Pipelines | All layers | Each layer has well-defined input/output contracts, isolated failure domains, independent versioning. |
| Build vs. Buy vs. Hack | Layer 6 (TAL) | Framework for tool adapter decisions based on strategic value, maintenance burden, and time pressure. |
| Non-Destructive Layering | Layer 5 (APML) | USD-inspired composition arcs — multiple contributions coexist without overwriting. |
| Feedback-Authority Separation | Layer 7 (FIL) vs. Layer 1 (DEL) | Core Braintrust pattern. FIL recommends; DEL decides. |
| Exploration vs. Refinement | Layer 2 (CIL) | Two distinct modes with different rules. FIL feedback can trigger mode transitions. |

---

## 16. Architectural Decision Records (ADRs)

### ADR-001: Seven Layers vs. Alternative Layer Counts

**Status:** Accepted  
**Context:** Must determine the optimal number of layers that balances separation of concerns with system complexity.  
**Decision:** Seven layers organized into three stacks (Creative, Orchestration, Infrastructure).  
**Rationale:** Fewer than 5 layers would collapse distinct responsibilities (e.g., knowledge and feedback are fundamentally different), creating monolithic layers. More than 9 layers would create excessive indirection for the value provided. Seven layers map cleanly to the seven core responsibilities: interact, translate, orchestrate, know, manage assets, integrate tools, and evaluate feedback.  
**Alternatives considered:** 5-layer (combined KQL+APML), 9-layer (split POL into workflow+resources), 4-layer (merged creative stack).

---

### ADR-002: Director Experience Layer as Sole Human Interface

**Status:** Accepted  
**Context:** Multiple layers could expose human interfaces (e.g., technical configuration UI in Layer 6, direct asset browsing in Layer 5).  
**Decision:** Layer 1 (DEL) is the ONLY human interface. All human interaction routes through the director UX.  
**Rationale:** Prevents fragmentation of the user experience. Ensures consistent director-centric design. Forces all human input through the intent translation pipeline, preventing bypass of creative quality processes. Directors should never need to touch infrastructure layers directly.  
**Consequence:** Layer 6 and Layer 5 must expose rich APIs for DEL to provide configuration and monitoring UIs. Infrastructure layers must be fully automatable.

---

### ADR-003: Feedback-Authority Separation (Braintrust Pattern)

**Status:** Accepted  
**Context:** How does the COS evaluate quality without becoming a bottleneck or creating fear of judgement?  
**Decision:** Layer 7 (FIL) evaluates, recommends, and tracks — but NEVER approves. Only Layer 1 (DEL) has approval authority.  
**Rationale:** This is the core insight from Pixar's Braintrust. When feedback has no authority, recipients accept it more openly. When a director (or the Director layer) makes the final decision, they own the outcome. This prevents the COS from becoming a "mandating system" that kills creative risk-taking.  
**Consequence:** FIL must be confident in its recommendations but humble in their presentation. The system must clearly distinguish "this is good enough" (FIL recommendation) from "this is approved" (DEL decision).

---

### ADR-004: Platform Independence Through Tool Abstraction Layer

**Status:** Accepted  
**Context:** The COS must work across Blender, Unreal, Houdini, Nuke, Maya, and any future tool without upper-layer changes.  
**Decision:** Layer 6 (TAL) is the sole tool-dependent layer. All layers above use tool-agnostic interfaces. Tools are integrated via adapters that implement a standard contract.  
**Rationale:** This adapter pattern is proven in operating systems (POSIX, HAL), game engines (render abstraction layers), and VFX pipelines (USD). It insulates the core architecture from tool churn and enables incremental adoption.  
**Consequence:** Adapter development is the primary integration cost. Each new tool requires an adapter implementing the standard contract. The adapter contract must be stable but extensible.

---

### ADR-005: Knowledge Layer as Separate Persisted Store

**Status:** Accepted  
**Context:** Quality heuristics, domain knowledge, and style guides could be hardcoded into Layer 7 or maintained as configuration by Layer 1.  
**Decision:** Layer 4 (KQL) is a separate, persistent knowledge layer that accumulates learning across projects.  
**Rationale:** Knowledge is distinct from both feedback (FIL) and configuration (DEL). It must accumulate over time, be shared across projects, and be queryable by multiple layers. Embedding it in FIL would conflate evaluation with knowledge. Embedding it in DEL would make it per-project and unreusable.  
**Consequence:** KQL requires its own storage, update mechanism, and query API. It must support incremental learning from FIL feedback trends.

---

### ADR-006: Default Pipeline Stage Model is Configurable

**Status:** Accepted  
**Context:** Different project types (film, game, VFX, TV) have different optimal pipeline stages. A fixed pipeline would be too rigid.  
**Decision:** The default 10-stage pipeline model (based on Pixar's 9-stage model + VFX/game insights) is configurable. Projects can add, remove, or reorder stages. Layer 3 (POL) takes a pipeline definition as a parameter.  
**Rationale:** No single pipeline fits all creative production. A film needs different stages than a game or a VFX sequence. Making the pipeline configurable respects the "platform-independent" principle at the workflow level.  
**Consequence:** POL must treat the pipeline definition as data, not code. The stage model, transition rules, and gate criteria must be declaratively configurable. The 10-stage model serves as the default but is not the only option.

---

### ADR-007: Asset Management Uses Non-Destructive Layering (USD Model)

**Status:** Accepted  
**Context:** Multiple departments contribute to the same assets. Sequential overwriting causes data loss.  
**Decision:** Layer 5 (APML) implements non-destructive layering inspired by Pixar's USD composition arcs. Contributions from different sources coexist in layers rather than being flattened.  
**Rationale:** This is the proven industry solution (USD, Photoshop layers, Nuke nodes). It enables parallel work, parallel review, and non-destructive iteration. Without it, every revision risks losing previous work.  
**Consequence:** APML must implement a layer composition engine. Assets have layer stacks, not just version histories. Publishing creates a new layer, not a new file overwrite.

---

## 17. Open Questions and Future Work

### 17.1 Architecture Questions

1. **How does the COS handle the "messy middle" — when later pipeline stages need earlier assets that are still being revised?** Pixar handles this with USD's non-destructive layering, but the COS needs a strategy for version pinning, branching, and parallel workflows.

2. **What is the right granularity for the pipeline stage model?** Should the COS default to Pixar's 9 stages, VFX's 18 stages, or a hybrid 10-stage model? Answer may depend on project type.

3. **How does the COS manage cross-project knowledge transfer?** The TD "casting" system naturally spreads knowledge. The COS needs an equivalent mechanism — perhaps automatic postmortem analysis and cross-project quality heuristic updates.

4. **Should the COS support a "showrunner layer" above the director?** In TV and games, showrunners manage multiple projects. This might be a future layer above DEL or a configurable mode of DEL.

5. **How does the COS handle the "IKIWISI" problem — when the director can only recognize quality when they see it?** Layer 2's generate-evaluate cycle addresses this, but the mechanism for convergent search without a clear target needs more design.

6. **What is the authentication/authorization model for multiple human roles?** DEL currently assumes one director. Real productions have multiple stakeholders (client, director, producer, leads). Multi-role auth is future work.

### 17.2 Implementation Questions

7. **Which layer should be implemented first?** Likely Layer 3 (POL) and Layer 5 (APML), as they provide the foundational infrastructure that all other layers depend on. Followed by Layer 6 (TAL) with a single tool adapter (Blender or Unreal) for proof of concept.

8. **How much of Layer 2 (CIL) requires LLM/AI vs. deterministic processing?** Intent decomposition likely requires AI. Constraint extraction and brief formalization may be hybrid — AI for interpretation, deterministic for formatting.

9. **What is the storage backend for Layer 5 (APML)?** USD-native for scene data + relational database for metadata + file store for published assets. Exact stack TBD.

10. **How does the COS handle real-time vs. offline tools?** Unreal Engine is real-time; RenderMan is offline. The TAL adapter contract must handle both synchronous and asynchronous execution models.

### 17.3 Research Gaps

11. **Cost-of-change models need empirical validation.** The 3-5x ratio from concept art may not apply to all creative domains. Need domain-specific cost models.

12. **Quality heuristics are domain-specific.** Layer 4 (KQL) currently has a few general heuristics. Each creative domain needs its own set, derived from practitioner knowledge.

13. **The "director UX" needs user research.** Is the director persona accurate for all COS users? What about producers, art directors, or individual artists? More research needed on who interacts with the system and how.

14. **How does the COS handle multi-project orchestration?** The current architecture assumes one project per COS instance. Real studios run multiple projects concurrently, sharing resources and talent. This is future scope.

### 17.4 Next Steps (Recommended)

1. **Implement Layer 3 (POL) state machine** — Proof of concept with a simple 5-stage pipeline
2. **Implement Layer 5 (APML) basic asset management** — Versioning, publishing, dependency tracking
3. **Implement one Layer 6 (TAL) adapter** — Blender or Unreal Engine as the first integrated tool
4. **Prototype Layer 1 (DEL) minimal UX** — Brief submission and approval workflow
5. **Prototype Layer 7 (FIL) feedback loop** — Basic note tracking and iteration management
6. **Integrate Layer 4 (KQL) minimal quality heuristics** — Silhouette readability and constraint satisfaction
7. **Prototype Layer 2 (CIL) basic intent decomposition** — Translate a single brief into structured requirements

---

*End of COS Architecture v1 Document*

---

## Appendix A: Document Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-06-14 | COS Architecture Agent | Initial architecture document — 7 layers, interface contracts, data flows, pattern mappings |

## Appendix B: File Metadata

- **Path:** `C:\Users\USER\OneDrive\Documents\Creative_Operating_System\01_Capability_Architecture\COS_Architecture_v1.md`
- **Size:** ~2,500 lines
- **Status:** First Draft — Ready for Review
- **Prerequisites:** All 6 documents in `02_Specialist_Architecture/`
- **Next Document:** `02_Capability_Architecture/COS_Interface_Spec_v1.md` (detailed API specifications)
