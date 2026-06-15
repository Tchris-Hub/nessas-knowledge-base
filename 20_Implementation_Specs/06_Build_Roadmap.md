# COS Implementation Specifications — Build Roadmap

**Date:** June 15, 2026
**Author:** Chioma (Systems Architect)
**Builder:** Antigravity
**Reference:** [COS_Practicality_Review.md](../01_Capability_Architecture/COS_Practicality_Review.md) §5 — 30-Day Prototype Plan

---

## 1. Phasing Overview

```
Phase 0: Foundation    (Week 1)   Intent Token + Orchestrator
Phase 1: Core Loop     (Week 2)   Frame → Explore → Select agents
Phase 2: Output        (Week 3)   Realize → Evaluate agents  
Phase 3: Integration   (Week 4)   Full workflow + testing + demo
```

**Total MVP:** ~4 weeks for a working storyboard creation system.

**Reference:** [COS_Practicality_Review.md](../01_Capability_Architecture/COS_Practicality_Review.md) §5 — 30-Day Prototype Plan

---

## 2. Build Order (Day-by-Day)

### Phase 0: Foundation (Days 1-5)

**Goal:** Project structure, Intent Token, Orchestrator skeleton.

| Day | Task | Deliverable | Dependencies | Verifiable |
|-----|------|-------------|--------------|------------|
| 1 | Set up project structure + directory scaffolding | `projects/`, `configs/`, `agents/` directories | None | `ls projects/` shows expected structure |
| 1 | Write Intent Token JSON schema + validator | `schemas/intent_token_v1.json`, validation function | None | 5 hand-written Intent Tokens pass validation |
| 2 | Write dummy Intent Token for testing | `test/fixtures/test_intent.json` | Schema | Fixture loads and validates |
| 2 | Build Orchestrator skeleton | `orchestrator.py` — loads Intent Token, routes to agents | Project structure | `orchestrator.run("test_intent.json")` doesn't crash |
| 3 | Implement file-based state persistence | read/write/update Intent Token, work items, checkpoints | Orchestrator skeleton | Intent Token written + read back identically |
| 3 | Implement checkpoint save/load | Checkpoint at each state transition | State persistence | Save at step 2, load from step 2, continue |
| 4 | Build agent base class + message protocol | `BaseAgent` with standard contract | State persistence | Agent receives message, processes, returns result |
| 4 | Implement orchestrator → agent routing | Agent registry + dispatch by name | Base agent class | `dispatch("frame_agent", payload)` calls correct agent |
| 5 | Integration test: empty workflow | Orchestrator creates project → completes → exports | All of Phase 0 | End-to-end run with dummy agents returns clean output |
| 5 | **BUILD GATE: Phase 0 complete** | All tests pass | — | ✓ Go / ✗ Block |

**Assumption validated in Phase 0:**
- A1: JSON file-based state is fast enough for MVP
- A2: Agent base class provides sufficient abstraction

---

### Phase 1: Core Loop (Days 6-12)

**Goal:** Frame → Explore → Select agents working. User can see story beats and choose directions.

| Day | Task | Deliverable | Dependencies | Verifiable |
|-----|------|-------------|--------------|------------|
| 6 | Build Frame Agent (prompt-based) | Takes raw text → structured Intent Token with beats | Base agent class | 3 test scripts parsed into correct beats |
| 7 | Build Frame Agent clarifying questions | Identifies gaps, returns questions for user | Frame Agent | Missing mood/style produces question; complete brief does not |
| 8 | Build Explore Agent (per beat) | Takes Intent Token + beat → 5 panel descriptions | Frame Agent | 5 distinct panel options generated |
| 9 | Build Explore Agent diversity check | Deduplicate similar options, ensure meaningful variation | Explore Agent | Options differ in composition, angle, or mood |
| 10 | Build Select Agent (UI-mediated) | Presents options, records user choice | Explore Agent | Selection recorded in Intent Token |
| 11 | Wire up: Frame → Explore → Select end-to-end for 1 beat | User submits brief → sees 5 options → picks one | All Phase 1 agents | End-to-end works for single beat |
| 12 | **BUILD GATE: Phase 1 complete** | 5 test briefs processed through Frame→Explore→Select | — | ✓ Go / ✗ Block |

