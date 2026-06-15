# COS Implementation Specifications — Workflows, State Machines & Execution Flows

**Date:** June 15, 2026
**Author:** Chioma (Systems Architect)
**Reference:** [Decision_Architecture.md](../11_Decisions/Decision_Architecture.md), [COS_Architecture_v4_Creativity_First.md](../01_Capability_Architecture/COS_Architecture_v4_Creativity_First.md)

---

## 1. Master State Machine

### 1.1 States

```
stateDiagram-v2
    [*] --> INTAKE: User submits brief
    
    INTAKE --> FRAMING: Raw input received
    FRAMING --> FRAMING: Clarifying questions (loop)
    FRAMING --> EXPLORATION: Intent Token complete
  
    EXPLORATION --> SELECTION: Options generated (5 per beat)
    SELECTION --> EXPLORATION: "Show me more options"
    SELECTION --> REALIZATION: Direction selected
  
    REALIZATION --> EVALUATION: Panels generated
    EVALUATION --> REALIZATION: "Revise based on feedback"
    EVALUATION --> EXPLORATION: "Change direction entirely"
    EVALUATION --> APPROVED: Quality bar met OR director approves
  
    APPROVED --> EXPORT: Assembly
    EXPORT --> [*]
```

### 1.2 Transition Rules

| From | To | Trigger | Condition | Gatekeeper |
|------|----|---------|-----------|------------|
| INTAKE | FRAMING | User submits script/brief | Non-empty input | System (auto) |
| FRAMING | FRAMING | Intent confidence < 0.7 | Gaps identified | Frame Agent |
| FRAMING | EXPLORATION | Intent confidence >= 0.7 | All required fields populated | Frame Agent |
| EXPLORATION | SELECTION | N options generated per beat | N >= count requested | Explore Agent |
| SELECTION | EXPLORATION | User: "Show me more" | Explicit user request | Director (L5) |
| SELECTION | REALIZATION | User selects an option | Selection recorded | Director (L4) |
| REALIZATION | EVALUATION | Panels generated | Non-empty output | Realize Agent |
| EVALUATION | REALIZATION | Overall score < 0.6 AND Director chooses to revise | No structural issues | Director (L4) |
| EVALUATION | EXPLORATION | Structural feedback | Current approach cannot be refined | Director (L5) |
| EVALUATION | APPROVED | Score >= 0.7 OR Director overrides | Quality bar met | Director (L5) |
| APPROVED | EXPORT | All beats in approved state | All beats completed | System (auto) |

**Reference:** [Decision_Architecture.md](../11_Decisions/Decision_Architecture.md) §2 — Decision Authority Model, L4 = Director Must Confirm, L5 = Director Must Decide

---

## 2. Storyboard Workflow (Detailed)

### 2.1 Workflow Overview

```
Workflow: Storyboard Creation  
Domain: Storyboard  
Agents: Frame → Explore → Select → Realize → Evaluate (loop)  
Output: JSON sequence + panel images  
Max iterations: 3 per beat (then Director must decide to approve, change approach, or expand iteration limit)  
```

### 2.2 Step-by-Step Execution Flow

**Step 1: Intake**
- User submits: script text or verbal pitch + direction (tone, style, emotional beats)
- Orchestrator creates: project directory, initial Intent Token
- Output: `intent_token.json` with intent.script populated, state.stage = "intake"

**Step 2: Framing**
- Frame Agent invoked with raw input
- Agent parses script into story beats (5-15 per sequence)
- Identifies gaps: missing mood? unclear style? vague constraints?
- If confidence < 0.7, generates clarifying questions for user
- Produces: complete Intent Token with storyboard.beats array
- State transition: intake → framing → exploration

**Step 3: Exploration (per beat, sequential)**
- For each beat, Explore Agent generates 5 panel options
- Each option includes: description, camera note, composition type, emotional target
- MVP: text-based descriptions, not images
- Output: options stored in work item, presented to user after all beats explored
- State per beat: pending → exploring → evaluated

**Step 4: Selection**
- All beat options presented to user simultaneously
- User selects one option per beat
- User may request "more options" for specific beats (returns to Exploration for that beat)
- User provides optional feedback ("Make beat 3 more dramatic")
- Selected option recorded in Intent Token
- User feedback appended to Intent Token iterations array

**Step 5: Realization**
- For each beat, Realize Agent generates panel image(s) based on selected option
- Uses image generation API (e.g., Stable Diffusion, DALL-E, Midjourney)
- Prompt constructed from: beat description + camera note + mood + style
- Self-evaluation: does the generated panel match the description?
- If self-evaluation score < 0.5, re-generate with adjusted parameters
- Output: panel images saved to `artifacts/beats/{beat_id}/realize/`

**Step 6: Evaluation**
- Evaluate Agent scores each panel against all 5 quality criteria
- Scores: silhouette_readability, emotional_beat_clarity, narrative_coherence, pacing_rhythm, tonal_consistency
- Produces structured feedback per beat
- Overall recommendation: approve / revise / restructure

**Step 7: Iteration**
- Director reviews evaluation scores + panel images
- Director decides: Approve / Revise / Change approach
- If Revise: provide feedback text → Realize Agent refines → Evaluate again
- If Change approach: return to Exploration mode for that beat
- If Approve: beat marked as approved, move to next beat or Export

