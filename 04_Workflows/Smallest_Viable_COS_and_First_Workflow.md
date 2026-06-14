# Smallest Viable COS & First Workflow Analysis

**Document ID:** COS-04-WF-001
**Date:** June 14, 2026
**Purpose:** Identify the minimum viable Creative Operating System and recommend the first user workflow to master.
**Source Documents:** COS_Architecture_v1.md, Specialist_Capability_Domains.md (47 capabilities), Capability_Dependency_Map.md, Decision_Architecture.md, Specialist Architecture files (Pixar, VFX, Game, Directors, Story/Concept, TD/Pipeline)

---

## PART 1 — Smallest Viable COS

### The Core Premise

The COS vision is: "What if every creative production had the equivalent of Pixar's Braintrust, an elite VFX pipeline TD team, a game studio's iterative playtest loop, and an experienced director's creative judgment — built into the infrastructure itself?"

The MVP must answer this question: **Can we produce a recognizable creative output through multi-capability orchestration, with a feedback loop, quality evaluation, and director-driven iteration?** It does not need to be cinematic quality. It needs to *feel* like a creative production system, not a single tool.

### Analysis: What Is the Shortest Dependency Chain?

From the Capability Dependency Map, the shortest production chains that produce a complete, recognizable visual output are:

| Chain | Capabilities | Link Count | Output |
|-------|-------------|------------|--------|
| Environment (static) | S04 → V01 → V03 → V04 → V05 → P05 | 6 | Rendered environment image |
| Character Asset | S04 → C01 → C04 → C05 → A01 → V05 → P05 | 7 | Rendered animated character |
| Material/Surface | C04 → C06 → C07 → V08 → V05 → P05 | 6 | Shaded lookdev render (depends on model) |
| Storyboard (narrative) | S02 → S01 → V04 → A01 → V07 → V05 → P05 → D08 | 8 | Animated story sequence |
| VFX Integration | A01 → V07 → V05 → P05 → D08 | 5 | Composited FX shot (depends on animation) |

**The shortest chain that produces a standalone output is the Environment chain at 6 production capabilities.** However, we must add: the Director (D01) who provides creative vision and approval, a quality evaluation capability (from Quality domain or FIL), and the Pipeline TD (P04) infrastructure that enables tool integration. This brings us to ~9 capabilities total.

**But can we cut further?** Yes — by stripping non-essential stages:

1. **Remove V04 (LayoutArtist)** for static environments — use a fixed or procedural camera. Saves 1 link.
2. **Remove explicit D08 (CompSup)** — for a single render, no compositing is needed beyond the render. Saves 1 link.
3. **Fold Quality evaluation into the DEL/FIL layer generically** rather than requiring a dedicated Q01 Braintrust capability. The COS's Feedback & Iteration Layer (L7) provides this natively.

This yields the absolute minimum chain: **S04 → V01 → V03 → V05 → P05** = 5 production capabilities + D01 direction + P04 infrastructure + FIL quality = **8 abstracted capability units**.

### 1) How Many Capabilities Are Needed?

**8 core capabilities** from the 47 specialist capabilities (plus 2 internal COS layers that serve as integrated capabilities):

| # | Capability ID | Capability Name | COS Layer | Role in MVP |
|---|--------------|----------------|-----------|-------------|
| 1 | **D01** | FilmDirector (User as Director) | L1 (DEL) | Provides creative vision, reviews output, approves/rejects |
| 2 | **S04** | Visual Development Artist | L2 (CIL) | Establishes visual language, style, color philosophy |
| 3 | **V01** | Environment Concept Artist | L2 (CIL) | Designs environment mood, architecture, atmosphere |
| 4 | **V03** | Environment Artist | L3 (POL)/L6 (TAL) | Creates 3D environment meshes, terrain, materials |
| 5 | **V05** | Lighting TD | L3 (POL)/L6 (TAL) | Places lights, sets mood, configures render |
| 6 | **P05** | Rendering TD | L3 (POL) | Manages render execution, produces final frames |
| 7 | **FIL (L7)** | Feedback & Iteration (integrated) | L7 (FIL) | Evaluates quality, structures feedback, tracks iterations |
| 8 | **P04** | Pipeline TD | L6 (TAL) | Tool adapters, automation, data transfer between capabilities |