**Assumption validated in Phase 1:**
- B1: Frame Agent can parse scripts into meaningful story beats
- B2: Explore Agent produces diverse, useful panel options
- B3: Director can make selection decisions from text descriptions

---

### Phase 2: Output (Days 13-19)

**Goal:** Realize → Evaluate agents working. Storyboard panels generated and scored.

| Day | Task | Deliverable | Dependencies | Verifiable |
|-----|------|-------------|--------------|------------|
| 13 | Build Realize Agent (image generation) | Takes selected option → panel image | Image gen API access | Panel image generated and saved to `artifacts/` |
| 14 | Build Realize Agent prompt construction | Maps beat description + mood + style → API prompt | Realize Agent | Prompt produces image matching beat description |
| 15 | Build Realize Agent self-evaluation | Score: does panel match beat description? | Realize Agent | Self-eval scores correlate with human judgment on 5 test images |
| 16 | Build Evaluate Agent (5 criteria scores) | Scores each panel on all 5 quality criteria | Realize Agent | Scores produced for all criteria, overall computed |
| 17 | Build Evaluate Agent feedback construction | Generates structured feedback per criterion | Evaluate Agent | Feedback mentions specific panel elements, not generic text |
| 18 | Wire up: Realize → Evaluate → Iteration | Panels generated, scored, feedback produced | All Phase 2 agents | Loop works: generate → evaluate → feedback → regenerate |
| 19 | **BUILD GATE: Phase 2 complete** | 5 test panels generated, scored, iterated | — | ✓ Go / ✗ Block |

**Assumption validated in Phase 2:**
- B4: Image generation can produce storyboard-quality panels from text descriptions
- B5: Evaluate Agent scores correlate with human judgment (r > 0.7 target)

---

### Phase 3: Integration (Days 20-28)

**Goal:** Full storyboard workflow, multi-beat pipeline, evaluation + demo.

| Day | Task | Deliverable | Dependencies | Verifiable |
|-----|------|-------------|--------------|------------|
| 20 | Chain all 5 agents for full storyboard sequence | Multi-beat workflow (5-15 beats) | All agents | Full sequence: brief → all beats explored → selected → realized → evaluated |
| 21 | Implement iteration loop (Director feedback → Realize → Evaluate) | Up to 3 iterations per beat | Full chain | Feedback text → panel update → re-evaluation |
| 22 | Build storyboard assembly | All approved panels → ordered JSON sequence | Full chain + iteration | `storyboard.json` with correct panel order and metadata |
| 23 | Build Director dashboard (CLI or simple web UI) | Show options, panels, scores, accept feedback | Storyboard assembly | User can see all panels, give feedback, approve |
| 24 | Write 10 test briefs covering diverse storyboard scenarios | Test suite with ground-truth expectations | Director dashboard | Each brief processed without errors |
| 25 | Baseline comparison: Intent Token vs raw prompt | 10 outputs scored blindly | Test suite | Compare intent fidelity scores across conditions |
| 26 | Bug-fix and polish | All critical issues resolved | Baseline comparison | Known issues tracked and resolved |
| 27 | Demo prep: best 3 examples + comparison report | Demo materials | Bug fixes | Director can present working storyboard system |
| 28 | **BUILD GATE: Phase 3 complete — MVP ready** | All acceptance criteria met | — | ✓ Ship / ✗ Fix |

**Acceptance Criteria (Phase 3 gate):**

| # | Criterion | Target | Pass/Fail |
|---|-----------|--------|-----------|
| 1 | End-to-end workflow completes for 10/10 test briefs | 100% | |
| 2 | Output recognizable as storyboard to third party | Human judge confirms | |
| 3 | Iteration loop: feedback → panel change in <2 iterations | 2 iterations | |
| 4 | Intent Token adds value over raw prompt | +20% fidelity | |
| 5 | Evaluate scores correlate with human judgment | r > 0.7 | |
| 6 | Full sequence produced in <30 minutes | <30 min | |

---

## 3. What NOT to Build (and Why)