**Step 8: Export**
- All approved beats assembled into storyboard sequence
- Output: `storyboard.json` with ordered panel references + metadata
- Optional: generate a visual storyboard PDF

---

## 3. Per-Beat State Machine

Each beat follows its own mini state machine within the overall workflow:

```
PENDING → EXPLORING → SELECTED → REALIZING → EVALUATING → 
  ├── APPROVED → (next beat)
  ├── REVISING → REALIZING (loop, max 3x)
  └── RESTRUCTURING → EXPLORING (change approach)
```

Beat lifecycle:

| State | Description | Duration Estimate |
|-------|-------------|-------------------|
| PENDING | Awaiting exploration | 0s (initial) |
| EXPLORING | Generating options | 5-10s |
| SELECTED | User chose direction | 10-30s (user time) |
| REALIZING | Generating panels | 10-60s (API call) |
| EVALUATING | Scoring quality | 3-5s |
| APPROVED | Director sign-off | 5-15s (user time) |
| REVISING | Awaiting director feedback + regeneration | 30-120s |
| RESTRUCTURING | Changing creative direction | 10-30s |

---

## 4. Error Handling

| Error | Detection | Recovery |
|-------|-----------|----------|
| Intent Token incomplete | Validate at every state transition | Return to Framing for clarification |
| Agent timeout (>60s) | Orchestrator timeout monitor | Retry once. If fails again, report to Director with partial output |
| Image generation fails | Realize Agent catches API error | Retry with different parameters. After 3 failures, suggest text-only panel |
| Evaluate returns contradictory scores | Cross-criterion variance > 0.4 | Flag for Director review, don't auto-recommend |
| User disappears mid-workflow | No response for >15min | Save checkpoint, notify user, enter pause state |
| Recursive call depth exceeded | Track call stack depth > 5 | Halt recursion, flatten to sequential, notify Director |

**Reference:** [Decision_Architecture.md](../11_Decisions/Decision_Architecture.md) §4.4 — Escalation Paths

---

## 5. AGE^T Primitive Execution Detail

### 5.1 Attend Primitive

```
Attend(context):
  1. Receive: raw_input or intent_token or work_item
  2. Parse: Extract key elements (domain, subject, constraints)
  3. Focus: Direct attention to relevant subset based on current stage
  4. Output: Focused attention vector (what matters NOW)
  
Example (Frame Agent):
  Input: "Create storyboard for fantasy quest..."
  Attend: Extract {domain: storyboard, genre: fantasy, elements: [hero, village, dawn, departure]}
  Output: Focus vector = {primary_subject: hero, setting: village, time: dawn, emotional_context: hopeful}
```

### 5.2 Generate Primitive

```
Generate(focus, constraints):
  1. Receive: Attention vector + constraints from Intent Token
  2. Produce: N variations within constraint space
  3. Diversity: Ensure options are meaningfully different (not N copies of the same)
  4. Output: Array of generated options
  
Example (Explore Agent):
  Input: {beat: "hero waking at dawn", constraints: {style: cinematic realism, panel_count: min5_max15}}
  Generate: 5 panel descriptions
  Output: [{description: "Wide shot, hero's silhouette through misty window..."}, ...]
```

### 5.3 Evaluate Primitive

```
Evaluate(output, criteria):
  1. Receive: Generated output + quality criteria from Intent Token
  2. Score: 0.0-1.0 per criterion
  3. Aggregate: Weighted overall score
  4. Recommend: Approve / Revise / Restructure
  5. Output: scores + feedback
  
Example (Evaluate Agent):
  Input: {panel_images: [...], criteria: [silhouette_readability:0.2, emotional_clarity:0.3, ...]}
  Evaluate: Score each criterion, produce feedback
  Output: {scores: {emotional_clarity: 0.82, ...}, overall: 0.78, recommendation: "approve"}
```

### 5.4 Transform Primitive

```
Transform(original, evaluation):
  1. Receive: Original output + evaluation results
  2. Identify: Which aspects need changing based on evaluation gaps
  3. Modify: Adjust parameters, regenerate with new constraints
  4. Output: Transformed version
  
Example (Realize Agent during refinement):
  Input: {panel: "hero at dawn (existing)", feedback: "darkness needs to feel mysterious not scary"}
  Transform: Adjust generation prompt: "add warm golden hues, soft mist, reduce contrast"
  Output: Refined panel image
```

---

## 6. Recursion Control

From the adversarial review, recursion is a known risk ([COS_v4_Adversarial_Review.md](../01_Capability_Architecture/COS_v4_Adversarial_Review.md) §6 — Realize calls Explore, which calls Evaluate, which calls Realize...).

### Guards

```
MAX_DEPTH = 5        // Maximum nested function calls
MAX_ITERATIONS = 10   // Maximum iterations per beat
CONVERGENCE_THRESHOLD = 0.05  // If improvement < 5%, stop
TIMEOUT_PER_CALL = 60         // seconds
```

### Convergence Detection

```
if abs(score_current - score_previous) < CONVERGENCE_THRESHOLD:
    halt_recursion()
    recommend_accept_current()
```

---

*Next document: [06_Build_Roadmap.md](06_Build_Roadmap.md)*