**Total: 6 specialist capabilities + 2 integrated COS capabilities = 8.**

If we want to include basic asset versioning (recommended), add P11 (Asset Manager) = **9 capabilities total**.

### 2) Which Capabilities?

The 8 capabilities listed above. The critical insight is what we **exclude**:

- **No Screenwriter (S02)** — no text-based narrative needed
- **No StoryArtist (S01)** — no storyboarding
- **No CharDesigner (C01)** — no characters
- **No DigitalModeler (C04)** — environment artist handles their own geometry
- **No Rigger (C05)** — no rigging
- **No Animator (A01)** — no animation
- **No FXArtist (V07)** — no simulation
- **No ShadingTD (C07)** — surface work absorbed by environment artist + lighting
- **No Braintrust (Q01)** — quality evaluation is handled by the FIL layer directly
- **No Producer (P01)** — no scheduling/budget infrastructure in MVP
- **No Compositing Supervisor (D08)** — single render doesn't need comp

This is a **radical simplification**: we eliminate 38 of 47 specialist capabilities.

### 3) Which Domain?

**Primary Domain: Visual Domain (DOMAIN 3)**
- S04 (VisDev) from Story Domain
- V01, V03, V05 from Visual Domain
- P05 from Production Domain
- P04 from Production Domain (infrastructure)

**Secondary Domains Tapped:**
- Direction Domain (D01)
- Quality Domain (via integrated FIL)

The MVP is centered on the **Visual Domain** because:
- It has the shortest dependency chain to a visible output (6 links)
- Environment creation doesn't require characters, rigging, or animation
- Visual output is immediately recognizable and evaluable
- It exercises the core COS layers without needing the full complexity

### 4) How Many Tools to Integrate?

**2 tools minimum:**

| Tool | Role | COS Interface |
|------|------|---------------|
| **Blender** (or equivalent 3D suite) | Environment modeling, texturing, lighting, rendering | L6 (TAL) adapter — procedural scene generation, material application, render submission |
| **COS Dashboard / CLI** | Director interaction, feedback, iteration tracking | L1 (DEL) — the director's interface to the system |

**Optional 3rd tool:** A simple image viewer for review (browser-based or integrated into the COS dashboard).

The key design choice: **Blender handles ALL production work** (modeling + texturing + lighting + rendering). In the full COS, these would be separate tool adapters (Blender for modeling, Substance for texturing, Katana for lighting, RenderMan for rendering). In the MVP, one tool proves the orchestration concept.

### 5) What's the User Interface?

**Single interface: The Director's Chat Interface (DEL)**

The user interacts with the COS through a **conversational, director-centric interface** — a chat or command-line that feels like talking to a production team, not operating software. The interface has three modes:

```
┌─────────────────────────────────────────────────────┐
│  COS DIRECTOR INTERFACE — Project: Alpine_Lake      │
├─────────────────────────────────────────────────────┤
│                                                     │
│  [Director] Create a serene alpine lake scene at    │
│             golden hour. Mist rising, pine trees,   │
│             distant snow-capped mountains.          │
│                                                     │
│  [COS] Understood. Generating 5 environment         │
│        concepts for your review...                  │
│                                                     │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────┐  ┌─────┐
│  │ Option 1│  │ Option 2│  │ Option 3│  │Opt 4│  │Opt 5│
│  │ Misty   │  │ Clear   │  │ Storm   │  │Dawn  │  │Dusk │
│  └─────────┘  └─────────┘  └─────────┘  └─────┘  └─────┘
│                                                     │
│  [Director] I like Option 1. Refine with more       │
│             dramatic lighting — stronger sun rays   │
│             through the mist.                        │
│                                                     │
│  [COS] Refining. Adjusting lighting, adding         │
│        volumetric rays... [rendering]                │
│                                                     │
│  [Preview Image Displayed Here]                      │
│                                                     │
│  [COS] Quality evaluation: Silhouette readability   │
│        0.82 ✓ | Tonal consistency 0.79 ✓ |          │
│        Reference grounding 0.74 △ (suggested)       │
│                                                     │
│  [Director] Approve. Save as final.                  │
│                                                     │
└─────────────────────────────────────────────────────┘
```

