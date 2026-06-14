# Capability Dependency Map — Creative Operating System

**Version:** 1.0  
**Date:** June 14, 2026  
**Source:** Derived from Specialist_Capability_Domains.md (47 capabilities across 7 domains)  
**Purpose:** Comprehensive dependency map showing how every specialist capability connects to every other — data flow, decision flow, decision authority, critical chains, parallelizable paths, and bottleneck analysis.

---

## TABLE OF CONTENTS

1. [CAPABILITY MASTER LIST WITH SHORT NAMES](#1-capability-master-list-with-short-names)
2. [UPSTREAM DEPENDENCIES (What Each Capability Needs)](#2-upstream-dependencies-what-each-capability-needs)
3. [DOWNSTREAM DEPENDENCIES (What Each Capability Provides)](#3-downstream-dependencies-what-each-capability-provides)
4. [DEPENDENCY MATRIX](#4-dependency-matrix)
5. [TEXT-BASED DEPENDENCY GRAPH](#5-text-based-dependency-graph)
6. [DATA FLOW MAP](#6-data-flow-map)
7. [DECISION FLOW MAP](#7-decision-flow-map)
8. [CRITICAL DEPENDENCY CHAINS](#8-critical-dependency-chains)
9. [PARALLELIZABLE PATHS](#9-parallelizable-paths)
10. [BOTTLENECK ANALYSIS](#10-bottleneck-analysis)
11. [DOMAIN-LEVEL FLOW CHARTS](#11-domain-level-flow-charts)
12. [FEEDBACK LOOPS](#12-feedback-loops)
13. [KEY INSIGHTS](#13-key-insights)

---

## 1. CAPABILITY MASTER LIST WITH SHORT NAMES

| ID | Short Name | Full Name | Domain | Stage | COS Layer |
|----|-----------|-----------|--------|-------|-----------|
| S01 | StoryArtist | Story Artist/Storyboard Artist | Story | Pre-Production | L2 (CIL) |
| S02 | Screenwriter | Screenwriter/Writer | Story | Pre-Production | L2 (CIL) |
| S03 | NarrativeDesigner | Narrative Designer (Game) | Story | Production | L2 (CIL)/L3 (POL) |
| S04 | VisDev | Visual Development Artist | Story | Pre-Production | L2 (CIL) |
| C01 | CharDesigner | Character Designer | Character | Pre-Production | L2 (CIL) |
| C02 | Sculptor | Sculptor (Physical Maquette) | Character | Pre-Production | L2 (CIL)/L6 (TAL) |
| C03 | CharArtist | Character Artist (Game) | Character | Production | L3 (POL)/L6 (TAL) |
| C04 | DigitalModeler | Digital Modeler / 3D Modeler | Character | Production | L3 (POL) |
| C05 | Rigger | Rigger / Rigging TD | Character | Production | L3 (POL) |
| C06 | TextureArtist | Texture Artist | Character | Production | L3 (POL) |
| C07 | ShadingTD | Shading TD / Surfacing TD | Character | Production | L3 (POL) |
| C08 | GroomingTD | Grooming TD | Character | Production | L3 (POL) |
| C09 | CreatureTD | Creature TD | Character | Production | L3 (POL) |
| V01 | EnvConcept | Environment Concept Artist | Visual | Pre-Production | L2 (CIL) |
| V02 | ProdDesigner | Production Designer | Visual | Pre-Production | L2 (CIL) |
| V03 | EnvArtist | Environment Artist (Game/Modeling) | Visual | Production | L3 (POL) |
| V04 | LayoutArtist | Layout Artist / Previz Artist | Visual | Production | L3 (POL) |
| V05 | LightingTD | Lighting TD / Lighting Artist | Visual | Post-Production | L3 (POL) |
| V06 | MattePainter | Matte Painter | Visual | Post-Production | L3 (POL) |
| V07 | FXArtist | FX Artist / VFX Artist (Simulation) | Visual | Production/Post | L3 (POL) |
| V08 | Lookdev | Look Development Artist (Lookdev) | Visual | Production | L3 (POL) |
| A01 | Animator | Animator / Character Animator | Animation | Production | L3 (POL) |
| A02 | AnimationTD | Animation TD | Animation | Production | L3 (POL)/L6 (TAL) |
| A03 | Matchmove | Matchmove Artist / Camera Tracker | Animation | Post-Production | L3 (POL) |
| A04 | MocapTD | Motion Capture TD | Animation | Production | L3 (POL) |
| A05 | SimTD | Simulation TD | Animation | Production | L3 (POL) |
| D01 | FilmDirector | Film Director | Direction | All | L1 (DEL) |
| D02 | CCO | Chief Creative Officer | Direction | Pre-Production | L1 (DEL) |
| D03 | GameDirector | Game Director | Direction | All | L1 (DEL) |
| D04 | CreativeDir | Creative Director (Game) | Direction | All | L1 (DEL)/L2 (CIL) |
| D05 | Showrunner | Showrunner (TV) | Direction | All | L1 (DEL) |
| D06 | VFXSup | VFX Supervisor | Direction | All | L1 (DEL)/L3 (POL) |
| D07 | CGSup | CG Supervisor | Direction | All | L3 (POL) |
| D08 | CompSup | Compositing Supervisor | Direction | Post-Production | L3 (POL) |
| D09 | ArtDirector | Art Director | Direction | All | L2 (CIL)/L4 (KQL) |
| D10 | TechDirector | Technical Director / Engineering Director (Game) | Direction | All | L3 (POL)/L6 (TAL) |
| D11 | AnimSup | Animation Supervisor | Direction | Production | L2 (CIL)/L3 (POL) |
| Q01 | Braintrust | Braintrust (Pixar) | Quality | All | L7 (FIL) |
| Q02 | DeptLead | Department Lead / Supervisor | Quality | Production | L4 (KQL) |
| Q03 | QAQC | Quality Assurance / QC Specialist | Quality | Post-Production/Launch | L4 (KQL) |
| Q04 | Postmortem | Postmortem Facilitator | Quality | Post-Production | L4 (KQL) |
| P01 | Producer | Producer (Production Management) | Production | All | L5 (APML) |
| P02 | ProdManager | Production Manager | Production | All | L5 (APML) |
| P03 | ProdCoord | Production Coordinator | Production | All | L5 (APML) |
| P04 | PipelineTD | Pipeline TD | Production | All | L6 (TAL) |
| P05 | RenderingTD | Rendering TD | Production | Post-Production | L3 (POL) |
| P06 | SoftwareEng | Software Engineer / Tools Developer | Production | All | L6 (TAL) |
| P07 | TechArtist | Technical Artist (Game) | Production | All | L6 (TAL) |
| P08 | RenderWrangler | Render Wrangler | Production | Post-Production | L5 (APML) |
| P09 | ResearchSci | Research Scientist | Production | Pre-Production | L6 (TAL) |
| P10 | SysITEng | Systems Engineer / IT | Production | All | L6 (TAL) |
| P11 | AssetManager | Asset Manager / Librarian | Production | All | L5 (APML) |

---

## 2. UPSTREAM DEPENDENCIES (What Each Capability Needs)

Each capability entry shows: **Capability Name** → depends on → [list of upstream capabilities it requires input/context from], with the specific data/information passed.

### DOMAIN 1: STORY DOMAIN

| Capability | Upstream Dependencies | Data/Info Received |
|------------|----------------------|-------------------|
| **S01: StoryArtist** | S02 (Screenwriter), D01 (FilmDirector), C01 (CharDesigner), V01 (EnvConcept) | Script/outline, creative direction, character designs, environment concepts |
| **S02: Screenwriter** | D01 (FilmDirector), P01 (Producer) | Creative vision, project feasibility/approval |
| **S03: NarrativeDesigner** | S02 (Screenwriter), D03 (GameDirector)/D04 (CreativeDir), V03 (EnvArtist)/V04 (LayoutArtist) | Script/story bible, game design direction, level layouts/spaces |
| **S04: VisDev** | D01 (FilmDirector), S02 (Screenwriter) | Creative vision, script/narrative context |

### DOMAIN 2: CHARACTER DOMAIN

| Capability | Upstream Dependencies | Data/Info Received |
|------------|----------------------|-------------------|
| **C01: CharDesigner** | D01/D03 (Director/CreativeDir), S04 (VisDev), S02 (Screenwriter) | Creative vision, style guide, character descriptions |
| **C02: Sculptor** | C01 (CharDesigner) | Character design sheets |
| **C03: CharArtist** | C01 (CharDesigner), P07 (TechArtist) | Concept art, shader/performance specs |
| **C04: DigitalModeler** | C01 (CharDesigner)/V01 (EnvConcept), C02 (Sculptor) | Design sheets, scanned maquette data |
| **C05: Rigger** | C04 (DigitalModeler) | Clean 3D geometry with proper topology |
| **C06: TextureArtist** | C04 (DigitalModeler), V08 (Lookdev), C01 (CharDesigner) | UV'd model, material specs, concept reference |
| **C07: ShadingTD** | C06 (TextureArtist), C04 (DigitalModeler), V05 (LightingTD) | Texture maps, geometry, lighting for test renders |
| **C08: GroomingTD** | C04 (DigitalModeler), A05 (SimTD) | Base mesh, physics simulation setup |
| **C09: CreatureTD** | C05 (Rigger), C04 (DigitalModeler) | Skeleton/rig, creature geometry |

### DOMAIN 3: VISUAL DOMAIN

| Capability | Upstream Dependencies | Data/Info Received |
|------------|----------------------|-------------------|
| **V01: EnvConcept** | D01/D03 (Director/CreativeDir), S04 (VisDev) | Creative vision, style/color guide |
| **V02: ProdDesigner** | D01 (FilmDirector), S04 (VisDev) | Creative vision, initial style |
| **V03: EnvArtist** | V01 (EnvConcept), V04 (LayoutArtist) | Concept art reference, level layout |
| **V04: LayoutArtist** | S01 (StoryArtist), C04 (DigitalModeler), D01 (Director), A03 (Matchmove) | Storyboards, 3D assets, shot intent, camera tracking data |
| **V05: LightingTD** | V04 (LayoutArtist), C07 (ShadingTD), V07 (FXArtist) | Camera/scene, materials, simulation validation |
| **V06: MattePainter** | A03 (Matchmove), V01 (EnvConcept) | Camera data, environment reference |
| **V07: FXArtist** | A01 (Animator), V04 (LayoutArtist) | Animated assets, scene context |
| **V08: Lookdev** | C06 (TextureArtist), C07 (ShadingTD), V05 (LightingTD) | Texture maps, shader framework, lighting for review |

### DOMAIN 4: ANIMATION DOMAIN

| Capability | Upstream Dependencies | Data/Info Received |
|------------|----------------------|-------------------|
| **A01: Animator** | C05 (Rigger), V04 (LayoutArtist), D01/D11 (Director/AnimSup) | Functional rig, camera/scene, performance direction |
| **A02: AnimationTD** | A01 (Animator), C05 (Rigger) | Workflow requirements, rigs needing support |
| **A03: Matchmove** | P03 (ProdCoord), On-Set Data | Plates/footage, lens metadata |
| **A04: MocapTD** | On-Set Capture Team | Raw mocap data from stage |
| **A05: SimTD** | A01 (Animator), C04 (DigitalModeler) | Animated base assets, sim-ready geometry |

### DOMAIN 5: DIRECTION DOMAIN

| Capability | Upstream Dependencies | Data/Info Received |
|------------|----------------------|-------------------|
| **D01: FilmDirector** | S02 (Screenwriter), P01 (Producer), Q01 (Braintrust) | Script, budget/schedule, creative feedback |
| **D02: CCO** | D01 (FilmDirector), P01 (Producer) | Project vision, feasibility |
| **D03: GameDirector** | D10 (TechDirector), P01 (Producer) | Feasibility reports, schedule |
| **D04: CreativeDir** | D03 (GameDirector), S02 (Screenwriter), D09 (ArtDirector) | Shared vision, narrative, visuals |
| **D05: Showrunner** | S02 (Screenwriter), D01 (Episodic Directors), P01 (Producer) | Scripts, execution feedback, budget |
| **D06: VFXSup** | D01 (FilmDirector), P01 (Producer), D07 (CGSup) | Overall vision, budget/schedule, technical execution |
| **D07: CGSup** | D06 (VFXSup), P04 (PipelineTD) | Creative direction, infrastructure |
| **D08: CompSup** | D06 (VFXSup), V05 (LightingTD) | Direction, AOVs/renders |
| **D09: ArtDirector** | D01/D03/D04 (Director/CreativeDir) | Creative vision |
| **D10: TechDirector** | D03 (GameDirector), P01 (Producer) | Design vision, schedule |
| **D11: AnimSup** | D01 (FilmDirector), C05 (Rigger) | Performance vision, functional rigs |

### DOMAIN 6: QUALITY DOMAIN

| Capability | Upstream Dependencies | Data/Info Received |
|------------|----------------------|-------------------|
| **Q01: Braintrust** | D01 (FilmDirector), P01 (Producer) | Work samples/rough cuts, session facilitation |
| **Q02: DeptLead** | D01/D06/D09 (Director/Sup/ArtDir), Artists (execution) | Quality vision, work-in-progress |
| **Q03: QAQC** | Dev teams, P01 (Producer) | Builds/renders, schedule for fixes |
| **Q04: Postmortem** | All departments, P01 (Producer) | Participation, project data |

### DOMAIN 7: PRODUCTION DOMAIN

| Capability | Upstream Dependencies | Data/Info Received |
|------------|----------------------|-------------------|
| **P01: Producer** | D01 (FilmDirector) | Creative vision |
| **P02: ProdManager** | P01 (Producer), Q02 (DeptLead) | Budget/schedule, task requirements |
| **P03: ProdCoord** | P02 (ProdManager), Q02 (DeptLead) | Task priorities, submissions |
| **P04: PipelineTD** | D07 (CGSup), All Departments | Technical direction, workflow requirements |
| **P05: RenderingTD** | V05 (LightingTD), C07 (ShadingTD), P04 (PipelineTD) | Scene setup, materials, farm integration |
| **P06: SoftwareEng** | Studio leadership/D07, P04 (PipelineTD) | Technology roadmap, integration requirements |
| **P07: TechArtist** | D10 (TechDirector), D09 (ArtDirector) | Engine constraints, visual direction |
| **P08: RenderWrangler** | P05 (RenderingTD), P10 (SysITEng) | Scene setup, farm hardware |
| **P09: ResearchSci** | Studio CTO, P01 (Producer) | Research direction, real production problems |
| **P10: SysITEng** | Studio leadership | Hardware budget |
| **P11: AssetManager** | P04 (PipelineTD), All Departments | Asset management system, published assets |

---

## 3. DOWNSTREAM DEPENDENCIES (What Each Capability Provides)

| Capability | Downstream Dependents | Data/Info Provided |
|------------|----------------------|-------------------|
| **S01: StoryArtist** | V04 (LayoutArtist), A01 (Animator), P03 (ProdCoord) | Storyboard panels, animatics, shot breakdowns |
| **S02: Screenwriter** | S01 (StoryArtist), S03 (NarrativeDesigner), D01 (FilmDirector) | Script, story spine, character bibles |
| **S03: NarrativeDesigner** | A01 (Animator), V07 (FXArtist), Q03 (QAQC) | Dialogue trees, quest scripts, interactive story |
| **S04: VisDev** | C01 (CharDesigner), V01 (EnvConcept), V02 (ProdDesigner) | Mood paintings, color scripts, style guides |
| **C01: CharDesigner** | C02 (Sculptor), C03 (CharArtist), C04 (DigitalModeler), C06 (TextureArtist) | Turnarounds, expression sheets, orthographic views |
| **C02: Sculptor** | C04 (DigitalModeler) | Scanned 3D data, physical maquettes |
| **C03: CharArtist** | C05 (Rigger), A01 (Animator) | High/low-poly models, PBR textures, engine-ready assets |
| **C04: DigitalModeler** | C05 (Rigger), C06 (TextureArtist), C07 (ShadingTD), C08 (GroomingTD), C09 (CreatureTD), V04 (LayoutArtist), A05 (SimTD) | 3D wireframe models, organized geometry |
| **C05: Rigger** | A01 (Animator), C09 (CreatureTD), A02 (AnimationTD), D11 (AnimSup) | Animation-ready rig, facial rig, documentation |
| **C06: TextureArtist** | C07 (ShadingTD), V08 (Lookdev) | Texture maps (diffuse, normal, roughness, etc.) |
| **C07: ShadingTD** | V05 (LightingTD), V08 (Lookdev), P05 (RenderingTD) | Shader networks, lookdev renders, material definitions |
| **C08: GroomingTD** | V08 (Lookdev), V05 (LightingTD) | Groom guides, hair/fur setups |
| **C09: CreatureTD** | A01 (Animator), A05 (SimTD) | Muscle/flesh/skin sim, secondary motion rigs |
| **V01: EnvConcept** | V03 (EnvArtist), V06 (MattePainter), V04 (LayoutArtist), V05 (LightingTD) | Mood paintings, architectural breakdowns, area overviews |
| **V02: ProdDesigner** | V03 (EnvArtist), V06 (MattePainter), V05 (LightingTD) | Production bible, set designs, color palettes |
| **V03: EnvArtist** | V05 (LightingTD), V07 (FXArtist), V04 (LayoutArtist) | 3D environment meshes, engine-ready levels |
| **V04: LayoutArtist** | A01 (Animator), V05 (LightingTD), V07 (FXArtist) | 3D layout scenes, camera animation, previz |
| **V05: LightingTD** | P05 (RenderingTD), V08 (Lookdev), D08 (CompSup), A05 (SimTD) | Lit shots, AOVs, lighting templates |
| **V06: MattePainter** | D08 (CompSup) | Matte paintings, projected environment setups |
| **V07: FXArtist** | V05 (LightingTD), D08 (CompSup) | Simulation caches, FX render layers |
| **V08: Lookdev** | V05 (LightingTD), D08 (CompSup) | Shader definitions, material library entries |
| **A01: Animator** | V07 (FXArtist), V05 (LightingTD), D08 (CompSup), A05 (SimTD), A02 (AnimationTD) | Animated shots, animation curves, animation clips |
| **A02: AnimationTD** | A01 (Animator), P04 (PipelineTD) | Animation tools, scripts, picker UIs |
| **A03: Matchmove** | V04 (LayoutArtist), A01 (Animator), D08 (CompSup) | Solved camera, tracking data, lens distortion |
| **A04: MocapTD** | A01 (Animator), C05 (Rigger) | Cleaned mocap data, retargeted animation |
| **A05: SimTD** | V05 (LightingTD), D08 (CompSup), C08 (GroomingTD) | Simulation caches, optimized parameters |
| **D01: FilmDirector** | S01, S02, S04, C01, V01, V02, V04, A01, D06, D09, D11, Q01, P01, ALL | Vision, approvals, feedback to ALL departments |
| **D02: CCO** | D01 (FilmDirector), Studio Leadership | Greenlight decisions, studio strategy |
| **D03: GameDirector** | D04 (CreativeDir), D10 (TechDirector), S03, P07, ALL | Vision, feature decisions, milestone targets |
| **D04: CreativeDir** | D09 (ArtDirector), S03 (NarrativeDesigner), A01 (Animator), V05 (LightingTD) | Creative vision, tonal direction, art style guidelines |
| **D05: Showrunner** | S02 (Screenwriter), D01 (Episodic Directors), P03 (ProdCoord) | Series vision, episode outlines, creative notes |
| **D06: VFXSup** | D07 (CGSup), D08 (CompSup), V05, V07, All VFX depts | Creative direction, shot approvals, technical specs |
| **D07: CGSup** | C04, C05, C06, C07, V03, V05, V08, P04, P05, ALL 3D | Pipeline standards, tool priorities, quality bar |
| **D08: CompSup** | Q03 (QAQC), D06 (VFXSup) | Final shot composites, quality reviews |
| **D09: ArtDirector** | C01, V01, V03, V07, All art disciplines | Art guidelines, style enforcement, quality bar |
| **D10: TechDirector** | P07 (TechArtist), Engineering teams | Technical architecture, performance budgets |
| **D11: AnimSup** | A01 (Animator), V07 (FXArtist) | Animation quality reviews, direction, approved shots |
| **Q01: Braintrust** | D01 (FilmDirector) | Creative feedback, problem identification |
| **Q02: DeptLead** | A01, C03, C04, V03, V05, V07, All discipline artists | Approved rounds, quality feedback |
| **Q03: QAQC** | Dev teams (bug lists) | QA reports, certification status, bug lists |
| **Q04: Postmortem** | Studio leadership, future project teams | Postmortem reports, action items, institutional knowledge |
| **P01: Producer** | P02 (ProdManager), P03 (ProdCoord), All departments | Budget, schedule, resource allocation |
| **P02: ProdManager** | P03 (ProdCoord), Q02 (DeptLead) | Task assignments, status reports, blocker escalation |
| **P03: ProdCoord** | All departments | Dailies sessions, version tracking, review notes |
| **P04: PipelineTD** | All departments | Pipeline tools, automation, standards, documentation |
| **P05: RenderingTD** | P08 (RenderWrangler), D08 (CompSup) | Final rendered frames, optimized settings |
| **P06: SoftwareEng** | All departments | Core software, rendering technology, simulation tools |
| **P07: TechArtist** | C03, V03, All art disciplines | Shaders, art pipeline tools, performance optimization |
| **P08: RenderWrangler** | All departments | Completed renders, farm utilization reports |
| **P09: ResearchSci** | P06 (SoftwareEng), P04 (PipelineTD) | Publications, algorithms, prototypes |
| **P10: SysITEng** | All departments | Infrastructure, storage, farm operations |
| **P11: AssetManager** | All departments | Organized asset library, version tracking, archival |

---

## 4. DEPENDENCY MATRIX

### Dependency Matrix Key

**Rows** = Capabilities (what depends on what). **Columns** = Capabilities (what is depended upon).
- `●` = Direct dependency (row capability directly depends on column capability)
- `○` = Indirect/transitive dependency (row depends on column through intermediate nodes)
- `D` = Decision authority (row receives authoritative decisions from column)
- `F` = Feedback (row receives non-binding feedback from column)
- `I` = Infrastructure dependency (row relies on column for tools/infrastructure)
- `P` = Production dependency (row relies on column for schedule/budget/coordination)
- `→` = Row provides output TO column (for data flow)

### SHORT ABSTRACTED MATRIX (Reduced to Key Relationships)

For brevity, the full 47×47 matrix is represented as **domain-level** and **key capability-level** matrices.

#### 4a. Domain-Level Dependency Matrix

| Domain → Depends On ↓ | Story | Character | Visual | Animation | Direction | Quality | Production |
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **Story** | — | — | — | — | D | F,P | P |
| **Character** | D | — | I | I | D | F,P | P |
| **Visual** | D | I | — | I | D | F,P | P |
| **Animation** | — | D | D | — | D | F,P | P |
| **Direction** | I | — | — | — | — | F | I |
| **Quality** | — | — | — | — | D | — | I |
| **Production** | — | — | — | — | D | — | — |

Legend: `D`=Direction/Decisions, `I`=Input/Data, `F`=Feedback, `P`=Production constraints

#### 4b. Full Capability-Level Dependency Matrix (47×47)

Reading: Row capability depends on Column capability. Empty cells = no direct dependency.

```
CapID    S01 S02 S03 S04 C01 C02 C03 C04 C05 C06 C07 C08 C09 V01 V02 V03 V04 V05 V06 V07 V08 A01 A02 A03 A04 A05 D01 D02 D03 D04 D05 D06 D07 D08 D09 D10 D11 Q01 Q02 Q03 Q04 P01 P02 P03 P04 P05 P06 P07 P08 P09 P10 P11
S01       -   ●   -   -   ○   -   -   -   -   -   -   -   -   ○   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
S02       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -
S03       -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   ○   ○   -   -   -   -   -   -   -   -   -   -   -   ●   ○   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
S04       -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
C01       -   ●   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   ○   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
C02       -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
C03       -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -
C04       -   -   -   -   ●   ●   -   -   -   -   -   -   -   ○   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
C05       -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
C06       -   -   -   -   ●   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
C07       -   -   -   -   -   -   -   ●   -   ●   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
C08       -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
C09       -   -   -   -   -   -   -   ●   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
V01       -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
V02       -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
V03       -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
V04       ●   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
V05       -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   ●   -   -   ●   ○   -   -   -   -   ○   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
V06       -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
V07       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
V08       -   -   -   -   -   -   -   -   -   ●   ●   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
A01       -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
A02       -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
A03       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -
A04       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
A05       -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
D01       -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ○   -   -   -   ●   -   -   -   -   -   -   -   -   -   -
D02       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -
D03       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -
D04       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
D05       -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -
D06       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -
D07       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -
D08       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
D09       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
D10       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -
D11       -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
Q01       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -
Q02       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   ●   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
Q03       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -
Q04       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -
P01       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
P02       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   ●   -   -   -   -   -   -   -   -   -   -
P03       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   ●   -   -   -   -   -   -   -   -   -
P04       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
P05       -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -
P06       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -
P07       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   ●   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
P08       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   ●   -   -
P09       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
P10       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
P11       -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   ●   -   -   -   -   -   -   -
```

---

## 5. TEXT-BASED DEPENDENCY GRAPH

### 5a. Primary Production Chain (Film/VFX Pipeline)

```
                                              FEEDBACK LOOPS (L7 FIL)
              ┌───────────────────────────────────┼───────────────────────────────────────┐
              ▼                                   ▼                                       ▼
    ┌──────────────┐    ┌──────────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌─────────┐    ┌─────────┐    ┌───────────┐
    │  S02        │    │  S01        │    │  V04     │    │  A01    │    │  V07    │    │  V05   │    │  P05    │    │  D08      │
    │  Screenwriter│──▶│  StoryArtist│──▶│  Layout  │──▶│  Animator│──▶│  FX     │──▶│  Light  │──▶│  Render │──▶│  CompSup  │
    │  (Script)   │    │  (Boards)   │    │  Artist  │    │  (Perf)  │    │  Artist │    │  TD     │    │  TD     │    │  (Final)  │
    └──────┬───────┘    └──────────────┘    └──────┬────┘    └────┬─────┘    └──────────┘    └────┬────┘    └─────────┘    └───────────┘
           │                                        │              │                               │
           │                                        │              │                               │
           │                                        │         ┌────▼────┐                    ┌──────▼───────┐
           │                                        │         │  A05   │                    │  V08         │
           │                                        │         │  SimTD │                    │  Lookdev     │
           │                                        │         └─────────┘                    └──────────────┘
           │                                        │                                           ▲
           │                                        │                                           │
    ┌──────▼───────┐    ┌──────────────┐    ┌───────┴─────────────┐    ┌──────────┐           │
    │  S04         │    │  C01        │    │  C04                │    │  C05    │           │
    │  VisDev      │──▶│  CharDesigner│──▶│  Digital Modeler     │──▶│  Rigger  │──▶ A01    │
    │  (Style)     │    │  (Designs)  │    │  (Geometry)          │    │  (Rig)   │           │
    └──────────────┘    └──────┬───────┘    └────────┬───────────┘    └──────────┘           │
                               │                      │                                      │
                               │                ┌─────┴──────┐                              │
                               │                │  C06      │                              │
                               │                │  Texture  │──▶ C07 ──▶ V08 ────────────────┘
                               │                │  Artist   │    (Shading)
                               │                └────────────┘
                               │                      │
                               │                ┌─────▼──────┐
                               └────────────────│  C02      │──▶ C04
                                                │  Sculptor │
                                                └───────────┘
```

### 5b. Game Production Pipeline

```
    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
    │  D03         │    │  D04         │    │  S03         │    │  A01         │
    │  GameDirector│──▶│  CreativeDir │──▶│  Narrative   │──▶│  Animator    │
    │  (Vision)    │    │  (Tone/Style)│    │  Designer    │    │  (Gameplay)  │
    └──────┬───────┘    └──────────────┘    └──────────────┘    └──────────────┘
           │                                                            ▲
           │    ┌──────────────┐                                        │
           │    │  D10         │                                        │
           └───▶│  TechDirector│──▶ P07 ──▶ C03 ──▶ C05 ────────────────┘
                │  (Feasibility)│    (TechArt) (CharArtist) (Rigger)
                └──────────────┘
```

### 5c. Direction Domain Oversight (Star Topology)

```
                                   ┌───────────┐
                                   │  D01/D03  │
                                   │  Director  │
                                   └─────┬─────┘
                                         │
              ┌──────────────────────────┼──────────────────────────┐
              │              │           │           │              │
              ▼              ▼           ▼           ▼              ▼
        ┌──────────┐  ┌──────────┐  ┌────────┐  ┌────────┐  ┌──────────┐
        │  D11     │  │  D06     │  │  D09   │  │  D02   │  │  D07     │
        │AnimSup   │  │VFXSup    │  │ArtDir  │  │ CCO    │  │CGSup     │
        └────┬─────┘  └────┬─────┘  └───┬────┘  └───┬────┘  └────┬─────┘
             │              │            │           │            │
             ▼              ▼            ▼           ▼            ▼
          Animation      VFX Depts    Art Depts   All Projs   3D Depts
```

### 5d. Quality Domain Feedback Topology

```
                              ┌─────────────┐
                              │   Q01       │
                              │  Braintrust  │──(non-binding feedback)──▶ D01
                              └─────────────┘
                                     ▲
                                     │ (presents work)
                                     │
    ┌─────────────────────────────────┼───────────────────────────────────────┐
    │                    │                       │                            │
    ▼                    ▼                       ▼                            ▼
┌────────┐        ┌───────────┐          ┌──────────┐                ┌────────────┐
│  Q02   │        │   Q03     │          │   Q04    │                │  P01       │
│DeptLead│        │  QA/QC    │          │Postmortem│                │  Producer  │
└────┬───┘        └───────────┘          └──────────┘                └─────┬──────┘
     │                    │                       │                        │
     ▼                    ▼                       ▼                        ▼
  Artists            Dev Teams              Leadership               All Depts
```

---

## 6. DATA FLOW MAP

### 6a. Primary Data Flow — Film/VFX Pipeline

```
[S02 Screenwriter]
  │ Script, Story Spine, Character Bibles
  ├──▶ [S01 StoryArtist]
  │     │ Storyboards, Animatics, Shot Breakdowns
  │     └──▶ [V04 LayoutArtist]
  │           │ 3D Layout, Camera Animation, Previz
  │           ├──▶ [A01 Animator]
  │           │     │ Animated Shots, Curves, Playblasts
  │           │     ├──▶ [V07 FXArtist] ──▶ Simulation Caches, FX Layers
  │           │     ├──▶ [A05 SimTD]    ──▶ Sim Caches, Optimized Params
  │           │     └──▶ [V05 LightingTD]
  │           │           │ Lit Shots, AOVs (diffuse, spec, SSS, z-depth, motion)
  │           │           ├──▶ [P05 RenderingTD] ──▶ Final Rendered Frames
  │           │           │                         └──▶ [D08 CompSup] ──▶ Final Composites
  │           │           └──▶ [V08 Lookdev] ──▶ Material Definitions, Shader Library
  │           │
  │           └──▶ [V05 LightingTD] (scene context)
  │
  ├──▶ [S03 NarrativeDesigner] (game branch)
  │     │ Dialogue Trees, Quest Scripts, Interactive Story
  │     └──▶ [A01 Animator] (cinematic anim)
  │
  └──▶ [D01 FilmDirector] (for approval)

[S04 VisDev]
  │ Mood Paintings, Color Scripts, Style Guides
  ├──▶ [C01 CharDesigner]
  │     │ Turnarounds, Expression Sheets, Ortho Views
  │     ├──▶ [C02 Sculptor] ──▶ Scanned Maquette ──▶ [C04 DigitalModeler]
  │     └──▶ [C04 DigitalModeler]
  │           │ 3D Wireframe (hi/med/lo)
  │           ├──▶ [C05 Rigger] ──▶ Rig, Controls ──▶ [A01 Animator]
  │           ├──▶ [C06 TextureArtist]
  │           │     │ Texture Maps (diffuse, normal, roughness, AO, displacement)
  │           │     └──▶ [C07 ShadingTD]
  │           │           │ Shader Networks, Lookdev Renders
  │           │           └──▶ [V08 Lookdev] ──▶ [V05 LightingTD]
  │           ├──▶ [C08 GroomingTD] ──▶ Grooms ──▶ [V08 Lookdev]/[V05 LightingTD]
  │           ├──▶ [C09 CreatureTD] ──▶ Muscle/Flesh Sim ──▶ [A01 Animator]/[A05 SimTD]
  │           └──▶ [V04 LayoutArtist] (assets for scene building)
  │
  └──▶ [V01 EnvConcept]
        │ Mood Paintings, Area Overviews, Arch Breakdowns
        ├──▶ [V03 EnvArtist] ──▶ 3D Environment Meshes ──▶ [V05 LightingTD]
        ├──▶ [V06 MattePainter] ──▶ Matte Paintings ──▶ [D08 CompSup]
        └──▶ [V04 LayoutArtist] (environment context)
```

### 6b. Primary Data Flow — Game Pipeline

```
[D03 GameDirector]
  │ Vision, Feature Decisions, Scope, Milestones
  ├──▶ [D04 CreativeDir]
  │     │ Creative Vision, Tonal Direction, Art Style
  │     ├──▶ [D09 ArtDirector] ──▶ Art Guidelines ──▶ All Art Disciplines
  │     └──▶ [S03 NarrativeDesigner] ──▶ Dialogue, Quests, Story
  │
  └──▶ [D10 TechDirector]
        │ Architecture, Performance Budgets, Feasibility
        └──▶ [P07 TechArtist]
              │ Shaders, Art Pipeline Tools, Performance Opt
              ├──▶ [C03 CharArtist] ──▶ Engine-Ready Assets ──▶ [C05 Rigger]
              └──▶ [V03 EnvArtist] ──▶ Engine-Ready Levels ──▶ [V05 LightingTD]
```

### 6c. Infrastructure Data Flow (Enables Everything)

```
[P04 PipelineTD]
  │ Pipeline Tools, Automation, Naming Standards, DCC Integration
  └──▶ ALL DEPARTMENTS (Maya/Houdini/Nuke plugins, publish/validate scripts)

[P06 SoftwareEng]
  │ Proprietary Software, Rendering Technology, Simulation Frameworks
  └──▶ P04 (tools) + ALL DEPARTMENTS (core tools)

[P10 SysITEng]
  │ Infrastructure, Storage, Farm Hardware, Network
  └──▶ ALL DEPARTMENTS (workstations, storage, connectivity)

[P11 AssetManager]
  │ Versioned Asset Library, Metadata, Archived Projects
  └──▶ ALL DEPARTMENTS (asset access and tracking)

[P01 Producer/P02 ProdManager/P03 ProdCoord]
  │ Budget, Schedule, Tasks, Dailies, Version Tracking
  ├──▶ ALL DEPARTMENTS (schedule/budget constraints)
  └──▶ P08 RenderWrangler (priority list)
```

---

## 7. DECISION FLOW MAP

### 7a. Decision Authority Hierarchy

```
Level 0: Studio Strategy
  [D02 CCO] ──▶ Greenlight decisions, studio creative strategy
      │
Level 1: Project Creative Authority (FINAL SAY)
  [D01 FilmDirector] / [D03 GameDirector] / [D05 Showrunner]
      │   All creative decisions: story, design, performance, tone, pacing, final cut
      │   Can override ANY department
      │
      ├──▶ [D06 VFXSup] ──▶ VFX technique choice, shot approval, client delivery
      ├──▶ [D09 ArtDirector] ──▶ Art style, consistency, quality bar
      └──▶ [D11 AnimSup] ──▶ Animation quality, performance consistency
      │
Level 2: Technical Authority
  [D07 CGSup] ──▶ Pipeline, tool priorities, 3D department quality
  [D10 TechDirector] ──▶ Engine choice, architecture, tech feasibility
      │
Level 3: Department Execution Authority
  [Q02 DeptLead] ──▶ Internal shot approval, task assignment, technique choice
  [D08 CompSup] ──▶ Comp readiness, comp workflow
  [P01 Producer] ──▶ Budget allocation, resource distribution, milestone gates
  [P02 ProdManager] ──▶ Task prioritization, staffing, workflow optimization
      │
Level 4: Creative Proposal (Executes, Does Not Decide)
  [All artists and TDs] ──▶ Propose work for review and approval at Levels 1-3
```

### 7b. Decision Flow by Pipeline Stage

```
PRE-PRODUCTION DECISIONS:
  D02 (CCO) ──▶ Which projects get made
  D01/D03/D05 ──▶ Creative vision, tone, style
  D09 (ArtDir) ──▶ Art direction guidelines
  D07 (CGSup) ──▶ Pipeline technical standards
  D10 (TechDir) ──▶ Engine/architecture decisions
  P01 (Producer) ──▶ Budget allocation, schedule

PRODUCTION DECISIONS:
  Q02 (DeptLead) ──▶ Shot readiness for review
  D11 (AnimSup) ──▶ Animation approval
  D06 (VFXSup) ──▶ VFX shot approval
  P02 (ProdManager) ──▶ Task priority, staffing adjustments
  C05 (Rigger) ──▶ Rig deformation approach
  A01 (Animator) ──▶ Performance choices within approved direction

POST-PRODUCTION DECISIONS:
  D08 (CompSup) ──▶ Composite readiness
  V05 (LightingTD) ──▶ Lighting mood, render sampling
  P05 (RenderingTD) ──▶ Render farm priority, optimization
  Q03 (QAQC) ──▶ QC pass/fail, severity classification

REVIEW DECISIONS (No Authority - Influence Only):
  Q01 (Braintrust) ──▶ Recommendations only
  Q04 (Postmortem) ──▶ Recommendations for future projects
```

### 7c. Decision Cascades (Single Decision → Multiple Downstream Impacts)

| Decision Maker | Decision | Directly Affects | Cascading Effects |
|---------------|----------|-----------------|-------------------|
| D01/D03 (Director) | "Change story from X to Y" | S02, S01, S04 | C01 (redesign characters), V01 (redesign env), A01 (re-animate), V07 (re-simulate), V05 (re-light) |
| D07 (CGSup) | "Change polygon budget" | C04 (LOD strategy), C05 (rig complexity), C06 (tex resolution), V03 (env detail) | A01 (deformation quality), V05 (render time), P05 (farm load) |
| P01 (Producer) | "Cut 10% of department budget" | Q02 (team size), P02 (schedule), All depts | Fewer shots, lower quality, longer wait times, cascading delays |
| D06 (VFXSup) | "Change VFX approach from practical to CG" | V07 (sim approach), V04 (layout), A03 (matchmove), V05 (lighting integration) | Entire VFX pipeline path changes |
| C05 (Rigger) | "Rig topology decision" | A01 (range of motion), C09 (muscle sim), V05 (deformation under light) | Downstream rework if rig doesn't support animation needs |

---

## 8. CRITICAL DEPENDENCY CHAINS

### 8a. Longest Production Chain (Film Pipeline)

**Chain 1 (Primary Narrative Chain) — 9 links**
```
S02(Screenwriter) → S01(StoryArtist) → V04(LayoutArtist) → A01(Animator) → V07(FXArtist) → V05(LightingTD) → P05(RenderingTD) → D08(CompSup) → D01/D06(Approval)
```
**Impact:** Breaking any link breaks the entire production flow. If storyboards are wrong, every downstream department reworks. This is the single longest data transformation chain.

### 8b. Character Asset Chain — 7 links
```
S04(VisDev) → C01(CharDesigner) → C04(DigitalModeler) → C05(Rigger) → A01(Animator) → V05(LightingTD) → P05(RenderingTD)
```
**Impact:** If modeling topology is bad, rigging breaks, which breaks animation, which breaks lighting. Character pipeline is the most tightly coupled chain.

### 8c. Environment Chain — 6 links
```
S04(VisDev) → V01(EnvConcept) → V03(EnvArtist) → V04(LayoutArtist) → V05(LightingTD) → P05(RenderingTD)
```
**Impact:** Environment designs constrain camera placement, which constrains what can be lit.

### 8d. Material/Surface Chain — 6 links
```
C04(DigitalModeler) → C06(TextureArtist) → C07(ShadingTD) → V08(Lookdev) → V05(LightingTD) → P05(RenderingTD)
```
**Impact:** Without textures, shading has nothing to work with; without shaders, lookdev can't finalize the look; without lookdev, lighting uses placeholder materials.

### 8e. VFX Integration Chain — 5 links
```
A01(Animator) → V07(FXArtist) → V05(LightingTD) → P05(RenderingTD) → D08(CompSup)
```
**Impact:** FX sims depend on animated character motion; if animation changes, FX must re-sim.

### 8f. Game Pipeline Chain — 7 links
```
D03(GameDirector) → D10(TechDirector) → P07(TechArtist) → C03(CharArtist) → C05(Rigger) → A01(Animator) → Q03(QAQC)
```
**Impact:** Tech feasibility gate blocks entire art pipeline. If engine can't support feature, everything downstream is wasted.

---

## 9. PARALLELIZABLE PATHS

### 9a. Independent Parallel Pipelines

These capability paths have NO cross-dependencies and can run simultaneously:

```
PARALLEL GROUP 1 (Character + Visual):
  Path A: C01→C02→C04→C05 (Character modeling & rigging chain)
  Path B: V01→V03 (Environment modeling chain)
  Path C: S01→V04 (Layout/staging chain - needs assets from A & B)

  CONSTRAINT: Paths A, B, and C merge at V04 (Layout needs both characters AND environments).
  BEFORE merge: Fully parallel.
  AFTER merge: Sequential.

PARALLEL GROUP 2 (Tail-end Pipeline):
  Path D: V07 (FX Simulation)
  Path E: V08 (Lookdev) — fed by C06→C07
  Path F: V06 (Matte Painting) — fed by A03

  CONSTRAINT: All three converge at V05 (LightingTD) and then D08 (CompSup).
```

### 9b. Full Parallelization Timeline

```
TIME ──────────────────────────────────────────────────────────────▶

[S02 Screenwriter] ──────────────────────────────────────────────────┐
[S04 VisDev] ────────────────────────────────────────────────────────┤
                                                                      │
[S01 StoryArtist] ───────────────────────────────────────────────────┤
[C01 CharDesigner] ──────────────────────────────────────────────────┤
[V01 EnvConcept] ────────────────────────────────────────────────────┤
                                                                      │
[C02 Sculptor] ──┐                                                    │
[C04 DigitalModeler] ◄───────────────────────────────────────────────┤
[C06 TextureArtist] ──┐                                              │
[C07 ShadingTD] ◄─────┘                                              │
[C05 Rigger] ────────────────────────────────────────────────────────┤
[V03 EnvArtist] ──┐                                                  │
[V04 LayoutArtist] ◄─────────────────────────────────────────────────┤
[A03 Matchmove] ──┘                                                  │
                                                                      │
[A01 Animator] ─────────────────────────────────────────────────────▶│
[A05 SimTD] ────┐                                                    │
[V07 FXArtist] ◄┴──┐                                                 │
[C08 GroomingTD] ──┤                                                 │
[C09 CreatureTD] ──┤                                                 │
[V08 Lookdev] ◄────┘                                                 │
                                                                      │
[V05 LightingTD] ◄──────────────────────────────────────────────────┘
[V06 MattePainter] ──┐
[P05 RenderingTD] ◄──┤
[D08 CompSup] ◄──────┘

LEGEND:
  ─── = Can run in parallel
  ◄── = Merge point (depends on multiple parallel paths completing)
  ┌┴┐ = Fork point (splits into parallel)
```

### 9c. Maximum Parallelism Estimate

| Phase | Sequential Steps Required | Parallel Workstreams | Minimum Time |
|-------|-------------------------|---------------------|--------------|
| Pre-Production | S02 → S04 → (C01, V01, S01) | 3 paths (Char, Env, Story) | 3 sequential steps |
| Production | (C04→C05→A01) parallel with (V01→V03→V04) | 2+ paths through assets | 4 sequential steps |
| Post-Production | (A01→V07, A01→V05, V08→V05) → P05 → D08 | 3 paths merge at Lighting | 3 sequential steps |

---

## 10. BOTTLENECK ANALYSIS

### 10a. Bottleneck Ranking (By Number of Dependencies)

| Rank | Capability | Depends On (Upstream) | Provides To (Downstream) | Total Connections | Reason |
|------|-----------|----------------------|------------------------|-------------------|--------|
| **1** | **C04: DigitalModeler** | C01, C02, V01 | C05, C06, C07, C08, C09, V04, A05 | **10 connections** | Central gateway between design and all downstream 3D work |
| **2** | **V04: LayoutArtist** | S01, C04, D01, A03 | A01, V05, V07 | **7 connections** | Single point where story, assets, camera, and direction converge |
| **3** | **V05: LightingTD** | V04, C07, V07, V08, A05 | P05, V08, D08 | **7 connections** | Sits at the convergence of ALL downstream pipelines |
| **4** | **A01: Animator** | C05, V04, D01/D11 | V07, V05, D08, A05, A02 | **7 connections** | Core creative execution — many depend on animation output |
| **5** | **D01: FilmDirector** | S02, P01, Q01 | ALL DOMAINS | **47 connections** (uniquely universal) | Every capability receives direction from here |
| **6** | **P01: Producer** | D01 | All departments | **47 connections** (uniquely universal) | Every capability receives budget/schedule constraints |
| **7** | **C05: Rigger** | C04 | A01, C09, A02, D11 | **6 connections** | Without a rig, nothing animates |
| **8** | **C01: CharDesigner** | D01, S04, S02 | C02, C03, C04, C06 | **6 connections** | Character designs feed multiple downstream paths |
| **9** | **P04: PipelineTD** | D07, All Depts | All Depts | **~47 connections** | Infrastructure bottleneck — all depts need tools |
| **10** | **P06: SoftwareEng** | Studio leadership, P04 | All Depts | **~47 connections** | Core software enables everything |

### 10b. Single Points of Failure (Non-Redundant Bottlenecks)

These capabilities have NO substitutes — if they fail, the pipeline stops:

1. **C04 (DigitalModeler)** — No alternative path to produce clean 3D geometry. If modeler is blocked, rigging, texturing, shading, layout, and simulation all stop.

2. **C05 (Rigger)** — No alternative way to produce animation-ready controls. Without a rig, character animation is impossible.

3. **V04 (LayoutArtist)** — No alternative path to set up camera, blocking, and scene staging. Without layout, animators don't know where to place characters.

4. **V05 (LightingTD)** — The convergence point of all downstream work. If lighting is blocked, rendering and compositing stop entirely.

5. **P04 (PipelineTD)** — If pipeline tools are broken, NO department can publish or load assets. This is the technical single point of failure.

6. **P05 (RenderingTD)** — The ONLY path to final frames. If rendering is blocked, compositing has nothing to work with.

### 10c. Decision Authority Bottlenecks

These are the decision-makers whose approval is REQUIRED for work to advance — if they're unavailable, the pipeline stalls:

1. **D01/D03 (Director)** — Final say on ALL creative decisions. No shot can be finalized without director approval.
2. **D06 (VFXSup)** — Final say on ALL VFX shots. Bottleneck for VFX department throughput.
3. **P01 (Producer)** — Controls resource allocation. If producer doesn't approve budget shifts, departments can't scale up to meet demand.
4. **Q02 (DeptLead)** — First quality gate. If department lead doesn't approve internal rounds, work never reaches director for final approval.

---

## 11. DOMAIN-LEVEL FLOW CHARTS

### 11a. Story Domain Flow

```
┌────────┐     ┌──────────┐
│  D01   │     │   P01    │
│Director│────▶│ Producer │──(budget/schedule)──▶
└───┬────┘     └──────────┘
    │
    ▼
┌──────────┐
│  S02     │  Script ──▶ D01 (for approval)
│Screenwrtr│  Script ──▶ S01 (for boards)
└──────────┘  Script ──▶ S03 (for game narrative)
    │          Script ──▶ S04 (for visual development)
    │
    ├──▶ S01 ──▶ Storyboards ──▶ V04 LayoutArtist
    ├──▶ S03 ──▶ Dialogue Trees ──▶ A01 Animator
    └──▶ S04 ──▶ Style Guides ──▶ C01, V01, V02
```

### 11b. Character Domain Flow

```
┌───────────┐    ┌──────────┐    ┌───────────────┐    ┌────────┐    ┌─────────┐
│  S04/VisDev│──▶│ C01      │──▶│ C02 (Sculptor) │──▶│ C04    │──▶│ C05     │──▶ A01
│  C01 Design  │   │CharDesign│   └───────────────┘   │Digital │   │ Rigger  │
│  (Style +   │   └────┬─────┘                       │Modeler │   └────┬────┘
│   Narrative)│         │                             └───┬─────┘        │
└─────────────┘         │                                 │              │
                        │                                 ├──▶ C06 ──▶ C07 ──▶ V08
                        │                                 │   (Tex)  (Shade)  (Lookdev)
                        │                                 │
                        │                                 ├──▶ C08 (Groom) ──▶ V08/V05
                        │                                 │
                        │                                 └──▶ C09 (Creature) ──▶ A01/A05
                        │
                        └─────────────────▶ C03 (Game Character Artist) ──▶ C05
```

### 11c. Visual Domain Flow

```
┌──────────┐     ┌────────────┐     ┌───────────┐
│  D01/D03  │────▶│  V01       │────▶│  V03      │
│  Director  │     │ EnvConcept │     │EnvArtist  │
└──────────┘     └────────────┘     └─────┬─────┘
                                          │
┌──────────┐     ┌────────────┐           │
│  D01     │────▶│  V02       │           │
│Director  │     │ProdDesigner│           │
└──────────┘     └────────────┘           │
                                          ▼
┌──────────┐     ┌────────────┐     ┌───────────┐     ┌─────────┐     ┌─────────┐
│  S01     │────▶│  V04       │────▶│  A01      │────▶│  V07    │────▶│  V05    │
│StoryBrd  │     │LayoutArtist│     │ Animator  │     │ FXArtist│     │Lighting │
└──────────┘     └─────┬──────┘     └───────────┘     └─────────┘     └────┬────┘
                       │                                                    │
                       └────────────────────────────────────────────────────┘
                                             │
                                       ┌─────▼──────┐
                                       │  V08       │
                                       │ Lookdev    │────▶ V05
                                       └────────────┘
```

### 11d. Animation Domain Flow

```
┌─────────┐     ┌──────────┐     ┌───────────┐
│  C05    │────▶│  A01     │────▶│  A02      │ (tools support)
│  Rigger │     │ Animator │     │AnimTD     │
└─────────┘     └────┬─────┘     └───────────┘
                     │
┌─────────┐          │
│  V04    │──────────┤
│Layout   │          │
└─────────┘          │
                     │
┌─────────┐          │
│  D01    │──────────┤
│Director │          │
└─────────┘          │
                     │
                     ├──▶ V07 (FXArtist) — animated assets for FX interaction
                     ├──▶ A05 (SimTD) — animated base for simulation
                     └──▶ V05 (LightingTD) — animated characters to light
```

### 11e. Production Domain Flow (Enabling Infrastructure)

```
[D02 CCO / D01 Director / Studio Leadership]
  │
  ▼
[P01 Producer]
  │ Budget + Schedule
  ├──▶ [P02 ProdManager]
  │     │ Task Priorities + Status
  │     └──▶ [P03 ProdCoord]
  │           │ Dailies + Version Tracking + Notes
  │           └──▶ ALL DEPARTMENTS
  │
  ▼
[P04 PipelineTD]
  │ Tools, Automation, Standards
  └──▶ ALL DEPARTMENTS (infrastructure)
  │
  ▼
[P06 SoftwareEng] ◄── [P09 ResearchSci] (new techniques)
  │ Core Software
  └──▶ P04 + ALL DEPARTMENTS
  │
  ▼
[P10 SysITEng]
  │ Infrastructure, Storage, Farm
  └──▶ ALL DEPARTMENTS
  │
  ▼
[P11 AssetManager]
  │ Asset Library, Metadata, Archive
  │ Inputs: Published assets from ALL departments
  │ Outputs: Asset access to ALL departments
  │
  ▼
[P05 RenderingTD] ◄── [P08 RenderWrangler]
  │ Final Renders        │ Farm Management
  └──▶ D08 CompSup      └──▶ P05 (jobs)
```

---

## 12. FEEDBACK LOOPS

### 12a. Primary Feedback Loops

```
LOOP 1: Director ↔ Braintrust (High-Level Creative)
  D01 (Director) ──presents work──▶ Q01 (Braintrust)
  Q01 ──recommendations──▶ D01 (no authority, non-binding)
  D01 ──implements or rejects──▶ Iteration

LOOP 2: Director ↔ Animator (Performance Iteration)
  A01 (Animator) ──playblast──▶ D01/D11 (Director/AnimSup)
  D01 ──notes──▶ A01
  A01 ──revision──▶ D01 (repeat until approval)

LOOP 3: Lighting ↔ Lookdev ↔ Shading (Material Refinement)
  C07 (ShadingTD) ──shader network──▶ V08 (Lookdev)
  V08 ──lookdev renders──▶ V05 (LightingTD)
  V05 ──lighting test──▶ V08 (feedback)
  V08 ──material tweaks──▶ C07 (shader changes)

LOOP 4: Layout ↔ Director (Shot Intent)
  V04 (LayoutArtist) ──previz──▶ D01 (Director)
  D01 ──shot direction──▶ V04
  V04 ──revised layout──▶ D01 (repeat)

LOOP 5: Quality Gate Review (Department Level)
  Artist ──work──▶ Q02 (DeptLead)
  Q02 ──approved/rejected──▶ Artist
  Q02 ──curated work──▶ D01 (for final approval)

LOOP 6: Postmortem (Project → Future Projects)
  Q04 (Postmortem) ──report──▶ Studio leadership
  Studio leadership ──applied changes──▶ Future projects
```

### 12b. Feedback Loop Characteristics

| Loop | Cadence | Authority | Cost of Change | Typical Iterations |
|------|---------|-----------|----------------|-------------------|
| Director → Braintrust | Weekly/monthly | None (recommendations) | Very high (structural) | 2-5 per production phase |
| Director → Animator | Daily (dailies) | Director (final) | Medium (performance) | 3-10 per shot |
| Lookdev → Shading → Light | Per-asset | Lookdev + Director | Low (material params) | 5-20 per asset |
| Layout → Director | Per-sequence | Director (final) | Medium-High (camera) | 2-6 per sequence |
| DeptLead → Artist | Daily | DeptLead (internal) | Low (within discipline) | 2-8 per task |
| Postmortem → Future | Post-project | Leadership | N/A (next project) | 1 per project |

---

## 13. KEY INSIGHTS

### 13.1 The Four Critical Bottlenecks Are: Geometry, Layout, Lighting, Pipeline

The **Digital Modeler (C04)** is the single most-connected production capability — 10 direct connections spanning rigging, texturing, shading, grooming, creature work, layout, and simulation. It is the gateway through which all physical asset data must pass. **LayoutArtist (V04)** is the decision convergence point where story intent meets spatial execution. **LightingTD (V05)** is the downstream convergence point where all rendered elements combine. **PipelineTD (P04)** is the technical substrate enabling every capability to communicate — if it fails, the entire system stops.

### 13.2 The Pipeline Is a Series of Fork-Join-Merge Patterns

The pipeline is NOT a straight line. It forks at **VisDev (S04)** into character and environment paths, then **joins** at **LayoutArtist (V04)**, then **forks again at Animator (A01)** into FX, simulation, and lighting paths, then **joins** at **LightingTD (V05)**, then **joins** again at **Compositing Supervisor (D08)** for final output. Understanding these fork-join points is critical for parallelism optimization.

### 13.3 Direction Domain Is Universal — Every Capability Depends On It

**FilmDirector (D01)** and similar director capabilities are the ONLY capabilities that ALL 47 others depend on (directly or indirectly). This makes the Director Experience Layer (L1) the single most critical interface in the COS — if creative direction is unclear, every downstream department makes wrong decisions.

### 13.4 Production Domain Is the Second Universal Dependency

**Producer (P01)** and **PipelineTD (P04)** are the only other capabilities that nearly every downstream capability depends on. P01 provides the resource constraints that shape all work; P04 provides the tools enabling all work. Together with D01, these three form the foundational triangle of the COS: **Vision → Resources → Tools**.

### 13.5 The Longest Chain (9 Steps) Runs from Screenwriter to Approval

The critical path from **Screenwriter (S02)** through approval is 9 sequential dependencies. This is the irreducible minimum timeline for a film production — every step in this chain requires the previous step's output. Any acceleration strategy must either compress individual steps or parallelize sub-chains (like character modeling running in parallel with storyboarding).

### 13.6 Quality Domain Operates Orthogonal to Production Flow

**Braintrust (Q01), Department Lead (Q02), QA/QC (Q03), and Postmortem (Q04)** do NOT sit on the production chain — they observe, evaluate, and feed back from the side. This is by design: separating feedback from production authority enables candid evaluation. The Quality Domain is the COS's reflective intelligence.

### 13.7 Game and Film Pipelines Diverge at the Modeling Stage

Film pipeline: **C04 (DigitalModeler) → C05 (Rigger) → A01 (Animator)** — high-fidelity, render-oriented. Game pipeline: **C03 (CharArtist) → C05 (Rigger) → A01 (Animator)** — real-time optimization, engine-oriented. The **Technical Artist (P07)** replaces the **ShadingTD (C07)/Lookdev (V08)** bridge for game pipelines, handling shader/material work directly within engine constraints.

### 13.8 Seven Bridge Capabilities Connect Creative ↔ Technical Worlds

| Bridge Capability | Connects Creative → Technical | Interface Pattern |
|------------------|------------------------------|-------------------|
| V04 LayoutArtist | Storyboards → 3D Camera/Scene | Viz → Spatial |
| C05 Rigger | Character Design → Animation Controls | Design → Mechanics |
| P07 TechArtist | Art Direction → Engine Shaders | Visual → Code |
| P04 PipelineTD | All Depts → Technical Infrastructure | Workflow → Automation |
| D06 VFXSup | Director Vision → VFX Technical Spec | Intent → Parameter |
| D07 CGSup | Creative Intent → 3D Pipeline Standards | Vision → Standards |
| D08 CompSup | Rendered Elements → Final Image | Layers → Integration |

### 13.9 Warning: Five High-Risk Non-Redundant Dependencies

1. **C04 (DigitalModeler)** — No alternative geometry source
2. **C05 (Rigger)** — Animation impossible without rigs
3. **V04 (LayoutArtist)** — No spatial context without layout
4. **V05 (LightingTD)** — Everything converges here; can't skip
5. **P05 (RenderingTD)** — Only path to final frames

### 13.10 Recovery Strategy for Broken Chains

When a critical dependency chain breaks (resource goes down/deadline missed), the COS should:

1. **Identify the break point** — Which capability in the chain is blocked?
2. **Assess downstream impact** — What depends on the blocked capability?
3. **Decouple if possible** — Can downstream work proceed with placeholder data?
4. **Reprioritize unblocked parallel paths** — Accelerate work on paths not dependent on the blockage
5. **Collapse iterations** — Reduce feedback loop iterations on the critical path to recover time
6. **Trigger escalation** — If bottleneck is a decision authority (D01, D06), alert and request rapid decision

---

*End of Capability Dependency Map — 47 capabilities mapped across 7 domains, 11 Production Domain capabilities, 10 Decision Authority flows, 5 critical chains, 2 independent parallel pipelines, 10 bottleneck analysis, and 6 feedback loops documented.*