| Feature | Reason Excluded | When |
|---------|----------------|------|
| **Database** | JSON files are sufficient for single-project single-user MVP | Phase 2 |
| **Multi-user** | MVP is single-Director | Phase 3+ |
| **Full Capability Registry** | Hardcode 5 capabilities for storyboard domain | Phase 2 |
| **Multiple AI providers** | Pick one image gen API, hardcode it | Phase 2 |
| **Auto-approval** | Director reviews everything in MVP | Phase 3 |
| **Full Braintrust** | Single Evaluate agent with rubric is sufficient | Phase 3+ |
| **Model B (Capability Network)** | Extremely complex. MVP uses sequential orchestration. | Phase 4+ stretch |
| **USD/format abstraction** | Single output format for MVP (JSON + PNG) | Phase 3+ |
| **Real-time streaming** | Polling-based workflow status is fine | Phase 3+ |

**Reference:** [Architecture_Changing_Discoveries.md](../11_Decisions/Architecture_Changing_Discoveries.md) §5 — "Model B should not be built in parallel" and [COS_Practicality_Review.md](../01_Capability_Architecture/COS_Practicality_Review.md) §7 — "What NOT to build yet"

---

## 4. Expansion Path After MVP

```
Phase 1: STORYBOARD MVP (4 weeks)
  │
  ▼
Phase 2: WORKFLOW EXPANSION (6-8 weeks)
  ├── Layout workflow (storyboard → 3D scene blocking)
  ├── Environment workflow (layout → environment creation)
  ├── Capability Registry (database + schema)
  └── Agent handoff protocols + parallel execution
  
  │
  ▼
Phase 3: FULL COS CORE (8-12 weeks)
  ├── Character workflow (design → model → rig)
  ├── Braintrust quality system
  ├── Human-in-the-loop evaluation refinement
  ├── Quality heuristic validation sprint
  └── Director learning + preferences
  
  │
  ▼
Phase 4: PRODUCTION READY (12+ weeks)
  ├── Multi-tool orchestration (Blender adapter)
  ├── Model B: Graph-based routing (conditional)
  ├── Multi-user collaboration
  ├── Asset versioning + non-destructive layering
  └── Cinematic shot pipeline
```

---

## 5. Key Decision Gates

| Gate | Trigger | Question | Outcome Options |
|------|---------|----------|-----------------|
| **G1** | End of Phase 0 | Does file-based state work for MVP? | Continue / Switch to DB |
| **G2** | End of Phase 1 | Do Frame/Explore/Select produce useful output? | Continue MVP / Switch workflows |
| **G3** | End of Phase 2 | Does Evaluate correlate with human judgment? | Continue / Defer Evaluate to human-only |
| **G4** | End of Phase 3 | Does COS outperform raw generation? | Scale / Pivot / Document learnings |
| **G5** | Post-MVP | Which workflow next? Layout or Character? | Follow expansion path / Build custom |

**Reference:** [Architecture_Changing_Discoveries.md](../11_Decisions/Architecture_Changing_Discoveries.md) — Each gate corresponds to validating specific assumptions.

---

## 6. Files to Create (Antigravity Checklist)

```
cos-storyboard-mvp/
├── orchestrator.py               # Main workflow coordinator
├── agents/
│   ├── base_agent.py             # Abstract base class
│   ├── frame_agent.py            # Frame Agent (parses intent)
│   ├── explore_agent.py          # Explore Agent (generates options)
│   ├── select_agent.py           # Select Agent (presents + records choices)
│   ├── realize_agent.py          # Realize Agent (generates images)
│   └── evaluate_agent.py         # Evaluate Agent (scores quality)
├── schemas/
│   └── intent_token_v1.json      # JSON Schema for Intent Token
├── storage/
│   ├── project_store.py          # Read/write/update project files
│   └── checkpoint.py             # Checkpoint save/load
├── test/
│   ├── fixtures/
│   │   ├── test_intent.json      # Sample Intent Token
│   │   ├── brief_quest.txt       # Test brief: fantasy quest
│   │   ├── brief_thriller.txt    # Test brief: thriller opening
│   │   └── ... (10 total)
│   ├── test_orchestrator.py
│   ├── test_frame_agent.py
│   ├── test_explore_agent.py
│   └── ... (per agent)
├── configs/
│   ├── capability_registry.json  # Hardcoded capabilities
│   └── agent_profiles/          # Per-agent configuration
└── README.md                     # This spec + build instructions
```

---

*End of Implementation Specifications*