**Key UI principles:**
- Director speaks in natural language (no technical commands)
- COS shows intermediate options (exploration mode, 3-5 thumbnails)
- Director selects, COS refines (refinement mode)
- Quality scores shown alongside previews
- One-click approval or natural-language feedback

### 6) What's the User Experience of Using the MVP?

**The director's experience flow:**

**Step 1 — Brief (2 minutes)**
The director types or speaks: "Create [description of scene] in [style reference]. Include [must-have elements]. The mood should be [emotional quality]."

**Step 2 — Exploration (30-60 seconds)**
The COS generates 3-5 concept thumbnails (low-res, fast renders) showing different interpretations of the brief. These are visibly rough — the goal is direction-finding, not polish.

**Step 3 — Selection & Refinement Direction (30 seconds)**
The director picks one option and gives qualitative feedback: "I like the composition of #2 but the lighting of #1 — make it warmer."

**Step 4 — Refinement (1-3 minutes per iteration)**
The COS produces a higher-quality render incorporating the feedback. Quality signals are displayed. The director can iterate 2-4 times, each time giving increasingly specific feedback.

**Step 5 — Approval (10 seconds)**
The director clicks "Approve" or says "This is done." The final render is saved with metadata (intent, iterations, quality scores).

**Total time from brief to final render: ~5-15 minutes for a single static scene.**

**What it feels like:** Working with a very fast, very literal concept artist who shows you options, takes direction well, and never gets tired of iterations. The director never touches a 3D tool.

### 7) What Output Does It Produce?

**Primary output:** A single rendered environment image (PNG/EXR, up to 4K resolution) with:
- Full 3D scene geometry (terrain, vegetation, architecture, sky)
- Lighting and atmosphere (time of day, weather effects, volumetric effects)
- Material fidelity (water, rock, foliage, snow)
- Camera composition (framing, depth of field, focal length)

**Secondary outputs:**
- A structured creative brief (machine-readable intent record)
- An iteration history (all versions with feedback mapped to scores)
- Quality evaluation report per iteration
- The COS's learned preferences from the session

### 8) What Does It NOT Do Yet?

The MVP explicitly does NOT include:

| Feature | Why Excluded | When It Would Be Added |
|---------|-------------|----------------------|
| **Characters** | Requires C01→C04→C05→A01 chain (4 extra capabilities, rigging is high-complexity) | Workflow expansion after MVP validation |
| **Animation** | Requires rigged characters + keyframe/mocap pipeline | Workflow expansion |
| **Narrative/Story** | Requires S02→S01 chain + editorial | Workflow expansion |
| **VFX/Simulation** | Requires V07/A05 + caching infrastructure | Workflow expansion |
| **Multiple Shots** | Requires sequencing, editorial, shot tracking | Workflow expansion |
| **Game-ready Assets** | Requires C03 path with poly budgets, engine optimization | Separate workflow track |
| **Collaborative Review** | Only single-director model | Multi-user DEL expansion |
| **Schedule/Budget Tracking** | Requires P01/P02/P03 production management chain | Post-MVP production layer |
| **Multi-tool Orchestration** | Single tool (Blender) handles all stages | L6 (TAL) expansion |
| **Full Braintrust Feedback** | Q01 requires multiple expert personas with no authority | FIL maturity |
| **Asset Library/Versioning** | Basic file saving only, no USD/ShotGrid integration | APML maturity |
| **Non-destructive Layering** | Single monolithic scene, no USD composition | APML maturity |

---

## PART 2 — First Workflow to Master

### Workflow Options Analysis

#### Option A: Character Creation (Single Character: Concept → Rigged Model)

