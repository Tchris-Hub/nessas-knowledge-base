# Architecture-Changing Discoveries
## What Findings Would Fundamentally Alter the Creative Operating System Design

**Document ID:** COS-11-DA-002
**Version:** 1.0
**Date:** June 14, 2026
**Status:** Complete
**Purpose:** Force identification of hidden assumptions, potential breakthroughs, known unknowns, highest-impact research, and roadmap-altering findings

---

## Table of Contents

1. [Hidden Assumptions — What We Believe That Could Be Wrong](#1-hidden-assumptions)
2. [Potential Breakthroughs — Discoveries That Would Dramatically Simplify or Improve the Architecture](#2-potential-breakthroughs)
3. [Known Unknowns — What We Don't Know That Could Fundamentally Change the Design](#3-known-unknowns)
4. [Highest Architectural Impact Research — Which Document Would Change the Architecture Most If Wrong](#4-highest-architectural-impact-research)
5. [Roadmap-Changing Discoveries — What Research So Far Suggests a Different Priority Order](#5-roadmap-changing-discoveries)

---

## 1. Hidden Assumptions — What We Believe That Could Be Wrong

### A1: The 7-Layer Vertical Stack Is the Right Decomposition

**Current belief:** The COS is organized as 7 distinct layers (DEL, CIL, POL, KQL, APML, TAL, FIL) in three stacks (Creative, Orchestration, Infrastructure), with strict interface contracts between them and unidirectional data flow from top to bottom with feedback loops.

**What would change if wrong:** If the 7-layer separation introduces unacceptable latency or rigidity, the architecture might need to collapse layers (e.g., merging KQL into FIL, or APML into POL) or adopt a flat capability bus model where layers are logical groupings rather than architectural boundaries. The entire interface contract system (IC-01 through IC-19 in COS_Architecture_v1.md §12) would need redesign.

**Source:** COS_Architecture_v1.md (§4-§11) — the entire layer architecture.

**Current confidence:** 65% — based on specialist research patterns (Pixar's 9-stage pipeline maps well but the VFX 18-stage model suggests more granularity might be needed). The 7 layers feel right for initial decomposition but have not been tested against real multi-tool production workflows.

**Research to validate/invalidate:** Build a functional vertical slice through all 7 layers for the Storyboard workflow (recommended first workflow from Smallest_Viable_COS.md). Measure latency between each interface. If end-to-end time from intent to output exceeds what a single specialist (human or AI) would need for the same task, the layer overhead is too high.

---

### A2: The 23-Specialist Hierarchy Is the Right Granularity

**Current belief:** The Specialist Hierarchy (Specialist_Hierarchy.md) reduced 37-57 flat agents to 23 structured specialists across 4 tiers (9 Core, 6 Integrated, 5 Support, 3 Direction), based on 6 criteria (knowledge overlap, communication frequency, decision coupling, dependency direction, bottleneck analysis, failure isolation).

**What would change if wrong:** If the 8 strategic mergers (C06+C07+V08, V07+A05+C08+C09, etc.) are wrong, the system would either have too many agents (original 37-57 overhead) or the merged specialists would lack sufficient domain depth. For example, if the Surface & Material Artist (merged from Texture+Shading+Lookdev) actually requires distinct expertise that can't be combined, you'd need to split it back into 3 agents. Conversely, if additional mergers are possible (e.g., Layout+Lighting, or Animator+SimTD), the hierarchy would shrink further.

**Source:** Specialist_Hierarchy.md (§Proposed Hierarchy, §Summary). Each merger is justified by 6 criteria with specific evidence.

**Current confidence:** 70% — the 6 criteria analysis is rigorous, but it is based entirely on theoretical dependency analysis, not empirical performance data. The C04 DigitalModeler bottleneck (10 connections) and V04 LayoutArtist bottleneck (7 connections) are well-supported. The question is whether merged specialists (e.g., Surface & Material Artist) can actually produce output that meets professional quality standards.

**Research to validate/invalidate:** Prototype 2-3 merged specialists (surface & material, simulation & FX, environment world-builder) and measure: (a) quality of output vs. separate specialists, (b) iteration speed, (c) handoff overhead eliminated vs. new complexity created. Compare against the guarded assumptions stated in the hierarchy document (e.g., "30-40% reduction in material iteration time" for M1).

---

### A3: The Director-UX Model Is the Right Interaction Paradigm

**Current belief:** The COS user is a "Director" — they communicate intent, review output, give feedback, and make approval decisions. The DEL (Layer 1) is a director-centric interface that mimics working with a creative team.

**What would change if wrong:** If users actually want to be hands-on artists (not directors), the DEL would need to expose specialist-level controls — a "switch to artist mode" that lets users directly manipulate models, textures, or renders. If users want collaborative multi-user workflows (multiple directors, department leads reviewing simultaneously), the single-Director model breaks down. If non-experts find the "director" role intimidating or confusing, the UX model needs fundamental redesign.

**Source:** Three_Organizational_Models.md (§7.2 — Hybrid Layered Model), Decision_Architecture.md (§2.1 — Director as Ultimate Authority), Assumptions.md (C3 — "The director/curator role may be the right UX model").

**Current confidence:** 60% — supported by analogy to real studios (directors do exist) but untested with actual users. The Assumptions document (B1) explicitly questions whether a single non-expert user can effectively direct complex creative production.

**Research to validate/invalidate:** User studies with 10-20 potential users across the expertise spectrum (novice to professional). Test whether the Director mental model resonates. Key question from Open_Questions.md (Q9): "Does the system adapt to the user's creative sophistication?"

---

### A4: Feedback-Can Be Cleanly Separated from Approval Authority

**Current belief:** The Braintrust model's central insight — feedback authority separated from decision authority — is the most important architectural principle. The FIL (Layer 7) evaluates and recommends; the DEL (Layer 1) approves. This separation is enforced at the data flow level (Creative_Roles_as_Functions.md, §1).

**What would change if wrong:** If feedback without authority causes the system to produce bland, unhelpful critiques ("the Braintrust has no teeth"), the architecture would need to give FIL limited decision authority for low-impact decisions. If the separation introduces unacceptable latency (feedback must go through Director even for trivial corrections), the architecture needs delegation paths that bypass the Director for surface-level feedback while preserving the separation for structural feedback.

**Source:** Creative_Roles_as_Functions.md (§2 — Braintrust has ZERO decision authority), Decision_Architecture.md (§3.1 — "Feedback flows UP to the Director. Decisions flow DOWN from the Director."), COS_Architecture_v1.md (§11 — FIL interface contract).

**Current confidence:** 75% — well-supported by Pixar case studies (WALL-E saved by Braintrust feedback). But Pixar's Braintrust has expert human members; an AI feedback system may lack the credibility to make "no authority" work. The psychological safety contract (Creative_Roles_as_Functions.md §2.8 — AuthorityLeak failure mode) is designed for humans.

**Research to validate/invalidate:** Build the feedback system with strict separation. Measure: (a) Director acceptance rate of feedback, (b) quality of output with vs. without the separation, (c) whether Directors override automated feedback as often as they should.

---

### A5: The Linear Pipeline Metaphor (Stages → Output) Is Sufficient

**Current belief:** The COS enforces a pipeline stage model (Concept → Pre-Production → Production → Post-Production → Delivery) with gates between stages. Each stage has defined entrance and exit criteria.

**What would change if wrong:** Open_Questions.md (Q1) explicitly asks: "Is the Creative Operating System a pipeline, a graph, a network, or something else?" If non-linear creation is the norm (users want "I want a cinematic shot" without preceding stages), the POL must support creation from any node, not just stage 1. If iteration between non-adjacent stages is common (e.g., lighting changes that force changes back to modeling), the "loop not line" principle demands bidirectional stage transitions, not just "return to previous stage."

**Source:** Open_Questions.md (Q1), COS_Architecture_v1.md (§7 — Pipeline Stage Model), VFX_House_Pipeline.md ("Pipeline is a loop, not a straight line"), Game_Studio_Pipeline.md (nested macro/micro pipelines).

**Current confidence:** 55% — the pipeline metaphor is explicitly questioned in Open Questions. Every studio research document describes "loops not lines." The 7-layer architecture already includes feedback loops (FIL), but the POL state machine (§7.5) still defaults to stage-by-stage progression.

**Research to validate/invalidate:** Map real creative workflows from practitioners. Count how many productions actually follow a linear path vs. how many skip/reorder stages. If >50% of real productions skip stages, the pipeline model needs fundamental revision.

---

### A6: 8 Capabilities Is the Right MVP Size

**Current belief:** The Smallest Viable COS needs 8 capabilities (D01, S04, V01, V03, V05, P05, FIL, P04) across 2 tools (Blender + COS Dashboard/CLI). This is based on the shortest dependency chain (S04→V01→V03→V05→P05 = 5 production capabilities + direction + infrastructure + quality).

**What would change if wrong:** If 8 capabilities produce output too simple to demonstrate the COS vision (a static environment render doesn't feel like "creative production"), the MVP needs to expand. If even 8 capabilities are too many to build and integrate realistically, the MVP needs to shrink further (e.g., drop V05/Lighting and use a simple render setup, reducing to 5-6 capabilities). If the Storyboard workflow (4 capabilities, 1 tool) is the right first step, the 8-capability MVP is actually Phase 2, not Phase 1.

**Source:** Smallest_Viable_COS.md (§Part 1 — 8 core capabilities), (§Part 2 — Storyboard as first workflow with 4 capabilities).

**Current confidence:** 45% — the document itself notes a tension: the MVP recommends environment chain (8 capabilities) but the recommended first workflow is storyboard (4 capabilities). If storyboard is mastered first, the environment MVP is actually Phase 2. The Storyboard workflow uses different capabilities (S02, S01) than the environment chain.

**Research to validate/invalidate:** Build the Storyboard workflow (4 capabilities, 1 tool) first. If it successfully demonstrates the COS vision (intent → multi-capability orchestration → feedback loop → quality evaluation → director-driven iteration), the 8-capability environment MVP is delayed to Phase 2.

---

### A7: The Hybrid Organizational Model (All Three Modes) Is Buildable

**Current belief:** The recommended architecture is a hybrid layered model (Three_Organizational_Models.md §7.2) that overlays three modes: Direct Mode (Model A), Studio Mode (Model C, default), and Pipeline Mode (Model B). Implementation phases go: v1.0 = Model A, v2.0 = Model A+Departments, v3.0 = Model C, v4.0 = Model B optional.

**What would change if wrong:** If building even one mode is extremely difficult, supporting three simultaneously may be infeasible. If Mode switching is cognitively confusing for users, the architecture should pick one mode. If the Graph Router (Model B) is the architectural core needed for all modes (as the hybrid model suggests in Layer 2), then the phased approach is wrong — Model B should come earlier, not last.

**Source:** Three_Organizational_Models.md (§7.2 — Hybrid Layered Model, §7.3 — Implementation Phasing).

**Current confidence:** 40% — the Three Organizational Models document is explicitly speculative. The comparison matrix shows Model B (Capability Network) has "10/10 Implementation Difficulty" and "10/10 System Complexity." Building three parallel interaction modes on top of a single architecture is an unproven approach.

**Research to validate/invalidate:** Prototype Mode switching (Direct ↔ Studio) with real users. Measure: (a) time to switch modes, (b) cognitive load during mode transitions, (c) whether users prefer one mode and stick with it. If users rarely switch, the hybrid model adds unnecessary complexity.

---

### A8: Quality Heuristics Can Be Automatically Learned and Applied

**Current belief:** The KQL (Layer 4) encodes quality heuristics (silhouette readability, emotional beat clarity, tonal consistency, etc.) that the FIL uses to evaluate work automatically. Quality scores are calculated (0.0-1.0) and presented to the Director alongside visual output.

**What would change if wrong:** If quality is fundamentally subjective and context-dependent (as Open_Questions.md Q8 suggests: "How does a system measure quality when quality is context-dependent?"), automated heuristics may produce consistently wrong evaluations that erode Director trust. If quality evaluation requires embodied experience (the "Would I watch this?" test — Creative_Decision_Systems.md §6.1.2), AI heuristics may never achieve sufficient validity.

**Source:** Decision_Architecture.md (§5 — Quality Evaluation Framework), COS_Architecture_v1.md (§8 — KQL quality heuristics), Creative_Decision_Systems.md (§6 — Quality Calibration).

**Current confidence:** 35% — the lowest confidence assumption. The Decision_Architecture.md document provides detailed quality signals (11 creative, 6 technical, 6 production) but admits they are "drawn from creative decision research" rather than empirically validated. The quality evaluation engine (§5.2) is described but has no implementation plan.

**Research to validate/invalidate:** Train quality heuristics on a labeled dataset of creative work (e.g., professional vs. amateur renders). Measure: (a) correlation between automated scores and human expert ratings, (b) Director trust in automated scores over time, (c) whether quality scores improve iteration outcomes vs. unstructured feedback.

---

### A9: The Director Can Define Quality Criteria at Brief Time

**Current belief:** The CIL brief schema (COS_Architecture_v1.md §6.4) requires at least one "evaluable quality criterion" per brief. The Director provides quality criteria alongside creative intent, and the KQL evaluates against them.

**What would change if wrong:** If Directors cannot articulate quality criteria at brief time (the "I'll Know It When I See It" problem — Directors & Creative Leadership pattern), the brief model is structurally broken. The system would need to infer quality criteria from past preferences, reference materials, and iterative feedback rather than requiring explicit criteria upfront.

**Source:** COS_Architecture_v1.md (§6.4 — CIL output contract: "At least one required quality criterion must be evaluable"), Directors & Creative Leadership research (IKIWISI pattern), Decision_Architecture.md (§5 — Quality Evaluation Framework).

**Current confidence:** 50% — the Directors research explicitly documents the IKIWISI problem ("I'll Know It When I See It"), which directly contradicts the assumption that Directors can pre-define quality criteria. The architecture currently builds on both assumptions simultaneously, which is contradictory.

**Research to validate/invalidate:** Study how real directors communicate quality expectations. Count how often they can articulate criteria upfront vs. needing to see options first. If >70% of quality direction happens after seeing output, the brief model needs to accept "explore and I'll tell you" as a valid input.

---

### A10: Specialist Capabilities Can Be Implemented as Independent AI Agents

**Current belief:** Each of the 23 specialists (or 47 capabilities) is an independently addressable AI agent with a clean interface contract. They communicate via structured data passing, not shared state.

**What would change if wrong:** If capabilities need shared context to work effectively (e.g., the Layout Artist needs to understand the Animator's performance constraints, not just receive scene data), the independent-agent model breaks down. The Three Organizational Models (Model B, Capability Network) already recognizes this by proposing a Graph Router with shared state. If capabilities cannot function without shared context, Model B becomes the only viable option, and the implementation must focus on the Graph Router from day one.

**Source:** Specialist_Hierarchy.md (§Tier 1 — independent specialists), Three_Organizational_Models.md (§3 — Capability Network with shared graph state), Assumptions.md (B2 — "Capabilities can be cleanly decomposed into independent modules").

**Current confidence:** 45% — the Assumptions document explicitly flags this as a questionable assumption. The dependency graph (Capability_Dependency_Map.md) shows that the tightest coupling (C06+C07+V08, V07+A05) has already been resolved through mergers, but the independent-agent model for remaining bottlenecks (C04, V04, V05, A01, C05) assumes that clean interfaces are sufficient.

**Research to validate/invalidate:** Implement 3 core specialists (e.g., DigitalModeler, Rigger, Animator) with clean interface contracts. Measure: (a) how often specialist A needs information not in the formal interface, (b) quality degradation from information loss at handoffs, (c) whether shared context improves output quality by >20%.

---

### A11: The Cost-of-Change Model (3-5x Late Stage) Is Universal

**Current belief:** Changes at the final pipeline stage cost 3-5x more than changes at the sketch stage (from Story_Concept_Artists.md pattern), and this multiplier is built into the POL and KQL as a universal heuristic.

**What would change if wrong:** If AI-powered creative tools change the economics (e.g., an AI can regenerate a final render from new parameters in seconds, not days), the cost multiplier collapses. The entire quality gate strategy (which tolerates lower quality early and enforces higher quality later) is based on the economics of human labor. If AI tools make late-stage changes cheap, the architecture should allow rework at any stage without penalty, collapsing the need for stage gates entirely.

**Source:** Story_Concept_Artists.md (3-5x cost ratio pattern), COS_Architecture_v1.md (§8.4 — Cost-of-change models), Decision_Architecture.md (§3.3 — Feedback types with cost multipliers).

**Current confidence:** 40% — the 3-5x multiplier is well-established for human production but unverified for AI-orchestrated production. An AI system that can regenerate a render from scratch in 30 seconds would fundamentally change the economics.

**Research to validate/invalidate:** Measure actual cost of late-stage changes in an AI production pipeline. If the multiplier is <2x for AI-assisted work, the entire gate-based progression model should be replaced with a continuous flow model.

---

### A12: The Tool Abstraction Layer Can Unify Disparate DCC Tools

**Current belief:** The TAL (Layer 6) provides a unified adapter interface that insulates all upper layers from specific DCC tools. It supports format translation (USD primary, FBX/Alembic/etc. secondary) and a Build vs. Buy vs. Hack decision framework.

**What would change if wrong:** If DCC tools have fundamentally incompatible data models that cannot be abstracted through a common interface (e.g., Blender's modifier stack vs. Houdini's node graph vs. Nuke's compositing tree), the TAL becomes an impedance mismatch layer that either (a) limits functionality to the lowest common denominator, or (b) introduces bugs from lossy format conversions. The Assumptions document (B4) explicitly questions this: "Most tools have limited programmatic control."

**Source:** COS_Architecture_v1.md (§10 — TAL), Assumptions.md (B4 — "A capability orchestration layer above existing tools is feasible"), Capability_Dependency_Map.md (§10 — P04 PipelineTD is a bottleneck with ~47 connections).

**Current confidence:** 35% — this is one of the most technically challenging assumptions. USD is mentioned as the "primary interchange format" but USD adoption is uneven across tools. The Build vs. Buy vs. Hack framework acknowledges the difficulty by including "Hack" as an acceptable temporary solution.

**Research to validate/invalidate:** Prototype a TAL adapter between 3 tools (e.g., Blender → USD → Unreal Engine). Measure: (a) fidelity of round-trip conversions, (b) % of tool-specific features lost in abstraction, (c) time to build vs. maintain adapters.

---

## 2. Potential Breakthroughs — Discoveries That Would Dramatically Simplify or Improve the Architecture

### B1: A Universal Creative Data Model Exists

**What if:** Research reveals that all creative tools share a common underlying data structure — a "creative scene" graph that can represent any creative work (2D, 3D, animation, VFX, audio) through a unified set of primitives (geometry, materials, animation curves, cameras, lights, simulation caches).

**Architectural impact:** The TAL (Layer 6) becomes dramatically simpler — instead of maintaining N adapters for N tools, it maintains one universal data model with import/export filters. The APML (Layer 5) uses the same data model natively, eliminating format translation entirely. Asset management becomes tool-agnostic. The entire 7-layer architecture becomes simpler because Layer 6's complexity drops by an order of magnitude.

**Evidence so far:** USD (Universal Scene Description) from Pixar is a step in this direction (COS_Architecture_v1.md §3.1 — "Pixar pattern: USD as non-destructive data backbone"). Open_Questions.md (Q6) asks directly: "What is the universal data model that all creative tools share?"

**Confidence:** 25% — USD is promising but not universal. Houdini's VEX data model, Nuke's compositing tree, and Unreal's blueprint system all resist USD abstraction.

---

### B2: Many Specialists Can Be Replaced by a Single Foundation Model

**What if:** A single large multimodal model can perform the functions of multiple specialists (e.g., one model that can model, texture, light, and render) — reducing the 23-specialist hierarchy to 3-5 meta-capabilities.

**Architectural impact:** The Specialist Hierarchy collapses. The POL's dependency resolution becomes trivial (fewer nodes, fewer edges). The bottleneck analysis (10 connections for DigitalModeler) becomes irrelevant if one capability replaces DigitalModeler, Rigger, TextureArtist, ShadingTD, and Lookdev. The 7-layer architecture might reduce to 4-5 layers as entire capability domains merge into single model invocations. The TAL might shrink dramatically if the foundation model works internally and only needs to render final output.

**Evidence so far:** Current AI models (image/video generation) can already produce rendered-quality output from text prompts, bypassing the entire 3D pipeline. The Smallest_Viable_COS.md excludes most 3D specialists for the MVP.

**Confidence:** 30% — while single models can produce impressive output, they lack the controllability, consistency, and editability that professional production requires. A model that can do everything may not do anything at professional quality.

---

### B3: Multi-Modal Intent Communication Is More Powerful Than Text

**What if:** Research into creative intent communication reveals that directors communicate most effectively through a combination of sketches, reference images, verbal tone descriptions, and gestural input — and that text-only briefs are the least effective modality.

**Architectural impact:** The DEL (Layer 1) and CIL (Layer 2) would need native support for multi-modal input (sketch overlay, voice tone analysis, gesture recognition, reference image annotation) rather than treating these as optional "modalities" on top of a text-based intent model. The CIL's brief schema (currently text-focused) would need a multi-modal knowledge representation. The DEL interface would shift from "director types instructions" to "director paints, points, speaks, and shows."

**Evidence so far:** Directors & Creative Leadership research (§Layered Communication System) documents that directors use look books, tone packets, storyboards, and verbal direction — not just text. The DEL (§5.2) already lists multiple modalities but the interface contracts still default to text.

**Confidence:** 45% — supported by research but unproven in the COS context. The MVP interface (§7 in Smallest_Viable_COS.md) already shows text-based interaction primarily.

---

### B4: Quality Evaluation Can Be Framed as Comparative, Not Absolute

**What if:** Quality evaluation is more accurate when framed as "which of these two options is better?" rather than "score this option from 0.0-1.0" — the comparative approach used in Braintrust sessions (e.g., "this ending works better than the other one").

**Architectural impact:** The KQL quality evaluation engine (Decision_Architecture.md §5.2) shifts from absolute scoring to pairwise comparison. The "overall score 0.0-1.0" model is replaced with ranking, preference learning, and comparative judgments. The Director's interaction changes from "approve/reject this at score 0.7" to "which of these variations do you prefer?" — which aligns with the exploration mode's generate-evaluate cycle. The quality gate thresholds (0.6, 0.7, 0.8, 0.85) become relative rankings.

**Evidence so far:** The Braintrust pattern (Creative_Roles_as_Functions.md §2) is inherently comparative — it compares the current work against what the film could be. The "I'll Know It When I See It" pattern (Directors research) is inherently comparative — the director needs options to compare.

**Confidence:** 40% — comparative quality evaluation is promising but untested in the COS. The absolute scoring model (§5.5) may still be useful for automated gates.

---

### B5: The Most Critical Bottleneck Is Not DigitalModeler but Intent Translation

**What if:** Research into real production bottlenecks reveals that the most costly failures are not in modeling or lighting but in the translation of creative intent between stages — the "telephone game" degradation of creative vision (Open_Questions.md Q2).

**Architectural impact:** The CIL (Layer 2) becomes the most critical architectural layer, not the POL or TAL. Architecture investment shifts from tool integration (TAL) and workflow orchestration (POL) to intent preservation and translation fidelity (CIL). The "persistent creative intent model" (suggested in Q2) becomes a central architectural component — every layer references the same intent model, and every transformation validates against it. The bottleneck analysis (Capability_Dependency_Map.md §10) would be supplemented with an "intent fidelity analysis" that tracks how much creative intent is lost at each handoff.

**Evidence so far:** Open_Questions.md (Q2 — "How does creative intent survive the pipeline?"), Pixar research (director's vision maintained through 4-year process via Braintrust and reviews), VFX research (VFX supervisor bridges creative-technical gap). The bottleneck analysis currently focuses on data dependencies, not intent fidelity.

**Confidence:** 55% — research suggests intent loss is the real production killer, but the COS architecture currently allocates most complexity to POL and TAL rather than CIL.

---

## 3. Known Unknowns — What We Don't Know That Could Fundamentally Change the Design

### U1: What Is the Actual Cognitive Load of the "Director" Role?

**Context:** The Three_Organizational_Models.md comparison matrix rates Model A (Director + Specialists) at 10/10 cognitive load but Model B (Capability Network) at 2/10. These are estimates, not measurements.

**What we don't know:** Whether users across the expertise spectrum can effectively function as directors. A novice might be overwhelmed by even Model B's 2/10 load. An expert might find Model A's 10/0 liberating. Without user studies, the entire Director-UX model is unvalidated.

**Architectural impact:** If cognitive load is high for all users, the COS must default to high-automation modes (Model B/C) with learning curves for Model A. If cognitive load is manageable, the architecture can support Model A as primary.

---

### U2: How Much Creative Intent Is Lost at Each Layer Boundary?

**Context:** Open_Questions.md (Q2) raises this directly. The COS architecture has 6 layer-to-layer boundaries (DEL→CIL, CIL→POL, POL→TAL, etc.), each with interface contracts designed to preserve information.

**What we don't know:** The actual loss rate per boundary. If each boundary loses 10-15% of creative intent, cumulative loss across 6 boundaries would be 47-62% — rendering the system unusable for faithful creative production.

**Architectural impact:** If intent loss is high, the architecture needs either (a) fewer layer boundaries (collapse layers), (b) a persistent intent model that travels with work items and is checked at each boundary, or (c) bidirectional interfaces where intent can flow back upstream for correction.

---

### U3: Can AI Agents Replicate Specialist Decision-Making Fidelity?

**Context:** Each of the 23 specialists has unique knowledge and decision-making processes documented in Specialist_Capability_Domains.md and the 6 research documents.

**What we don't know:** Whether AI agents can replicate the quality of decisions made by specialist humans. A Rigger (C05) makes thousands of topology and joint placement decisions per character. An Animator (A01) makes tens of thousands of performance decisions per shot. If AI agents operate at 70% fidelity, the output quality degrades multiplicatively across 5+ agent chaining (0.7^5 = 0.17 — 17% of expected quality).

**Architectural impact:** If AI specialist fidelity is low, the architecture needs (a) human-in-the-loop for critical decisions, (b) tighter quality gates with human review at every stage, or (c) shorter dependency chains that minimize agent-to-agent handoffs.

---

### U4: What Is the Actual Dependency Graph for AI Capabilities (vs. Human Capabilities)?

**Context:** The Capability_Dependency_Map.md (§10) identifies C04 DigitalModeler as the #1 bottleneck (10 connections), V04 LayoutArtist as #2 (7 connections), and V05 LightingTD as #3 (7 connections). These rankings are based on human production workflows.

**What we don't know:** Whether AI capabilities have the same dependency topology. An AI that can generate 3D geometry from text (e.g., text-to-3D models) might bypass DigitalModeler entirely. An AI that can simulate lighting from a brief (e.g., neural rendering) might bypass LightingTD.

**Architectural impact:** If AI capabilities have a fundamentally different dependency graph than human capabilities, the bottleneck analysis, specialist hierarchy, and pipeline stage model all need revision. The entire architecture is built on human production patterns — if AI rewrites the dependencies, the architecture must adapt.

---

### U5: How Should the System Handle Multiple Concurrent Work Items?

**Context:** The Three Organizational Models comparison shows Model A "does not scale beyond ~5 concurrent work items." But real productions manage hundreds of shots and assets simultaneously.

**What we don't know:** How the COS should manage parallelism, resource contention, and cross-work-item dependencies. When two work items need the same character asset with different modifications, does the system fork the asset or serialize access? When lighting is blocked for Shot A but Shot B is ready, does the system idle or work ahead?

**Architectural impact:** If concurrent work management requires architectural features not currently specified (e.g., work queues, resource pools, transaction locks on shared assets), the POL must be significantly expanded beyond its current state machine design.

---

### U6: What Is the Right Feedback Cadence for AI Production?

**Context:** Decision_Architecture.md (§3.6) defines the dailies rhythm: daily standup + weekly review in pre-production, daily dailies + weekly milestone in production, alternate-day reviews in post-production. This is based on human studio patterns.

**What we don't know:** Whether AI production needs different feedback cadences. An AI specialist might produce work in seconds that a human takes days to create. Daily reviews might be too infrequent (allowing errors to accumulate) or too frequent (overwhelming the Director with review requests).

**Architectural impact:** If AI feedback cadence is event-driven (review every N iterations) rather than time-driven (review daily), the FIL scheduling model needs fundamental redesign. The "dailies rhythm" metaphor may not apply to AI production.

---

### U7: How Does Non-Destructive Layering Work Across AI Curated Outputs?

**Context:** The APML (Layer 5) is inspired by USD's non-destructive layering model (COS_Architecture_v1.md §9.1). It assumes that contributions from multiple specialists can be composed as layers.

**What we don't know:** Whether AI-generated outputs are compatible with non-destructive layering. Human specialists produce organized, layered work (e.g., separate geometry, texture, and lighting files). AI models often produce monolithic, non-decomposable outputs (e.g., a single image that can't be separated into components). If AI outputs resist decomposition, the APML layering model breaks.

**Architectural impact:** If AI outputs are non-decomposable, the APML must either (a) store entire outputs as atomic units (losing the benefits of non-destructive editing), (b) require AI models to produce layered outputs (constraining model choices), or (c) use a different asset management paradigm entirely.

---

### U8: What Is the Optimal Point of Human Intervention in an AI Pipeline?

**Context:** The Decision Architecture defines five decision authority levels (L1-L5) and maps decisions to autonomy levels (Decision_Architecture.md §2.3). The three organizational models represent different points on the human-automation spectrum.

**What we don't know:** Where human intervention adds the most value. Should the Director review every concept option (high intervention)? Only final output (low intervention)? Only when quality scores are low (conditional intervention)? The optimal point affects every layer's design.

**Architectural impact:** If humans add most value at intent-setting (early) and acceptance (late), the architecture should automate middle stages heavily. If humans add most value at quality evaluation (checkpoints throughout), the architecture needs human-in-the-loop at every stage. The entire DEL-FIL interaction model depends on this unknown.

---

## 4. Highest Architectural Impact Research — Which Document Would Change the Architecture Most If Wrong

### The Capability Dependency Map (Capability_Dependency_Map.md)

**Why it has the highest architectural impact:** This single document determines the structure of the entire system. If its dependency analysis is wrong, everything built on top of it is wrong.

**Specific architecture elements that depend on it:**

| Element | Dependency | What breaks if wrong |
|---------|-----------|---------------------|
| **Specialist Hierarchy** (23 specialists, 4 tiers) | Based on bottleneck ranking and non-redundant analysis (§10) | If C04 DigitalModeler is NOT the #1 bottleneck (10 connections), the entire Tier 1 (Core Specialists) structure changes. If different capabilities are bottlenecks, different specialists become Tier 1. |
| **8 Strategic Mergers** (C06+C07+V08, etc.) | Based on communication frequency, decision coupling, and shared failure domains | If these capabilities do NOT share knowledge bases or tight coupling, the mergers produce functionally impaired specialists. The 30-40% iteration time reduction estimate for Surface & Material Artist would be wrong. |
| **Pipeline Stage Model** (§5a — Primary Production Chain) | Based on the sequential dependency chain S02→S01→V04→A01→V07→V05→P05→D08 | If the actual dependency chain has different orderings or skips stages, the POL state machine and gate definitions are incorrect. The phase model (pre-pro/production/post-pro) is derived from stage dependencies. |
| **Smallest Viable COS** (8 capabilities) | Based on shortest dependency chain analysis (S04→V01→V03→V05→P05) | If the environment chain has hidden dependencies not captured in the map, the MVP is incomplete. If a shorter chain exists through different capabilities, the MVP is oversized. |
| **Storyboard as First Workflow** | Based on the Story chain being the shortest (S02→S01 = 2 capabilities) | If storyboarding has hidden dependencies on character design or layout context, the recommended first workflow is wrong. |
| **Three Organizational Models** | Model A's routing patterns, Model B's graph topology, Model C's department structure | All three models assume the dependency graph as ground truth. If the graph changes, the routing patterns change. Model B's subgraph instantiation (§3.3) is built directly on the dependency topology. |
| **TAL Adapter Priority** | Tool integration priority follows capability bottlenecks | If P04 PipelineTD's 47 connections are not the right metric, the TAL integration roadmap changes. |
| **Failure Isolation Strategy** | Non-redundant capabilities (C04, C05, V04, V05, P05, P04) must have independent failure domains | If other capabilities are also non-redundant, additional Tier 1 specialists are needed. If listed capabilities are actually redundant, they can be merged or risk-adjusted. |

**Impact severity:** If the dependency map is 50% wrong, every downstream document (Specialist Hierarchy, Three Organizational Models, COS Architecture v1, Decision Architecture, Smallest Viable COS) would need significant revision. The Capability Dependency Map is the single most critical document in the entire repository.

**Document location:** `01_Capability_Architecture/Capability_Dependency_Map.md`

---

### Runner-Up: The COS Architecture v1 (COS_Architecture_v1.md)

**Why it has the second-highest impact:** This defines the actual 7-layer architecture, interface contracts, data flow, and architectural principles. If its layer decomposition is wrong, the entire implementation framework needs restructuring.

**What depends on it:** Every other document either extends the architecture (Specialist Hierarchy, Decision Architecture) or builds applications on top (Smallest Viable COS, Three Organizational Models). The interface contracts (§12) define the API between every pair of layers — if these contracts change, every layer implementation changes.

**Document location:** `01_Capability_Architecture/COS_Architecture_v1.md`

---

## 5. Roadmap-Changing Discoveries — What Research So Far Suggests a Different Priority Order

### Finding 1: The Smallest Viable COS and First Workflow Are Mismatched

**What the research queue says:** The MVP should build 8 capabilities for environment creation (S04→V01→V03→V05→P05), but the recommended first workflow is Storyboard Creation (S02→S01).

**Roadmap implication:** These two tracks use different capabilities (environment uses Visual Domain; storyboard uses Story Domain) and different tools (Blender for environment; image generation for storyboard). Building both in parallel would split development focus. The architecture supports either starting point, but the roadmap needs to pick ONE.

**Recommendation:** Follow the Storyboard workflow first (4 capabilities, 1 tool). The environment MVP becomes Phase 2 (after storyboard is validated). This is consistent with:
- Smallest_Viable_COS.md (§Part 2 — Storyboard is "Best choice for first workflow")
- The expansion path diagram (Storyboard → Layout → Environment → Animation/Character → Cinematic Shot)
- The principle that storyboarding is the "keystone workflow" that unlocks all others

**Impact:** The 8-capability MVP estimate is premature. The actual first deliverable is a 4-capability storyboard system. Schedule estimates should be revised downward for first milestone.

---

### Finding 2: The Pipeline Metaphor Is Questioned Before Implementation Begins

**What the research says:** Open_Questions.md (Q1) explicitly questions whether "pipeline" is the right metaphor. Every studio research document emphasizes "loop not line." Game studios use nested macro/micro pipelines, not linear stage progression.

**Roadmap implication:** The POL (Layer 3) is currently designed as a state machine with defined stages (§7.5). If non-linear creation is the norm, building a linear POL first creates technical debt that must be paid during redesign for non-linear workflows.

**Recommendation:** Design the POL as a graph-based state machine (supporting transitions between any two states, not just linear progression) from the start. The implementation can default to linear progression for simplicity while supporting non-linear paths architecturally. This avoids a rewrite between v1.0 and v2.0.

**Source:** Open_Questions.md (Q1), VFX_House_Pipeline.md ("loop not line"), Game_Studio_Pipeline.md (nested micro/macro pipelines).

**Impact:** POL implementation complexity increases by ~30% for the graph-based design, but avoids 100% redesign cost if linear-only implementation needs to be replaced.

---

### Finding 3: The Bottleneck Analysis Suggests Different Tool Integration Priorities

**What the research says:** The Capability_Dependency_Map (§10) shows C04 DigitalModeler (#1 bottleneck, 10 connections) and V04 LayoutArtist (#2 bottleneck, 7 connections) as the most critical capabilities.

**Roadmap implication:** If DigitalModeler is the most connected bottleneck, tool integration priority should be: 3D modeling tools first, followed by layout/previz tools, then lighting tools. But the Smallest Viable COS recommends environment creation (V03 environment artist + V05 lighting) which bypasses DigitalModeler entirely — excluding the #1 bottleneck from the first production workflow.

**Recommendation:** Either (a) accept that the MVP defers the most critical bottleneck (DigitalModeler) to Phase 2, or (b) build a character asset workflow (C01→C04→C05) instead of environment workflow as the MVP, addressing the bottleneck directly. The current recommendation (environment MVP) avoids the bottleneck, which is pragmatic for first delivery but creates risk that DigitalModeler integration is harder than estimated.

**Source:** Capability_Dependency_Map.md (§10 — Bottleneck Analysis), Specialist_Hierarchy.md (§1.1 — DigitalModeler as Central Geometry Gateway).

**Impact:** If tool integration for DigitalModeler is deferred, it must be explicitly scoped as a Phase 2 dependency with dedicated integration time. The roadmap should include a "digital modeling integration spike" in Phase 1 to assess complexity before committing to Phase 2 timelines.

---

### Finding 4: The Braintrust Model May Not Transfer to AI Systems Without Human Expertise

**What the research says:** Creative_Decision_Systems.md (§3.1) documents that the Braintrust's effectiveness depends on experienced peers who "have been through the process." The candor contract works because members have credibility from shared experience.

**Roadmap implication:** The FIL (§11) is designed as an automated Braintrust that evaluates quality and provides feedback. But an AI system lacks the shared creative experience that makes Braintrust feedback credible. The FIL might produce feedback that Directors ignore because it lacks experiential authority.

**Recommendation:** Before building a fully automated FIL, implement a human-in-the-loop Braintrust system where expert curators provide feedback, and the AI FIL learns from those patterns. This is a hybrid approach: human quality evaluation first (Phase 1-2 of implementation phasing), automated FIL later (Phase 4+). The roadmap should prioritize human feedback collection and learning over automated quality evaluation.

**Source:** Creative_Decision_Systems.md (§3.1 — Braintrust composed of peers who have been through the process), Creative_Roles_as_Functions.md (§2.8 — AuthorityLeak and AuthorityDrift failure modes for automated systems).

**Impact:** The FIL implementation is deferred from Phase 1 to Phase 3+ for the automated feedback component. Phase 1 FIL is limited to feedback collection/tracking (non-evaluative infrastructure). The quality heuristics (KQL) are knowledge-base only, not automated evaluation.

---

### Finding 5: Quality Heuristics Need Empirical Validation Before Architecture Commitments

**What the research says:** The Decision_Architecture.md (§5) defines 23 quality signals across creative, technical, and production domains. These are "drawn from creative decision research" and not yet validated. The "80% grounded in reference, 20% original" rule (§5.1.2) is from VFX research but may not apply across all domains.

**Roadmap implication:** The KQL quality evaluation engine is specified in detail, but the heuristics it uses are unvalidated. Building the engine before validating the signals risks building an infrastructure that evaluates the wrong things.

**Recommendation:** Conduct a "quality signal validation sprint" before implementing the KQL evaluation engine. Collect labeled creative work samples (e.g., 100 renders rated by 5 professional artists) and test whether the proposed heuristics correlate with human quality ratings. Only after validation should the KQL engine be built. This sprint should be Phase 1.5 (after MVP storyboard workflow, before full KQL implementation).

**Source:** Decision_Architecture.md (§5 — Quality Evaluation Framework), COS_Architecture_v1.md (§8 — KQL), Assumptions.md (C2 — "Quality signals are learnable").

**Impact:** The KQL implementation shifts from "build engine + heuristics" to "validate heuristics → build engine → train on validated heuristics." This adds 2-4 weeks for a validation sprint but prevents building on unvalidated assumptions.

---

### Finding 6: The Three Organizational Models Should Not Be Built in Parallel

**What the research says:** The hybrid model (§7.2) proposes three modes (Direct, Studio, Pipeline) with a phased approach (v1.0 = Model A, v2.0 = A+Departments, v3.0 = Model C, v4.0 = Model B). The comparison matrix shows Model B at 10/10 implementation difficulty.

**Roadmap implication:** Building Model B (Capability Network) may be infeasible within reasonable project timelines. The graph router, subgraph instantiator, transitive dependency resolver, and feedback loop detector are "extremely difficult" to build.

**Recommendation:** Explicitly call Model B a "stretch goal" for Phase 4+. Do not include it in the committed roadmap. Focus Phase 1-2 on Model A (Direct + Specialists) with Model C's department structure as an organizational overlay (not an architectural change). If Model B proves unnecessary because Model A + C provides sufficient automation, remove it from the roadmap entirely. This is consistent with the phased implementation (§7.3) but adds a decision gate at Phase 3: "Do we need Model B or can we extend Model C?"

**Source:** Three_Organizational_Models.md (§5.1 — Model B has 10/10 Implementation Difficulty, Model A has 2/10), (§7.3 — Model B deferred to v4.0).

**Impact:** The roadmap explicitly de-risks Model B by making it a Phase 4+ stretch goal rather than a committed deliverable. Phase 1-3 resources are focused on delivering working Model A/C functionality.

---

### Summary of Roadmap Changes

| Finding | Original Plan | Recommended Change | Impact |
|---------|--------------|-------------------|--------|
| MVP vs First Workflow mismatch | Build 8-capability environment MVP | Build 4-capability storyboard MVP first; environment MVP becomes Phase 2 | Earlier first deliverable (smaller scope); later full MVP |
| Pipeline metaphor questioned | Build linear POL state machine | Build graph-based POL supporting non-linear transitions | +30% POL complexity; avoids 100% redesign later |
| Bottleneck DigitalModeler excluded from MVP | Environment chain bypasses #1 bottleneck | Add explicit DigitalModeler integration spike in Phase 1 | Assess complexity early; avoid surprise in Phase 2 |
| Braintrust needs human expertise | Build automated FIL in Phase 1 | Defer automated FIL to Phase 3+; build human-in-the-loop feedback first | Slower FIL automation; higher feedback quality |
| Quality heuristics unvalidated | Build KQL evaluation engine directly | Add quality signal validation sprint before KQL engine | +2-4 weeks validation; prevents wrong-signal architecture |
| Model B too complex for committed roadmap | Phased approach with Model B at v4.0 | Model B as stretch goal; decision gate at Phase 3 whether to build | Removes high-risk item from committed scope |

---

*Document prepared by Hermes Agent*
*Based on analysis of all repository documents: COS_Architecture_v1.md, Capability_Dependency_Map.md, Specialist_Capability_Domains.md, Specialist_Hierarchy.md, Three_Organizational_Models.md, Creative_Roles_as_Functions.md, Decision_Architecture.md, Creative_Decision_Systems.md, Smallest_Viable_COS_and_First_Workflow.md, Assumptions.md, Open_Questions.md, Research_Queue.md, and 6 specialist research documents*

*Date: June 14, 2026*
