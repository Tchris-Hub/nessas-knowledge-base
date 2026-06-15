# COS Implementation Specifications — Memory Architecture

**Date:** June 15, 2026
**Author:** Chioma (Systems Architect)
**Reference:** [COS_Architecture_v4_Creativity_First.md](../01_Capability_Architecture/COS_Architecture_v4_Creativity_First.md) §6.3

---

## 1. Philosophy

In MVP, everything is file-based JSON. No database. The memory architecture is deliberately minimal:

| Layer | Storage | Data |
|-------|---------|------|
| Project state | JSON files | Intent Token, Work Items, Agent States |
| Artifact storage | Directory | Panel images, iteration outputs |
| Agent memory | Process-local | None persisted in MVP — stateless agents |
| User preferences | JSON file | Director profile, style preferences |

**Assumption:** This is sufficient for the MVP storyboard workflow. JSON file I/O is well-understood, debuggable, and trivially inspectable by the Director.

**Risk:** JSON file access may become a bottleneck at scale (>100 concurrent projects).
**Mitigation:** Defer to Phase 2. Switch to SQLite or file-based key-value store if needed.

---

## 2. Directory Structure

```
projects/
  {project_id}/                          # e.g., "fantasy-quest-opening"
    intent_token.json                     # The Intent Token — single source of truth
    work_items/                           # Work items by ID
      001-frame.json
      002-explore-beat-01.json
      003-select-beat-01.json
      ...
    artifacts/                            # Generated outputs
      beats/
        beat-01/
          explore/
            option-1.png
            option-2.png
            ...
          realize/
            panel-final.png
            iteration-1.png
            iteration-2.png
        ...
      sequence/                           # Compiled storyboard
        storyboard.json                   # Ordered panel references
        storyboard_export.pdf             # (optional — deferred)
    checkpoints/                          # Workflow state snapshots
      step-01-framing.json
      step-02-exploration.json
      ...
    
config/
  capability_registry.json               # Hardcoded capability definitions
  agent_profiles/                         # Agent configuration
    frame_agent.json
    explore_agent.json
    select_agent.json
    realize_agent.json
    evaluate_agent.json
    
users/
  {user_id}.json                          # Director profile: preferences, style history
```

---

## 3. What Each File Stores

### 3.1 Intent Token (`intent_token.json`)

The spine of the system. Schema defined in [02_Data_Models.md](02_Data_Models.md). This file is the single source of truth for all project state.

**Read by:** All agents (read-only for Explore, Select, Realize; read-write for Frame, Evaluate)
**Written by:** Frame Agent (initial creation + clarification), Orchestrator (state updates), Evaluate (quality scores)
**Updated by:** Every agent appends to the `history` array

### 3.2 Work Item Files (`work_items/{id}.json`)

One file per discrete unit of work. Tracks individual task status.

```
{
  "work_item_id": "wi-explore-beat-01",
  "project_id": "fantasy-quest-opening",
  "type": "explore_beat",
  "status": "completed",
  "assigned_agent": "explore_agent",
  "input": { "beat_id": "beat-01", ... },
  "output": { "options": [...] },
  "created_at": "...",
  "started_at": "...",
  "completed_at": "...",
  "retry_count": 0
}
```

### 3.3 Checkpoints (`checkpoints/{name}.json`)

Workflow state snapshots for recovery. Basic JSON dump of project state at a given step.

```
{
  "checkpoint_id": "step-02-exploration",
  "project_id": "fantasy-quest-opening",
  "stage": "exploration",
  "completed_agents": ["frame_agent"],
  "pending_beats": ["beat-01", "beat-02", "beat-03", "beat-04", "beat-05"],
  "current_work_items": [...],
  "timestamp": "..."
}
```

### 3.4 Director Profile (`users/{user_id}.json`)

```
{
  "user_id": "director-001",
  "preferences": {
    "default_panel_count": 8,
    "default_aspect_ratio": "16:9",
    "default_style_preference": "cinematic realism",
    "exploration_option_count": 5,
    "max_iterations_per_beat": 4
  },
  "style_history": [
    {
      "project_id": "fantasy-quest-opening",
      "domains_used": ["storyboard"],
      "mood_patterns": ["hopeful", "melancholic"],
      "approval_rate": 0.85
    }
  ]
}
```

---

## 4. Agent Memory Model

**MVP agents are stateless.** Each agent:
- Reads its input from the Intent Token + work item
- Performs its function via LLM call
- Writes its output to the Intent Token + work item
- Forgets everything after completion

**Why stateless in MVP:**
- Simplifies debugging (no hidden state)
- Makes agent crashes non-fatal (re-run with same input)
- Forces all state to live in the Intent Token (which is the design intent)

**When to add state:** Phase 3+ when agents need to learn from past iterations (e.g., "The Director tends to prefer warm color palettes").

---

## 5. Intent Fidelity Tracking

Intent fidelity is tracked at every handoff point:

```
Frame → Intent formed:                         intent_fidelity = 0.85
Explore → Options generated:                   intent_fidelity = 0.80 (slight drift from interpretation)
Select → Direction chosen:                     intent_fidelity = 0.82 (user correction improves it)
Realize → Panels generated:                    intent_fidelity = 0.75 (generation model introduces artifacts)
Evaluate → Scores computed:                    intent_fidelity = 0.72 (evaluation identifies gaps)
Refine → Adjustments applied:                  intent_fidelity = 0.78 (adjustments improve match)
Final → Director approved:                     intent_fidelity = 0.85 (user satisfaction = intent fidelity)
```

**The goal:** Intent fidelity should never decrease by more than 0.15 between adjacent steps. If it does, that step's contract needs renegotiation.

**Reference:** [Architecture_Changing_Discoveries.md](../11_Decisions/Architecture_Changing_Discoveries.md) §U2 — "How Much Creative Intent Is Lost at Each Layer Boundary?"

---

*Next document: [05_State_Machines_and_Workflows.md](05_State_Machines_and_Workflows.md)*