| Dimension | Assessment |
|-----------|-----------|
| **Capabilities Required** | 7: S04→C01→C04→C05 (core) + D01 + Q + P04. Needs VisDev (style), CharDesigner (design), DigitalModeler (geometry), Rigger (skeleton/controls). |
| **Tools to Integrate** | 3-4: 3D modeling (Blender/ZBrush), UV/texturing (Substance), rigging (Blender/Maya), plus COS orchestration |
| **Complexity** | **High.** Rigging is the most technically demanding capability in the entire pipeline. A bad rig makes the whole output unusable. Topology decisions cascade through deformation, animation, and rendering. The Rigger capability is a bottleneck (C05 has 6 connections and no substitute). |
| **How Well It Demonstrates the Vision** | **Moderately.** A fully rigged character is impressive and shows the COS handling a multi-stage pipeline. But the final output (a rigged model) is not "finished creative content" — it's an intermediate asset. The most exciting part (animation) comes later. |
| **Risk if This Fails** | **Very High.** If rigging fails, the entire character pipeline collapses. Users would see a broken, unusable output — undermining confidence in the COS before any downstream workflow can save it. The C05 bottleneck is non-redundant. |
| **Future Workflows Unlocked** | Animation (character performance), Game-ready assets, Cinematic shots, Crowd simulation. The rigged character is the foundation of all character-driven work. |
| **Verdict** | Too risky for first workflow. High technical complexity, high dependency on getting topology/rigging right, and the output isn't independently "finished." |

#### Option B: Scene Creation (Complete Scene with Environment, Lighting, Props)

| Dimension | Assessment |
|-----------|-----------|
| **Capabilities Required** | 6: S04→V01→V03→V05→P05 (core) + D01 + Q + P04 = ~9 total. VisDev (style), EnvConcept (design), EnvArtist (modeling), LightingTD (lighting), RenderingTD (render). |
| **Tools to Integrate** | 2-3: 3D modeling/lighting/rendering (Blender or Unreal) + COS orchestration. V03 and V05 can share the same tool for MVP. |
| **Complexity** | **Medium.** Environment creation is well-understood, with fewer topological constraints than characters. Lighting is an artistic skill but technically simpler than rigging. The dependency chain is the shortest (6 links) with the most parallelism potential. |
| **How Well It Demonstrates the Vision** | **Strongly.** A complete rendered scene is immediately recognizable as "finished creative output." The director can see vision→execution in one cycle. The environment chain exercises the full stack: brief (CIL/L2) → orchestration (POL/L3) → tool execution (TAL/L6) → quality evaluation (FIL/L7) → approval (DEL/L1). |
| **Risk if This Fails** | **Medium.** Environment without characters can feel empty or generic. If lighting or rendering fails, the output is visibly bad (black frame, wrong colors, fireflies). But the chain is short enough to debug, and the individual stages have meaningful intermediate outputs (concept art is useful even without final render). |
| **Future Workflows Unlocked** | Layout (camera staging for scenes), Cinematic shots (env as backdrop), Matte painting (2D environment extensions), Game environments (environment modeling skills transfer). Does NOT directly unlock character or animation workflows. |
| **Verdict** | Strong candidate. Lowest-risk path to a recognizable "finished" output. Best shortest-chain demonstration. |

#### Option C: Advertisement Creation (Short Branded Visual, Quick Turnaround)

| Dimension | Assessment |
|-----------|-----------|
| **Capabilities Required** | 8+: S04→C01→V01→V03→C04→V05→P05 + D01 + Q + P04. Requires character + environment + product + text/typography + branding constraints — spans 4 domains. |
| **Tools to Integrate** | 4+: 3D modeling, texturing, lighting, rendering, compositing, potentially text/graphic design tools |
| **Complexity** | **High.** Advertisement requires integration across multiple domains (character, environment, graphic design) with rigid brand constraints. "Brand compliance" is a quality signal that's hard to automate. The output must be client-ready, not just "creative exploration." |
| **How Well It Demonstrates the Vision** | **Very Strongly.** A complete branded advertisement demonstrates the full COS vision end-to-end: intent → multi-domain creation → quality evaluation → client-ready output. It's commercially valuable immediately. |
| **Risk if This Fails** | **Very High.** Missing brand guidelines, awkward product placement, or generic-looking output destroys trust. The multi-domain requirements mean more failure modes. If the output looks like "generated art" rather than "professional advertisement," the vision feels cheap. |
| **Future Workflows Unlocked** | Brand asset management, multi-shot sequences, client review workflows, rapid iteration pipelines. |
| **Verdict** | Desirable but premature. Requires too many capabilities, too many tools, and carries too much brand-compliance risk for a first workflow. Better as a demonstration after character AND environment pipelines are mature. |

