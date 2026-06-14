# Decision Architecture for the Creative Operating System

**Document ID:** COS-11-DA-001  
**Version:** 1.0  
**Date:** June 14, 2026  
**Status:** Complete  
**Author:** Hermes Agent — Decision Architecture Specialist  
**Scope:** Decision authority model, feedback protocols, approval gates, quality evaluation framework, conflict resolution mechanics  

---

## TABLE OF CONTENTS

1. [Executive Summary](#1-executive-summary)
2. [Who Decides: Decision Authority Model](#2-who-decides-decision-authority-model)
   - 2.1 The Director as Ultimate Authority
   - 2.2 Autonomous vs. Approval-Required: The Authority Matrix
   - 2.3 Decision Authority Levels
   - 2.4 The Autonomy Spectrum
   - 2.5 Decision Mode Protocol
3. [Who Critiques: Feedback & Critique System](#3-who-critiques-feedback--critique-system)
   - 3.1 Feedback Authority Separation (Braintrust Model)
   - 3.2 The COS Feedback Protocol
   - 3.3 Feedback Types and Their Effects
   - 3.4 The Plussing Protocol
   - 3.5 Feedback Sources and Weighting
   - 3.6 Feedback Cadence: The Dailies Rhythm
4. [Who Approves: Approval Gates](#4-who-approves-approval-gates)
   - 4.1 The Approval Architecture
   - 4.2 Gate Authority Matrix
   - 4.3 Auto-Approval Rules
   - 4.4 Escalation Paths
   - 4.5 Override Protocols
5. [How Is Quality Measured: Quality Evaluation Framework](#5-how-is-quality-measured-quality-evaluation-framework)
   - 5.1 Quality Signal Taxonomy
   - 5.2 The COS Quality Evaluation Engine
   - 5.3 Quality Gate Criteria by Stage
   - 5.4 The "Good Enough" Signal
   - 5.5 Score Interpretation and Decision Mapping
6. [How Conflicting Recommendations Are Resolved](#6-how-conflicting-recommendations-are-resolved)
   - 6.1 Conflict Type Taxonomy
   - 6.2 Resolution Mechanisms
   - 6.3 The Escalation Ladder
   - 6.4 Tiebreaker Protocol
   - 6.5 Conflict Recording and Learning
7. [Integration with COS Layers](#7-integration-with-cos-layers)
8. [Open Questions and Future Work](#8-open-questions-and-future-work)

---

## 1. EXECUTIVE SUMMARY

The Creative Operating System (COS) requires a decision architecture that is simultaneously **director-centric** (the user retains ultimate creative authority) and **intelligent** (the system provides meaningful autonomous guidance). This document defines the complete decision architecture across five dimensions:

| Dimension | Core Principle | Source Pattern |
|-----------|---------------|---------------|
| **Who Decides** | The Director has final authority. The system decides autonomously only within defined, reversible boundaries. | Pixar Director model, Film Director's Cut authority |
| **Who Critiques** | Feedback authority is strictly separated from decision authority. Critique is candid, structured, and additive — never a command. | Pixar Braintrust, Plussing technique |
| **Who Approves** | Explicit approval gates at irreversible or high-impact transitions. Auto-approval at routine, low-risk, or reversible transitions. | VFX shot sign-off, Game quality gates, Software release gates |
| **How Quality Is Measured** | Multi-signal evaluation combining automated heuristics (KQL), domain expertise, comparative analysis, and director preference learning. | Braintrust quality judgment, McKee principles, VFX "Would I Watch This?" test |
| **How Conflicts Are Resolved** | Structured escalation ladder with defined tiebreaker rules. Conflicts are data, not failures — they reveal creative tension that drives better results. | Director vs Producer resolution, Technical vs Creative mediation, Showrunner negotiation |

The architecture draws from Pixar's Braintrust (candor without authority), VFX dailies (structured iterative review), game studio playtest loops (data-driven feedback), film director authority models (absolute creative control with structured input), and showrunner tradeoff frameworks (strategic sacrifice).

---

## 2. WHO DECIDES: DECISION AUTHORITY MODEL

### 2.1 The Director as Ultimate Authority

In the COS, the user is the **Director** — the final authority on all creative decisions. This is non-negotiable and architecturally enforced:

| Principle | Implication |
|-----------|-------------|
| **The Director has final say on all creative decisions** | No system recommendation, feedback, or evaluation can override a Director's decision. |
| **The Director can delegate authority** | The Director may designate auto-approval rules for specific domains, thresholds, or contexts. Delegation is always revocable. |
| **The Director can override any gate** | Every gate has an override mechanism that surfaces the override for audit but permits it. |
| **The Director's intent is the North Star** | When the system cannot determine intent with confidence, it asks rather than assumes. |

This mirrors the Pixar model: the Braintrust has **no authority** to mandate changes. The director retains full ownership and can accept, modify, or reject any feedback.

### 2.2 Autonomous vs. Approval-Required: The Authority Matrix

Decisions in the COS are classified along two axes:

**Axis 1: Impact Level** — The consequence of getting it wrong
- **Irreversible** — Cannot be undone without significant cost (e.g., deleting a published asset, changing project scope)
- **High Impact** — Affects downstream work for multiple people/departments (e.g., changing a milestone, altering a style guide)
- **Medium Impact** — Affects a single workstream for a defined period (e.g., choosing a rendering approach for one shot)
- **Low Impact** — Easily reversible, localized effect (e.g., parameter adjustment, alternative texture variation)
- **Negligible** — No meaningful downstream effect (e.g., incremental optimization, file organization)

**Axis 2: Decision Type** — The nature of the decision
- **Creative Direction** — What to make, what it should feel like, what the intent is
- **Execution Approach** — How to achieve the creative goal (tools, techniques, pipeline)
- **Quality Evaluation** — Whether something meets the bar
- **Resource Allocation** — How time, compute, and attention are distributed
- **Scope/Constraint** — What to include, what to cut, what limits apply
- **Tactical Adjustment** — Minor parameter changes within approved direction

#### Decision Authority Matrix

| Decision Domain | Irreversible | High Impact | Medium Impact | Low Impact | Negligible |
|----------------|--------------|-------------|---------------|------------|------------|
| **Creative Direction** | DIRECTOR ONLY | DIRECTOR ONLY | DIRECTOR (system may recommend) | Director Delegated* | Auto-Approval |
| **Execution Approach** | DIRECTOR ONLY | DIRECTOR (system may recommend with rationale) | Delegated (system decides, director notified) | Auto-Approval | Auto-Approval |
| **Quality Evaluation** | DIRECTOR ONLY | DIRECTOR ONLY (with KQL advisory) | Director with KQL recommendation | Delegated (KQL decides, director can override) | Auto-Approval (KQL verdict stands) |
| **Resource Allocation** | DIRECTOR ONLY | DIRECTOR ONLY (with POL cost analysis) | Director Delegated (within budget) | Auto-Approval (within thresholds) | Auto-Approval |
| **Scope/Constraint** | DIRECTOR ONLY | DIRECTOR ONLY | DIRECTOR (with tradeoff analysis) | Director Delegated (within guardrails) | Auto-Approval |
| **Tactical Adjustment** | DIRECTOR ONLY | DIRECTOR (with cost awareness) | Delegated (system decides, director can review) | Auto-Approval | Auto-Approval |

* **Director Delegated** = The Director pre-authorizes the system to decide within defined guardrails. The system acts autonomously but logs the decision for review. The Director can revoke delegation at any time.

### 2.3 Decision Authority Levels

The COS implements five decision authority levels:

| Level | Name | Description | When Used |
|-------|------|-------------|-----------|
| **L5** | Director Must Decide | System cannot proceed without Director input. Decision is paused. | Irreversible decisions, new creative direction, scope changes, final approvals |
| **L4** | Director Must Confirm | System recommends a course of action. Director must explicitly confirm or redirect. | High-impact decisions, first-time decisions in a domain, quality disputes |
| **L3** | Director Delegated | System decides within guardrails set by Director. Director is notified of the decision and can override within a review window. | Routine but meaningful decisions within established patterns |
| **L2** | System Decides, Director Can Review | System acts autonomously. Decision is logged for Director review on the dashboard. Director can undo. | Standard execution decisions, low-impact tactical choices |
| **L1** | System Decides | System acts autonomously. No review needed. | Negligible decisions, routine maintenance, optimization within approved parameters |

### 2.4 The Autonomy Spectrum

The COS learns the Director's preferred autonomy level over time. Initially, the system defaults to L4 (Director Must Confirm) for any decision the Director hasn't previously delegated. As patterns emerge:

- **Pattern learning:** If the Director consistently approves a particular decision type, the COS suggests moving it to L3 or L2.
- **Revocation:** The Director can always escalate a decision back to a higher level.
- **Context sensitivity:** Autonomy levels can vary by phase (more autonomy in production, less in pre-production and finaling).

#### Decision Mode Protocol

When the Director provides creative direction, the system enters one of two modes:

| Mode | Description | Decision Authority | System Behavior |
|------|-------------|-------------------|-----------------|
| **Exploration Mode** | Generating options, finding the design space | L3-L2 (System generates options autonomously within brief constraints) | Produce N variations; present to Director for evaluation; do NOT refine until direction is chosen |
| **Refinement Mode** | Polishing a chosen direction toward quality targets | L4-L3 (System recommends refinements, Director confirms or adjusts) | Iterate on selected direction; surface tradeoffs; escalate if structural changes needed |

The mode switch from Exploration to Refinement requires **Director approval**. The mode switch from Refinement back to Exploration (triggered by structural feedback) requires **Director awareness** at minimum, and Director approval if cost of change is above threshold.

---

## 3. WHO CRITIQUES: FEEDBACK & CRITIQUE SYSTEM

### 3.1 Feedback Authority Separation (Braintrust Model)

The COS implements the Pixar Braintrust principle as a hard architectural boundary:

> **The feedback layer evaluates and recommends. It does NOT decide.**

This separation is enforced at the data flow level:

```
Feedback Sources (FIL + KQL)
         │
         │  Structured feedback, quality scores, recommendations
         ▼
    Director (Layer 1 - DEL)
         │
         │  Approval or rejection decision
         ▼
    Pipeline (Layer 3 - POL) -- executes the decision
```

**The critical rule:** Feedback flows UP to the Director. Decisions flow DOWN from the Director. The feedback layer never sends commands directly to the pipeline layer — only recommendations that the Director has approved (or that fall within delegated authority).

### 3.2 The COS Feedback Protocol

The feedback protocol defines how the COS delivers critique without overruling the user.

#### Rule 1: Problems, Not Solutions

The COS identifies what isn't working. It does not prescribe how to fix it — that is the Director's role.

- **Good feedback:** "The character's silhouette doesn't clearly communicate menace. The curved form reads as gentle rather than threatening."
- **Bad feedback (overreaching):** "Change the character's shoulders to be more angular, reshape the jaw, and add spikes to the back."

The exception: When the Director explicitly asks for solution suggestions, the COS may provide them — but framed as options, not mandates.

#### Rule 2: Specific, Not Vague

Vague feedback is worse than no feedback. Every critique must be traceable to a specific entity, attribute, or criterion.

- **Good:** "In shot A37, the lighting on the protagonist's face doesn't match the emotional beat. The scene calls for suspicion, but the fill light is too warm, creating an atmosphere of comfort."
- **Bad:** "Something about shot A37 feels off."

#### Rule 3: Audience-Focused, Not Personal

Feedback is framed around the audience's experience, not the creator's choices.

- **Good:** "The audience may feel confused here because the rule system for this world hasn't been established before this moment."
- **Bad:** "You didn't set up the rules correctly."

#### Rule 4: Celebrate the Ambition First

Before identifying problems, the COS acknowledges what works and the ambition of the creative goal.

- **Good:** "This is a bold narrative choice — the nonlinear timeline is ambitious. However, the current structure may cause audience confusion because the temporal cues aren't clear enough."
- **Bad:** "This is confusing."

#### Rule 5: Leave the Solution to the Director

After identifying problems, the COS stops. The Director determines how to address them. This preserves creative ownership and produces better results because the Director knows the full creative context.

### 3.3 Feedback Types and Their Effects

| Feedback Type | Definition | Effect on COS | Cost Multiplier |
|--------------|------------|--------------|-----------------|
| **Structural** | The problem requires returning to exploration mode — the current approach cannot be refined to meet the goal | Triggers mode switch from Refinement to Exploration. L2 (CIL) generates new interpretations. | 3-5x if late-stage |
| **Surface** | The problem can be addressed within the current refinement pass | Stays in Refinement mode. L2 (CIL) adjusts parameters within current direction. | 1x (stage-appropriate) |
| **Intent Clarification** | The creative direction itself is unclear or inconsistent | Returns to Director for intent refinement. L2 (CIL) cannot proceed without clearer direction. | Variable |
| **Approval** | The work meets quality criteria and can advance | Triggers state transition in L3 (POL). Entity moves to next stage. | N/A |
| **Rejection** | The work does not meet quality criteria and cannot advance | Returns entity to in_progress. L2 (CIL) issues revision brief. | Full cost of revision |
| **Conditional Approval** | Work can advance provided specific conditions are met | Entity advances with open action items. Conditions tracked by L5 (APML). | Partial cost (conditions only) |
| **Comparative** | Feedback based on comparison to reference or alternative | Influences L2 (CIL) interpretation weighting. Does not trigger mode change alone. | Low |

### 3.4 The Plussing Protocol

Inspired by Walt Disney's plussing technique, the COS follows this structured approach to every critique:

1. **Start with what works.** "The composition here is strong — the rule of thirds draws the eye naturally to the focal point."
2. **State the problem.** "However, the color temperature shifts abruptly between frames 24 and 36, breaking the visual continuity."
3. **Explain why it matters.** "This will feel jarring to the audience. They'll register the discontinuity even if they don't consciously identify it."
4. **Suggest a direction (not a solution).** "What if we tried a gradual temperature transition across the full sequence instead of a hard cut?"
5. **End on encouragement.** "The intent is clear and strong — the execution just needs smoothing."

The COS NEVER:
- Says "this is bad" without constructive framing
- Attacks the Director's judgment
- Offers a single mandated solution
- Frames feedback as final verdict

### 3.5 Feedback Sources and Weighting

The COS aggregates feedback from multiple sources, each with different authority weights:

| Source | Weight | Description | When Dominant |
|--------|--------|-------------|--------------|
| **Director (DEL)** | **VETO / FINAL** | Human Director's feedback is authoritative. Overrides all other sources. | Always |
| **Quality Heuristics (KQL)** | High (0.7-0.9) | Automated evaluations against learned quality criteria | Early stages, technical domains, established patterns |
| **Domain Knowledge (KQL)** | Medium (0.5-0.7) | Best-practice guidance from encoded expertise | General guidance, industry standards |
| **Comparative Analysis (FIL)** | Medium (0.4-0.6) | Comparison against reference materials or alternatives | When strong references exist |
| **Preference Learning (FIL/KQL)** | Low-Medium (0.3-0.5) | Historical patterns from Director's past decisions | Increasing weight as confidence grows |
| **Self-Evaluation (FIL)** | Low (0.2-0.4) | System's own confidence assessment of output quality | Default when no other signal available |

**Weight integration:** When feedback sources agree, the system combines weights for a confident recommendation. When they disagree, the system presents the disagreement to the Director as a structured tradeoff (see Section 6).

### 3.6 Feedback Cadence: The Dailies Rhythm

The COS follows a regular review cadence rather than only event-driven review:

| Phase | Cadence | Duration | Focus |
|-------|---------|----------|-------|
| **Pre-Production** | Daily standup + weekly structured review | Standup: 10 min. Review: 45 min | Concept alignment, exploration direction |
| **Production** | Daily dailies + weekly milestone review | Dailies: 20 min. Milestone: 60 min | Execution quality, iteration progress |
| **Post-Production** | Alternate-day reviews + milestone signoffs | Review: 30 min. Signoff: 15 min | Surface refinement, completion verification |

Each review session produces:
1. A structured feedback log with categorized items
2. Action items with assigned responsibility and deadlines
3. Updated quality scores for reviewed entities
4. Recommendations for advancement, revision, or escalation

---

## 4. WHO APPROVES: APPROVAL GATES

### 4.1 The Approval Architecture

Approval gates are structured checkpoints that control state transitions in the Pipeline Orchestration Layer (Layer 3). Each gate has:

- **A trigger condition** — What event initiates the gate
- **A gatekeeper** — Who or what has authority to pass the gate
- **Evaluation criteria** — What must be true for the gate to pass
- **Outcome options** — Possible results of the gate evaluation
- **Override protocol** — How the Director can bypass the gate

### 4.2 Gate Authority Matrix

| Gate | Trigger | Default Gatekeeper | Criteria | Auto-Approval Rule | Outcome |
|------|---------|-------------------|----------|-------------------|---------|
| **Concept Approval** | Director submits creative brief | **Director** (L5) | Brief contains evaluable quality criteria, hard constraints, and reference materials | Never auto-approved | Pass / Revise |
| **Exploration Complete** | N variations generated per brief | **Director** (L4) | Design space sufficiently explored; at least one viable direction identified | If N>=5 and KQL confidence >= 0.8, auto-approve with Director notification | Pass / Explore More / Change Direction |
| **Refinement Complete** | Entity meets quality criteria | **Director** (L3/L4) | All required criteria pass; no structural issues; cost of further refinement exceeds benefit | If KQL "good_enough" signal AND diminishing returns detected, auto-approve to next stage | Approve / Revise / Return to Exploration |
| **Vertical Slice Gate** | First complete end-to-end example | **Director** (L5) | End-to-end pipeline validated; quality bar met for at least one complete unit | Never auto-approved | Pass / Fail (with revision brief) |
| **Production Readiness** | Pipeline validated, resources allocated | **Director** (L4) | Vertical slice approved; pipeline stable; resource plan confirmed | Never auto-approved | Ready / Not Ready |
| **Stage Transition** | Work submitted from one stage to next | **Director Delegated** (L3) | All outputs from current stage meet exit criteria; downstream stage ready to receive | If exit criteria met AND dependencies resolved, auto-approve with notification | Pass / Hold / Return |
| **Intermediate Review** | Work at pre-defined checkpoints | **Director Delegated** (L3) | Work meets stage-appropriate quality bar | Auto-approve with Director review window (24h) | Approve / Needs Work |
| **Alpha Gate** | All features implemented | **Director** (L5) | Feature-complete; no new features being added; all core systems functional | Never auto-approved | Pass / Conditional Pass / Fail |
| **Beta Gate** | All content complete | **Director** (L4) | Content-complete; polish and bug-fixing only; performance targets within range | Auto-approve with Director sign-off if performance targets met | Pass / Conditional / Fail |
| **Final Approval Gate** | Ship-ready candidate | **Director** (L5) | All criteria met; no critical issues; Director confirms creative intent satisfied | Never auto-approved | Approved / Conditional / Rejected |
| **Retake Decision** | Structural feedback requires major rework | **Director** (L4) | Cost-benefit analysis; alternative approaches proposed | Never auto-approved | Proceed with Retake / Accept Current / Change Approach |

### 4.3 Auto-Approval Rules

Auto-approval is a delegation of authority from the Director to the system. It is always:

- **Bound by guardrails** — Auto-approval only applies within defined thresholds
- **Logged and auditable** — Every auto-approval is recorded for review
- **Revocable** — The Director can cancel any auto-approval and revert the decision
- **Phase-dependent** — Auto-approval is more restricted in early and late phases

#### Auto-Approval Thresholds

| Domain | Auto-Approval Allowed When | Guardrails |
|--------|---------------------------|------------|
| **Tactical execution adjustments** | Parameter changes within ±20% of approved values | Must not alter creative intent |
| **Intermediate stage transitions** | All exit criteria met AND no structural issues | Director notified within 24h review window |
| **Routine publishing** | Standard asset versioning with no dependency conflicts | Version history preserved for rollback |
| **Low-impact quality passes** | KQL confidence >= 0.85 AND no Director-declared preferences violated | Director can retroactively revert |
| **Exploration generation** | Within brief constraints AND under cost threshold | Must present options, not commit to one |

#### Never Auto-Approved (Always Requires Director)

- Changes to creative direction or intent
- Scope changes (adding or removing features)
- Schedule changes affecting external commitments
- Final approval of any entity
- Structural revisions in post-production
- Resource allocation above budgeted thresholds
- Overriding a quality gate that the system has flagged as failed
- Any decision flagged as "irreversible" in the authority matrix

### 4.4 Escalation Paths

When a decision cannot be made at its current authority level (due to conflict, uncertainty, or threshold violations):

| Escalation Trigger | From | To | Protocol |
|-------------------|------|----|----------|
| **Auto-approval guardrail exceeded** | L1/L2 | L3+ | System presents the limit violation and awaits Director delegation extension or decision |
| **Quality dispute** | L3/KQL | L4/L5 | System presents both quality evaluation and counter-evidence; Director makes final call |
| **Resource conflict** | L3/POL | L4/L5 | System presents competing demands with cost-benefit analysis; Director prioritizes |
| **Creative uncertainty** | L2/CIL | L5 | System asks clarifying questions; Director provides refined intent |
| **Iteration limit reached** | L3/POL | L5 | System presents iteration history and diminishing returns analysis; Director decides to continue, accept, or change approach |
| **Cross-layer conflict** | Any | L5 | System presents the conflicting recommendations with rationale; Director breaks the tie |

### 4.5 Override Protocols

The Director can override any gate. Overrides are tracked and documented:

```
Override Record:
  - Gate: [gate name]
  - Decision Overridden: [original gate outcome]
  - Director's Decision: [what the Director decided instead]
  - Rationale: [Director's stated reason, if provided]
  - Risk Assessment: [system's assessment of override consequences]
  - Conditions: [any conditions attached to the override]
  - Timestamp: [ISO 8601]
  - Review Date: [if conditional, when the override will be reviewed]
```

**Override types:**

| Type | Description | Audit Level |
|------|-------------|-------------|
| **Approval Override** | Director approves work that the system flagged as not ready | Full record + notification to future stages |
| **Rejection Override** | Director rejects work that the system flagged as ready | Full record + feedback that triggered rejection |
| **Gate Bypass** | Director skips a gate entirely | Full record + risk assessment |
| **Delegation Revocation** | Director rescinds auto-approval for a domain | Record + confirmation of revocation |

---

## 5. HOW IS QUALITY MEASURED: QUALITY EVALUATION FRAMEWORK

### 5.1 Quality Signal Taxonomy

The COS evaluates quality using multiple signal types, drawn from creative decision research across animation, film, VFX, games, and narrative design:

#### 5.1.1 Creative Quality Signals

| Signal | Definition | Domain | Evaluation Method |
|--------|-----------|--------|-------------------|
| **Silhouette Readability** | Design is recognizable in silhouette alone | Character Design | KQL heuristic: contrast analysis, edge distinctness |
| **Emotional Beat Clarity** | Sequence communicates intended emotional arc without dialogue | Narrative | KQL heuristic: emotional arc tracing, pacing analysis |
| **Internal Consistency** | Elements are coherent with the established world rules | All Domains | KQL heuristic: constraint violation detection |
| **Narrative Coherence** | Story events follow a logical, emotionally satisfying structure | Narrative | KQL heuristic: cause-effect chain analysis, McKee principles |
| **Subtext Presence** | Scene operates on multiple levels — explicit and implicit meaning | Narrative, Performance | KQL heuristic: dialogue/textual subtext analysis |
| **Inciting Incident Clarity** | The event that disrupts balance is clear and meaningful | Narrative | KQL heuristic: McKee inciting incident criteria |
| **Stakes Communication** | Audience understands what the character stands to gain or lose | Narrative | KQL heuristic: stakes articulation analysis |
| **Pacing/Rhythm** | Tension and release are appropriately balanced | All Domains | KQL heuristic: temporal flow analysis |
| **Tonal Consistency** | Emotional register is coherent within and across scenes | All Domains | KQL heuristic: emotional signal continuity |
| **Form Follows Function** | Design choices serve creative purpose, not decoration | Design | KQL heuristic: intent-to-execution mapping |

#### 5.1.2 Technical Quality Signals

| Signal | Definition | Domain | Evaluation Method |
|--------|-----------|--------|-------------------|
| **Constraint Satisfaction** | All hard constraints met; acceptable % soft constraints met | All Domains | Automated verification (L6/TAL) |
| **Reference Grounding** | Output is 80% grounded in reference, 20% original spin | All Domains | KQL heuristic: reference similarity scoring |
| **Performance Targets** | Resource usage within acceptable range (render time, memory, frame rate) | Technical | Automated measurement (L6/TAL) |
| **Pipeline Compatibility** | Asset works correctly at all downstream stages | Technical | Integration testing (L3/POL) |
| **Version Discipline** | Correct versions are used; no conflicting dependencies | Production | Automated verification (L5/APML) |
| **Integrity Standards** | No degenerate geometry, valid normals, complete metadata | Technical | Validation gates (L5/APML) |

#### 5.1.3 Production Quality Signals

| Signal | Definition | Domain | Evaluation Method |
|--------|-----------|--------|-------------------|
| **Cost of Change Priority** | Changes at current stage are appropriately costed | Production | KQL heuristic: stage-aware cost multiplier (3-5x late stage) |
| **Diminishing Returns** | Further refinement adds <5% improvement | All Domains | KQL heuristic: improvement curve analysis |
| **Schedule Adherence** | Work is on track relative to plan | Production | POL milestone tracking |
| **Iteration Efficiency** | Each iteration produces meaningful improvement | All Domains | KQL heuristic: iteration quality trend analysis |
| **Resource Utilization** | Compute and attention resources are well-allocated | Production | POL resource tracking |

### 5.2 The COS Quality Evaluation Engine

Quality evaluation flows through this process:

```
1. Work is submitted for review (via L5/APML)
         │
2. L4/KQL evaluates against quality criteria:
   ├── Automated heuristics (silhouette, consistency, constraints, etc.)
   ├── Reference comparison (similarity to approved references)
   ├── Domain expertise check (best practices, common patterns)
   └── Historical pattern check (past Director preferences)
         │
3. L7/FIL aggregates evaluations into structured feedback:
   ├── Score per criterion (0.0 - 1.0)
   ├── Confidence per criterion
   ├── Overall quality score
   └── "Good Enough" assessment
         │
4. Results presented to Director (L1/DEL):
   ├── Dashboard with scores and visual annotations
   ├── Structured feedback items
   └── Clear recommendation: Approve / Revise / Return to Exploration / Escalate
         │
5. Director decides (L5 final authority):
   ├── Approve (work advances)
   ├── Reject with feedback (work returns for revision)
   └── Override (accept work despite evaluation)
```

### 5.3 Quality Gate Criteria by Stage

| Stage | Required Quality Signals | Threshold | Evaluation Source |
|-------|-------------------------|-----------|-------------------|
| **Story & Concept** | Emotional beat clarity, narrative coherence, inciting incident clarity, tonal consistency | Overall >= 0.6 | KQL + Director review |
| **Design & Visual Dev** | Silhouette readability, form follows function, constraint satisfaction, reference grounding | Overall >= 0.7 | KQL + Director review |
| **Modeling** | Constraint satisfaction, integrity standards, pipeline compatibility | All hard constraints met | Automated + KQL |
| **Layout & Blocking** | Pacing/rhythm, emotional beat clarity, tonal consistency, form follows function | Overall >= 0.65 | KQL + Director review |
| **Animation** | Emotional beat clarity, subtext presence, stakes communication, tonal consistency, performance targets | Overall >= 0.75 | KQL + Director review |
| **FX & Simulation** | Constraint satisfaction, reference grounding, performance targets, pipeline compatibility | All hard constraints met + overall >= 0.75 | Automated + KQL + Director spot-check |
| **Lighting & Rendering** | Tonal consistency, emotional beat clarity, reference grounding, performance targets, constraint satisfaction | Overall >= 0.8 | KQL + Director review |
| **Compositing & Final** | All creative signals, pipeline compatibility, integrity standards, version discipline | Overall >= 0.85 | KQL + Director final approval |

### 5.4 The "Good Enough" Signal

The system must know when to stop. The "good enough" signal is generated when:

1. **All required quality criteria pass** — No criterion is below its minimum threshold
2. **Diminishing returns detected** — The last N iterations produced <5% improvement per iteration
3. **Aspirational criteria plateau** — Further work on aspirational criteria is unlikely to meaningfully improve the overall product
4. **Cost-benefit analysis favors stopping** — The cost of another iteration exceeds the expected creative value

The "good enough" signal is a **recommendation only**. The Director can:
- Accept it (work moves forward)
- Reject it (request further refinement despite diminishing returns)
- Accept with conditions (approve provided specific improvements are tracked)

### 5.5 Score Interpretation and Decision Mapping

| Overall Score | Interpretation | Default Recommendation | Director Action |
|---------------|---------------|----------------------|-----------------|
| 0.0 - 0.3 | Does not meet minimum bar | Reject — return for fundamental revision | Accept rejection or override with conditions |
| 0.3 - 0.5 | Below threshold — needs significant work | Revise — structural issues likely | Provide structural feedback or accept with conditions |
| 0.5 - 0.7 | Approaching threshold — needs refinement | Revise — surface issues likely | Provide surface feedback or conditional approve |
| 0.7 - 0.85 | Meets threshold — solid work | Approve with notes | Approve or provide final tweaks |
| 0.85 - 0.95 | Exceeds threshold — strong work | Approve | Approve |
| 0.95 - 1.0 | Exceptional — exceeds all criteria | Approve with commendation | Approve; system records as quality benchmark |

---

## 6. HOW CONFLICTING RECOMMENDATIONS ARE RESOLVED

### 6.1 Conflict Type Taxonomy

The COS identifies four categories of conflict:

| Conflict Type | Description | Example | Default Resolution |
|---------------|-------------|---------|-------------------|
| **System vs. Director** | COS recommends approach A; Director wants approach B | System recommends photorealistic rendering; Director prefers stylized | Director always wins. System documents the conflict and adapts its model. |
| **Specialist vs. Specialist** | Two capability domains disagree on approach | Creative Intent says "explore more options"; Pipeline says "schedule requires moving forward" | Director decides. System presents tradeoff data. |
| **Quality vs. Schedule** | Quality evaluation says "not ready"; Schedule says "must ship" | KQL gives 0.6 quality score; Milestone requires completion | Director decides. System presents cost of delay vs. cost of shipping below quality bar. |
| **Creative vs. Technical** | Creative desire conflicts with technical feasibility | Director wants 8K textures; Render budget allows only 4K | Director decides with full cost awareness. Technical presents alternatives. |

### 6.2 Resolution Mechanisms

#### Mechanism 1: Structured Tradeoff Presentation

When conflicts arise, the COS presents a structured tradeoff card:

```
TRADEOFF CARD
─────────────
Conflict: [Type] — [Brief description]

Option A (Recommended by [Source]):
  Description: ...
  Estimated Cost: [Time/Resources]
  Quality Impact: [Score delta]
  Risk Level: [Low/Medium/High]
  Rationale: ...

Option B (Preferred by [Source]):
  Description: ...
  Estimated Cost: [Time/Resources]
  Quality Impact: [Score delta]
  Risk Level: [Low/Medium/High]
  Rationale: ...

Option C (Compromise):
  Description: ...
  Estimated Cost: [Time/Resources]
  Quality Impact: [Score delta]
  Risk Level: [Low/Medium/High]
  Rationale: ...

Director Decision: [ ] Option A  [ ] Option B  [ ] Option C  [ ] Custom
```

#### Mechanism 2: The "Three Cuts" Strategy (from Showrunner Framework)

When negotiating between system recommendations and Director preferences:

1. **Director's Cut** — The Director's pure, uncompromised vision (anchor position)
2. **System's Recommended Cut** — The COS's optimal recommendation with rationale
3. **Compromise Cut** — A middle ground proposed by the system

The system presents all three cuts with estimated costs, quality scores, and risks. The Director selects or modifies.

#### Mechanism 3: Cost-Benefit Escalation

When a conflict cannot be resolved at the working level:

1. **Each side documents its position** with evidence and rationale
2. **The system presents both positions** to the Director with neutral framing
3. **The Director decides** — no appeals, no second chances without new information
4. **The decision is recorded** with rationale for future reference

#### Mechanism 4: The "Note Behind the Note" Protocol

When the Director gives feedback that appears to conflict with their stated intent, the system investigates:

1. **Identify the underlying concern** — "When you say 'make it more polished,' are you concerned about audience perception, character consistency, or something else?"
2. **Probe without challenging** — "I want to make sure I understand the root concern. Is the issue technical quality, or is the creative direction not quite where you want it?"
3. **Reframe the feedback** — "So the real goal is X. Let me suggest approaches that address X directly."

This mirrors the showrunner's "note behind the note" strategy — understanding the fear or concern behind the surface feedback.

#### Mechanism 5: Comparative A/B Testing

When the system and Director disagree on an approach, the system can generate both versions for direct comparison:

1. Generate Option A (system-recommended)
2. Generate Option B (Director-preferred or alternative)
3. Generate Option C (compromise/hybrid)
4. Present side-by-side with quality scores and tradeoffs
5. Director selects

### 6.3 The Escalation Ladder

Conflicts that cannot be resolved at the working level escalate through these steps:

| Step | Level | Who Resolves | Method | Time Limit |
|------|-------|-------------|--------|------------|
| **1** | Working Level | L2 (CIL) + L3 (POL) | Automated tradeoff presentation | Immediate |
| **2** | Domain Lead | L4 (KQL) domain expert | Contextual analysis + recommendation | 1 hour |
| **3** | System-Level | L7 (FIL) | Aggregated recommendation with confidence | 2 hours |
| **4** | Director | L1 (DEL) | Director reviews structured tradeoff | Director's schedule |
| **5** | Director + System | L1 + L7 | If still unresolved, system asks clarifying questions | Per Director |
| **6** | Director Final | L1 | No further escalation possible | Final |

### 6.4 Tiebreaker Protocol

When two specialist capabilities disagree and the Director is not available:

| Condition | Tiebreaker Rule | Rationale |
|-----------|----------------|-----------|
| **Creative vs. Technical** | Default to the more conservative path | Safer to preserve creative intent for Director review than to commit to a risky technical approach |
| **Quality vs. Schedule** | Default to quality if schedule impact is <20%; default to schedule if >20% | Small delays are worth protecting quality; large delays may kill the project |
| **Exploration vs. Refinement** | Default to exploration if confidence in current direction <0.7 | Better to explore more than to polish the wrong direction |
| **Two equal specialists disagree** | Default to the recommendation with higher confidence score | Trust the more certain assessment |
| **Equal confidence, equal impact** | Default to the recommendation that preserves more future options | Reversible over irreversible |
| **Action vs. Delay** | Default to action unless the cost of wrong action is catastrophic | Indecision is more expensive than a wrong decision (Five-Minute Rule) |

**Important:** Tiebreaker decisions are always temporary. They are logged and presented to the Director for confirmation at the next review.

### 6.5 Conflict Recording and Learning

Every conflict and its resolution is recorded for learning:

```
Conflict Record:
  - ID: [unique identifier]
  - Date: [timestamp]
  - Type: [System-vs-Director / Specialist-vs-Specialist / Quality-vs-Schedule / Creative-vs-Technical]
  - Domain: [narrative, visual, technical, production]
  - Participants: [sources of conflicting recommendations]
  - Option A: [description, source, cost, quality impact]
  - Option B: [description, source, cost, quality impact]
  - Option C: [description, source, cost, quality impact] (if applicable)
  - Resolution: [which option chosen]
  - Decided By: [Director / Tiebreaker Rule / Escalation]
  - Rationale: [Director's stated reason, if provided]
  - Outcome: [Did the decision produce good results? Tracked post-resolution]
  - Learned Preference: [Update to Director preference model]
```

This creates a **conflict knowledge base** that:
- Informs future similar conflicts with precedent
- Refines the Director's preference model
- Identifies recurring tension points for architectural improvement
- Provides post-mortem data for process improvement

---

## 7. INTEGRATION WITH COS LAYERS

The Decision Architecture is not a standalone layer — it is a cross-cutting concern embedded in every layer:

| Layer | Decision Architecture Role |
|-------|---------------------------|
| **L1: Director Experience (DEL)** | Decision user interface — communicates authority options, presents tradeoffs, collects approvals, surfaces conflicts |
| **L2: Creative Intent (CIL)** | Decision mode management — exploration vs. refinement, constraint extraction, intent clarification triggers |
| **L3: Pipeline Orchestration (POL)** | Gate enforcement — state transitions controlled by authority levels, auto-approval rules, escalation triggers |
| **L4: Knowledge & Quality (KQL)** | Quality signal evaluation — heuristic application, score computation, "good enough" detection |
| **L5: Asset & Production Management (APML)** | Decision recording — override audit trail, conflict records, approval history, versioned decision data |
| **L6: Tool Abstraction (TAL)** | Decision execution — translates approved decisions into tool-specific actions |
| **L7: Feedback & Iteration (FIL)** | Feedback separation — evaluation and recommendation without authority, Braintrust protocol, dailies cadence |

---

## 8. OPEN QUESTIONS AND FUTURE WORK

1. **How does the system build Director-specific preference models over time?** The preference learning signal starts with low weight and grows with confidence — but the bootstrapping problem (cold start) needs a concrete protocol.

2. **What is the appropriate confidence threshold for auto-approval?** The document proposes domain-specific thresholds, but these need empirical validation in real usage.

3. **How does the system handle multiple Directors or collaborative decision-making?** The current architecture assumes a single Director. Multi-user scenarios (co-directors, showrunner + department heads, client + studio) require an extension of the authority model.

4. **Should the Braintrust model extend to synthetic peer review?** The COS could simulate multiple critic perspectives (e.g., "story expert," "technical expert," "audience surrogate") — but this risks creating a false consensus that the Director should see through.

5. **How are quality criteria maintained and updated?** Quality criteria in KQL need a lifecycle — addition, deprecation, weight adjustment — based on production outcomes and Director feedback.

6. **What happens when the Director is unavailable for an extended period?** The system needs a "Director proxy" protocol with defined limits and escalation paths.

7. **How does the system handle the "I'll Know It When I See It" problem systematically?** The exploration mode addresses this partially, but a structured protocol for convergent search without a defined target is needed.

---

*End of Document — Decision Architecture for the Creative Operating System*