#### Option D: Storyboard Creation (Visual Sequence from Script — Front of Pipeline)

| Dimension | Assessment |
|-----------|-----------|
| **Capabilities Required** | 4: S02→S01 (core) + D01 + Q + P04. Screenwriter (script) + StoryArtist (storyboards). That's it. |
| **Tools to Integrate** | 1-2: Storyboarding/drawing tool (Procreate, Photoshop, or an AI image generation adapter) + COS orchestration. Storyboards are 2D images — no 3D toolchain needed. |
| **Complexity** | **Lowest of all options.** Storyboards are intentionally rough, cheap, and fast. The StoryArtist capability (S01) is designed for speed (100,000+ drawings per film). "Done" is defined by narrative clarity, not visual polish. No 3D geometry, no rigging, no lighting, no rendering. |
| **How Well It Demonstrates the Vision** | **Extremely Well.** Storyboarding IS the core COS vision in microcosm: the director communicates intent → the system interprets and generates visual interpretations → the director evaluates and gives feedback → the system iterates. The generate-evaluate cycle (from Story/Concept research) is the fundamental cognitive unit of all creative work. This workflow directly exercises L2 (CIL) — the Creative Intent Layer — which is the heart of the COS. |
| **Risk if This Fails** | **Lowest of all options.** Storyboards are disposable by nature. A bad storyboard costs nothing to redo. The 3-5x cost-of-change rule (from Story/Concept research) means changes at the storyboard stage are 3-5x cheaper than at later stages. Failure modes are low-stakes: wrong composition, unclear storytelling, missing beats — all fixable in the next iteration. |
| **Future Workflows Unlocked** | **ALL OF THEM.** Storyboards are the front of EVERY pipeline. Once the COS can generate storyboards from script:
  - Layout (V04) depends on storyboards
  - Animation (A01) depends on layout
  - VFX (V07) depends on animation
  - Everything downstream flows from this capability
  - Unlocks: Scene creation, cinematic shots, full narrative animation, commercial advertisement

  Storyboarding is the **keystone workflow** — mastering it unlocks every other workflow. |
| **Verdict** | **Best choice for first workflow.** |

#### Option E: Cinematic Shot Creation (Single High-Quality Cinematic Shot)

| Dimension | Assessment |
|-----------|-----------|
| **Capabilities Required** | 9+: S02→S01→V04→A01→V07→V05→P05→D08 (8 chain) + D01 + C01→C04→C05 (character chain needed for most shots) + Q + P04. Potentially 12+ capabilities. |
| **Tools to Integrate** | 6+: 3D modeling, rigging, animation, FX simulation, lighting, rendering, compositing |
| **Complexity** | **Highest of all options.** Requires the full 9-link production chain plus character pipeline. Every dependency must work. A single bad topology, wrong lighting, or mismatched composite ruins the shot. The longest chain leaves the most failure points. |
| **How Well It Demonstrates the Vision** | **Perfectly (if it works).** Nothing says "this is a real creative operating system" like a cinematic-quality rendered shot. This is the ultimate demonstration. |
| **Risk if This Fails** | **Catastrophic.** If any of the 9+ links fails, the output is visibly broken. Users never see a successful iteration cycle — they see a series of errors. The longest chain also means the longest debug cycle. One bad rig can waste days of work downstream. |
| **Future Workflows Unlocked** | All of them — but the reverse is also true: if the COS can do a cinematic shot, it can do everything upstream. However, the dependency is one-directional: mastering storyboards first would make cinematic shots easier. |
| **Verdict** | Too ambitious for first workflow. Save for "proof of full system" milestone after 3-5 workflow expansions. |

### Recommendation: Storyboard Creation

**The COS should master Storyboard Creation first.**

#### Justification

**1. Shortest dependency chain, lowest risk.**
Storyboarding requires only 4 capabilities (S02, S01, D01, Q) and 1-2 tools. It is the cheapest workflow to fail at — and the cheapest to iterate on. The 3-5x cost-of-change research finding means catching errors at the storyboard stage is 3-5x more efficient than catching them in layout, 10-15x more efficient than catching them in animation, and 20-30x more efficient than catching them in lighting.

**2. It directly exercises the COS's defining innovation: the Creative Intent Layer (L2).**
The CIL is what makes the COS different from a script-to-video generator. The CIL interprets, generates options, and translates ambiguous intent into structured production requirements. Storyboarding is the purest expression of this capability — the system reads a script and produces visual interpretations. The director's generate-evaluate cycle (5+ options) is the fundamental cognitive unit of all creative work (per Story/Concept research).

**3. Unlocks every downstream workflow.**
Storyboards feed directly into:
- Layout (V04) — the next critical bottleneck
- Animation (A01) — character performance
- VFX (V07) — effects integration
- Cinematography — shot composition decisions

Mastering storyboarding means the COS has solved the hardest creative translation problem (text → visual narrative intent). Every downstream workflow benefits from this foundation.

**4. The output is immediately useful and recognizable.**
A storyboard sequence is a legitimate creative deliverable. Directors use them for pitching, pre-visualization, and production planning. The COS is providing real value from day one — not just a tech demo but a working production tool.

**5. It establishes the feedback loop pattern.**
The Storyboard workflow is the simplest setting to test and refine:
- The FIL's feedback cadence (dailies rhythm)
- The Braintrust model (non-binding recommendations)
- The exploration→refinement mode switch
- The quality evaluation engine on creative (not technical) criteria

If the feedback loop doesn't work here, it won't work anywhere. If it does, it scales cleanly to every other workflow.

**6. It builds director trust early.**
Low risk means the director can experiment freely. By the time the COS expands to character creation or cinematic shots, the director already trusts the system's interpretation ability, feedback quality, and iteration discipline. Trust earned in storyboarding translates directly to willingness to delegate in production.

#### Storyboard MVP Specification

| Element | Definition |
|---------|-----------|
| **Input** | Script text or verbal pitch (natural language) + direction (tone, style references, emotional beats) |
| **Output** | 5-15 storyboard panels per sequence, with shot descriptions, camera notes, and timing annotations |
| **Capabilities Active** | S02 (Screenwriter) — parse script into story beats; S01 (StoryArtist) — generate visual panels; D01 (Director) — review, feedback, approval; FIL — quality evaluation, iteration tracking |
| **Tools** | 1 primary: image generation adapter (Stable Diffusion, Midjourney, or DALL-E via TAL) |
| **Quality Criteria** | Silhouette readability, emotional beat clarity, narrative coherence, pacing/rhythm, tonal consistency |
| **Iteration Model** | Exploration: 5 options per beat. Refinement: 2-4 iterations per selected option. |
| **Success Signal** | Director can assemble a story reel that communicates the full narrative to a third party |

#### Expansion Path After Storyboarding

```
Phase 1: STORYBOARD (FIRST) ─── Master text→visual intent translation
                                        │
                                        ▼
Phase 2: LAYOUT ───────────────── Master 3D camera staging from storyboards
   (Adds V04 capability, adds Blender as 3D tool)
                                        │
                                        ▼
Phase 3: ENVIRONMENT ──────────── Master environment creation for staged scenes  
   (Adds V01, V03 capabilities, expands Blender usage)
                                        │
                            ┌───────────┴───────────┐
                            ▼                       ▼
Phase 4a: ANIMATION      Phase 4b: CHARACTER
   (Adds A01, C05)          (Adds C01, C04)
                            │
                            ▼
Phase 5: CINEMATIC SHOT ─── Full pipeline integration
```

### Final Summary Table: First Workflow Options

| Criteria | Character | Scene | Ad | **Storyboard** | Cinematic Shot |
|----------|-----------|-------|----|----------------|----------------|
| Capabilities Required | 7 | 6 | 8+ | **4** | 9+ |
| Tools to Integrate | 3-4 | 2-3 | 4+ | **1-2** | 6+ |
| Complexity | High | Medium | High | **Low** | Very High |
| Vision Demonstration | Moderate | Strong | Very Strong | **Extremely Strong** | Perfect |
| Risk if Fails | Very High | Medium | Very High | **Lowest** | Catastrophic |
| Downstream Workflows Unlocked | Animation, Games | Layout, Cinematics | Brand, Multi-shot | **ALL** | All (upstream too) |
| **RECOMMENDATION** | ✗ | ✓ (backup) | ✗ | **✓ FIRST** | ✗ |

---

## Appendices

### Appendix A: Mapping MVP Capabilities to COS Layers

```
Layer 1 (DEL) ─── D01 (Director) — intent input, review, approval
    |
Layer 2 (CIL) ─── S04 (VisDev) + V01 (EnvConcept) — intent translation, exploration, brief creation
    |
Layer 3 (POL) ─── V03 (EnvArtist) + V05 (LightingTD) + P05 (RenderingTD) — workflow orchestration, stage management
    |
Layer 4 (KQL) ─── Integrated quality heuristics — silhouette readability, tonal consistency, reference grounding
    |
Layer 5 (APML) ─── Basic file versioning (minimal in MVP, stubbed for expansion)
    |
Layer 6 (TAL) ─── P04 (PipelineTD) — Blender adapter, data translation, execution environment
    |
Layer 7 (FIL) ─── Integrated feedback loop — iteration tracking, quality scoring, dailies rhythm
```

### Appendix B: What the MVP Exercises (vs. What It Skips)

| COS Feature | Exercised by MVP? | Notes |
|-------------|------------------|-------|
| Director ↔ System communication | ✓ YES | Core flow: brief → options → select → feedback → approve |
| Exploration → Refinement modes | ✓ YES | 3-5 options first, then refine selected |
| Generate-evaluate cycles | ✓ YES | Fundamental unit of creative work per Story/Concept research |
| Quality evaluation heuristics | ✓ YES | Creative signals (silhouette, tonal consistency, pacing) |
| Tool abstraction / multi-tool orchestration | PARTIAL | Single tool (Blender) but routed via TAL adapter — architecture is there |
| Non-destructive asset layering | ✗ SKIPPED | Requires USD/ShotGrid integration |
| Collaborative Braintrust feedback | ✗ SKIPPED | Single-director model only |
| Schedule/budget/resource management | ✗ SKIPPED | Production Management layer deferred |
| Revision loops and upstream propagation | PARTIAL | Feedback works, but no "upstream change cascades" in MVP |

### Appendix C: Key Architectural Principles Preserved in MVP

From the 10 architectural principles in COS_Architecture_v1.md:

| Principle | MVP Compliance |
|-----------|---------------|
| **Invisible by design** — Artist doesn't think about the pipeline | ✓ Director never touches the 3D tool — only the COS interface |
| **Feedback separated from authority** | ✓ FIL evaluates and recommends; Director decides |
| **Enforce via automation, not documentation** | ✓ Quality gates, dependency checks built into capability handoffs |
| **Protect creative intent above generated artifacts** | ✓ Every iteration preserves the brief and feedback lineage |
| **Ship 80%, iterate live** | ✓ This IS the principle — we're shipping the absolute minimum |
| **Separate exploration from refinement** | ✓ Explicit mode management with Director-driven mode switch |
| **Loop, not line** | ✓ Each storyboard iteration is a complete feedback loop |
| **Design for failure** | ✓ Storyboards are cheap — failure costs nothing |
| **Constraints are creative fuel** | ✓ Brief constraints (must-have, nice-to-have, open areas) structure the exploration |
| **Platform-independent core** | ✓ No code above TAL depends on any specific tool |

---

*End of document.*
