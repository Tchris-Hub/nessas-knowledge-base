# Specialist Hierarchy — Creative Operating System

## Attacking the 37-Agent/57-Agent Problem: From Flat List to Structured Hierarchy

**Document ID:** COS-06-AA-002  
**Version:** 1.0  
**Date:** June 14, 2026  
**Status:** Complete  
**Purpose:** Design the ideal specialist hierarchy for the Creative Operating System, reducing the original 37-57 flat-agent idea to a structured 4-tier system with clear merging justifications based on six criteria.

---

## Executive Summary

The original 37-agent / 57-agent concept treated every specialist role as an independent agent in a flat list. Research across Pixar, ILM, Weta, game studios, and VFX houses reveals this is wrong in three ways:

1. **Many capabilities share the same knowledge base** (e.g., Texturing + Shading + Lookdev are all surface appearance) — keeping them separate creates unnecessary handoff overhead.
2. **The dependency graph has clear bottlenecks** (C04 DigitalModeler, V04 LayoutArtist, V05 LightingTD) — these MUST be independent specialists; merging them would create supersized single points of failure.
3. **Decision authority follows a strict hierarchy** — Director-level decisions cannot be made by execution-level agents; the system must respect this separation.

**The result: 23 specialists in 4 tiers (down from 37-57 flat agents).**

| Tier | Name | Count | Function |
|------|------|-------|----------|
| Tier 1 | Core Specialists | 9 | Independent, high-skill, narrow-domain bottleneck roles |
| Tier 2 | Integrated Specialists | 6 | Merged capabilities sharing knowledge bases and tight coupling |
| Tier 3 | Support Specialists | 5 | Infrastructure, pipeline, QA, tools, data management |
| Tier 4 | Direction | 3 | Decision, coordination, feedback authority |

**Net reduction: 37-57 flat agents → 23 structured specialists** (59-40% reduction) achieved through 8 strategic mergers informed by the six criteria below.

---

## Six Criteria for Hierarchy Design

### Criterion 1: Knowledge Overlap
*Do two capabilities share the same knowledge base? If yes, consider merging.*

**Evidence from Specialist Capability Domains:** Six domains show significant knowledge overlap clusters:
- **Surface appearance:** TextureArtist (C06), ShadingTD (C07), Lookdev (V08) — all share PBR theory, material properties, color theory, renderer-specific shader knowledge.
- **Simulation:** FXArtist (V07), SimTD (A05), GroomingTD (C08), CreatureTD (C09) — all share Houdini/VEX, physics simulation, caching strategies, collision handling.
- **Environment:** EnvConcept (V01), ProdDesigner (V02), EnvArtist (V03) — all share architecture, world-building, spatial design, composition.
- **Production management:** Producer (P01), ProdManager (P02), ProdCoord (P03) — all share scheduling, tracking, resource allocation, production tools.
- **Pipeline infrastructure:** PipelineTD (P04), SoftwareEng (P06), SysITEng (P10) — all share Python/C++, pipeline architecture, DCC integration.
- **Quality evaluation:** QAQC (Q03), Postmortem (Q04) — both share process evaluation, metrics analysis, documentation.

**Capabilities with UNIQUE knowledge bases (keep separate):** Screenwriter (narrative craft), StoryArtist (visual narrative), Animator (performance/acting), Rigger (anatomy/kinesiology), LayoutArtist (cinematography/spatial), LightingTD (lighting physics/psychology), DigitalModeler (3D geometry/topology).

### Criterion 2: Communication Frequency
*Do two capabilities constantly need to talk? If yes, consider grouping.*

**Evidence from dependency graph communication patterns:**
- **C06 ↔ C07 ↔ V08** (Texture-Shading-Lookdev): Communicate on every material change — the most frequent communication pattern outside of direction.
- **V07 ↔ V05 ↔ C07** (FX-Lighting-Shading): Communicate on every shot with effects — lighting needs FX sim status; shading needs lighting environment.
- **P01 ↔ P02 ↔ P03** (Production triad): Communicate hourly — daily standups, priority shifts, resource allocation.
- **S02 ↔ S01 ↔ V04** (Story-Layout): Communicate on every sequence during pre-production for camera/staging intent.
- **C04 ↔ C05 ↔ A01** (Model-Rig-Animate): Communicate on every character pass — topology issues, rig limits, animation needs.

**Low communication pairs (keep separate):** S02 (Screenwriter) with A01 (Animator) — never communicate directly. S01 (StoryArtist) with C07 (ShadingTD) — never communicate. High frequency is a strong signal for merging or tight grouping.

### Criterion 3: Decision Coupling
*Does changing one capability's output always require changing another? If yes, consider merging or tight coupling.*

**Evidence from dependency matrix analysis:**
- **C06 ↔ C07 ↔ V08** (CRITICAL COUPLING): Changing a texture map (C06) ALWAYS requires re-shading (C07), which ALWAYS requires re-lookdeving (V08). These cannot be independently modified. **MERGE.**
- **V07 ↔ A05** (CRITICAL COUPLING): FX sims depend on sim methodology; simulation parameters affect FX appearance. A single change (e.g., "make this fire more turbulent") simultaneously affects both. **MERGE.**
- **P01 ↔ P02 ↔ P03** (STRONG COUPLING): A budget reallocation (P01) immediately changes task priorities (P02), which changes daily coordination (P03). **MERGE.**
- **C04 ↔ C05** (WEAK COUPLING, DEPENDENCY DIRECTION): Modeling feeds rigging but changes to the rig don't require re-modeling. Keep separate with interface.
- **V04 ↔ A01** (WEAK COUPLING, DEPENDENCY DIRECTION): Layout feeds animation; animation changes rarely require layout rework. Keep separate.

### Criterion 4: Dependency Direction
*Does A always feed B? Then keep them separate with a clear interface.*

**Evidence from upstream/downstream dependency chains:**
- **S02 → S01 → V04 → A01 → V07 → V05 → P05 → D08** — Clear 8-step sequential chain. Every step feeds the next; there is NO knowledge overlap between adjacent steps. Keep ALL separate with clean interfaces. This is the primary production chain.
- **S04 → C01 → C04 → C05 → A01** — Character asset chain. Each step has unique knowledge (style → design → geometry → controls → performance). Keep separate.
- **C04 → C06 → C07 → V08 → V05** — Material chain. But here, C06/C07/V08 share knowledge. The criterion says "if A always feeds B AND they share knowledge, consider merging." They DO share knowledge. **MERGE C06+C07+V08.**
- **D01 → ALL** — Director feeds EVERYONE. This is not a merge signal — it's a hub-and-spoke pattern. Director stays separate.

### Criterion 5: Bottleneck Analysis
*From the Capability Dependency Map, which capabilities are bottlenecks and should be prioritized as independent specialists vs merged?*

**Evidence from bottleneck ranking (Capability Dependency Map §10):**

| Rank | Capability | Connections | Nature | Decision |
|------|-----------|-------------|--------|----------|
| 1 | C04 DigitalModeler | 10 connections | Central geometry gateway | **Tier 1 Core — MUST be independent** |
| 2 | V04 LayoutArtist | 7 connections | Camera/spatial convergence | **Tier 1 Core — MUST be independent** |
| 3 | V05 LightingTD | 7 connections | Downstream pipeline convergence | **Tier 1 Core — MUST be independent** |
| 4 | A01 Animator | 7 connections | Core creative execution | **Tier 1 Core — MUST be independent** |
| 5 | D01 FilmDirector | 47 connections | Universal direction | **Tier 4 Direction — independent** |
| 6 | P01 Producer | 47 connections | Universal resource control | **Tier 4 Direction — independent** |
| 7 | C05 Rigger | 6 connections | Non-redundant (no rig = no anim) | **Tier 1 Core — MUST be independent** |
| 9 | P04 PipelineTD | ~47 connections | Infrastructure bottleneck | **Tier 3 Support — independent** |

**Non-bottleneck capabilities (safe to merge):**
- C06 TextureArtist (4 connections, no single point of failure)
- C07 ShadingTD (4 connections, part of material chain)
- V08 Lookdev (3 connections, end of material chain)
- V07 FXArtist (3 connections, simulation cluster)
- A05 SimTD (3 connections, simulation cluster)
- C08 GroomingTD (3 connections, narrow specialism)
- C09 CreatureTD (3 connections, narrow specialism)
- P02 ProdManager (3 connections, production management cluster)
- P03 ProdCoord (2 connections, production management cluster)
- Q04 Postmortem (1 connection, narrow function)

**Key insight:** Bottlenecks should NOT be merged — merging a bottleneck with another capability creates an even worse bottleneck. Non-bottleneck capabilities with shared knowledge SHOULD be merged to reduce handoff overhead.

### Criterion 6: Failure Isolation
*Can one capability fail independently without taking down others?*

**Evidence from non-redundant dependency analysis (Capability Dependency Map §10b):**

**Non-redundant (MUST have independent failure domains):**
1. C04 DigitalModeler — No alternative geometry source. If it fails, rigging, texturing, shading, layout, simulation ALL stop.
2. C05 Rigger — No alternative way to produce animation-ready controls. Animation impossible without rigs.
3. V04 LayoutArtist — No alternative path for camera/scene staging. Animators don't know where to place characters.
4. V05 LightingTD — Convergence point of ALL downstream work. If blocked, rendering and compositing stop.
5. P05 RenderingTD — Only path to final frames. Compositing has nothing to work with if rendering is blocked.
6. P04 PipelineTD — If pipeline tools break, NO department can publish or load assets.

These six MUST be independent specialists with isolated failure domains (Tier 1 or Tier 3).

**Safe-to-merge (shared failure domain is acceptable or even beneficial):**
- C06+C07+V08: If texturing fails, shading is blocked anyway. They share a failure domain. **Merging doesn't worsen failure isolation.**
- V07+A05+C08+C09: If one simulation capability fails, the others often can't proceed anyway (shared physics data). **Merging is safe.**
- P01+P02+P03: If the producer is blocked, production management is blocked as a unit. **Merging reflects the reality that they share a failure domain.**
- Q03+Q04: Both are evaluation capabilities that operate orthogonal to production flow. **Merging doesn't affect production failure modes.**

---

## Proposed Hierarchy

---

## TIER 1: CORE SPECIALISTS (9)

*Independent, high-skill, narrow-domain specialists occupying critical bottleneck positions in the dependency graph. Each has a unique knowledge base with no significant overlap with other capabilities. Each is a non-redundant bottleneck — if it fails, production stops. All MUST be independent agents with isolated failure domains.*

### 1.1 Digital Modeler (C04)

**Source capability:** Digital Modeler / 3D Modeler  
**Bottleneck rank:** #1 (10 connections)  
**Knowledge base:** 3D geometry, topology, edge flow, subdivision surfaces, NURBS, hard-surface vs. organic modeling, spatial reasoning, UV mapping basics  
**Why independent:** Central geometry gateway — NO alternative path exists. 10 direct connections span rigging (C05), texturing (C06), shading (C07), grooming (C08), creature work (C09), layout (V04), and simulation (A05). Merging would create a catastrophic single point of failure for the entire 3D pipeline.  
**Failure isolation:** Non-redundant — if modeling is blocked, every downstream 3D department stops.  
**Interface:** Receives design sheets (C01) and vis dev style (S04). Produces clean 3D wireframe geometry with proper topology at multiple LODs.

### 1.2 Rigger (C05)

**Source capability:** Rigger / Rigging TD  
**Bottleneck rank:** #7 (6 connections)  
**Knowledge base:** Anatomy and kinesiology, joint/deformation mathematics, skin weighting, blend shapes, constraint systems, Maya/Houdini rigging, Python scripting  
**Why independent:** Non-redundant bottleneck — animation is impossible without a rig. Unique knowledge of skeleton/muscle/deformation systems is not shared by any other capability. Rigging decisions (topology, joint placement, deformation approach) cascade into animation quality, creature sim, and even lighting (deformation under light).  
**Failure isolation:** Non-redundant — no rig means no animation.  
**Interface:** Receives clean 3D model with proper topology (C04). Produces animation-ready rig with skeleton, controls, and deformers.

### 1.3 Layout Artist (V04)

**Source capability:** Layout Artist / Previz Artist  
**Bottleneck rank:** #2 (7 connections)  
**Knowledge base:** Cinematography (camera angles, lens choice, composition), spatial reasoning, blocking and staging, storytelling through camera, continuity editing, 3D scene assembly  
**Why independent:** Decision convergence point where story intent meets spatial execution — unique cinematography knowledge that no other capability possesses. Single point where storyboards, 3D assets, camera data, and director intent must converge.  
**Failure isolation:** Non-redundant — no alternative path for camera/scene setup. Animators and FX artists require spatial context from layout.  
**Interface:** Receives storyboards (S01), 3D assets (C04), camera data (A03), director intent (D01). Produces 3D layout scenes with camera placement and blocking.

### 1.4 Animator (A01)

**Source capability:** Animator / Character Animator  
**Bottleneck rank:** #4 (7 connections)  
**Knowledge base:** 12 Principles of Animation, acting and performance, body mechanics, facial expression, timing and spacing, weighting, game animation state machines, blend trees  
**Why independent:** Core creative execution with unique performance knowledge. Animation quality is the single most visible creative output — it's where the character "comes to life." Animation feeds FX, simulation, lighting, compositing, and animation tools. The artistic judgment of performance cannot be merged with technical domains.  
**Failure isolation:** Non-redundant in terms of execution (layout needs animated characters to light), though placeholder animation can be used for lighting setup.  
**Interface:** Receives functional rig (C05), camera/scene (V04), performance direction (D01/D11). Produces animated shots, animation curves, clips.

### 1.5 Lighting TD (V05)

**Source capability:** Lighting TD / Lighting Artist  
**Bottleneck rank:** #3 (7 connections)  
**Knowledge base:** Lighting theory (3-point, practical, motivated, artistic), color temperature and light physics, renderer-specific lighting, HDR image-based lighting, exposure/color grading, shadow theory, mood/atmosphere communication  
**Why independent:** Downstream convergence point where ALL rendered elements combine — shaded models, FX simulations, lookdev materials, animated characters, environments. Unique knowledge of lighting physics and psychology. Lighting decisions directly determine render time, which is a critical production constraint.  
**Failure isolation:** Non-redundant — lighting is the convergence point; if lighting is blocked, rendering and compositing stop.  
**Interface:** Receives layout scene (V04), materials (C07/V08), FX validation (V07), sim context (A05). Produces lit shots, AOVs, lighting templates.

### 1.6 Screenwriter (S02)

**Source capability:** Screenwriter / Writer  
**Knowledge base:** Dramatic structure (McKee principles), character arcs, dialogue craft, genre conventions, theme and subtext, story spine design  
**Why independent:** Unique narrative craft knowledge — no other capability writes script or dialogue. Screenwriter feeds EVERY downstream capability (S01, S03, S04, D01, C01, V01). Narrative decisions made here cascade through the entire production.  
**Failure isolation:** Can fail independently — if the script is bad but technically complete, production can proceed (to poor results).  
**Interface:** Receives director creative vision (D01), producer approval (P01). Produces script, treatment, character bibles.

### 1.7 Storyboard Artist (S01)

**Source capability:** Story Artist / Storyboard Artist  
**Knowledge base:** Cinematic language (shot types, camera angles, transitions), narrative structure, character expression/body language, timing and pacing intuition, staging and composition, acting fundamentals  
**Why independent:** First visual translation of narrative — unique visual narrative knowledge distinct from both writing (S02) and cinematography (V04). Storyboarding decisions about shot composition, camera angle, and pacing determine the entire visual vocabulary of the production.  
**Failure isolation:** Can fail independently — downstream can proceed with text-only script and layout-defined camera.  
**Interface:** Receives script (S02), director direction (D01), character/environment reference (C01, V01). Produces storyboard panels, animatics, shot breakdowns.

### 1.8 Character Designer (C01)

**Source capability:** Character Designer  
**Bottleneck rank:** #8 (6 connections)  
**Knowledge base:** Anatomy and proportion, silhouette design, shape language theory, color theory, costume/fashion design, character archetypes, personality encoding through visual design  
**Why independent:** Character visual design is a unique creative discipline that feeds the entire character pipeline (modeling, sculpting, texturing, rigging). Design decisions about silhouette, proportion, and shape language cascade through all downstream 3D work. Cannot share knowledge with any other capability.  
**Failure isolation:** Can fail independently — production can proceed with existing character designs or use generic templates.  
**Interface:** Receives character description (S02), style guide (S04), director direction (D01). Produces turnarounds, expression sheets, orthographic views.

### 1.9 Compositing Supervisor (D08)

**Source capability:** Compositing Supervisor  
**Knowledge base:** Deep compositing (Nuke), color theory and grading, cinematography, light integration, AOV usage, creative eye for realism, multi-layer blending  
**Why independent:** Final image integration — the last creative gate before delivery. Unique compositing knowledge combining all rendered elements (lighting, FX, matte paintings) into the final image. Compositing decisions (color grading, light integration, grain matching) are the final creative pass.  
**Failure isolation:** Non-redundant — this is the ONLY path to final output.  
**Interface:** Receives AOVs (V05/render), plates (editorial), VFX sup direction (D06). Produces final shot composites.

---

## TIER 2: INTEGRATED SPECIALISTS (6)

*Merged capabilities that share knowledge bases, communicate frequently, have tight decision coupling, and share acceptable failure domains. Each cluster represents capabilities that should have been a single specialist from the start.*

### 2.1 Surface & Material Artist (merged from C06 + C07 + V08)

**Merged capabilities:** Texture Artist (C06) + Shading/Surfacing TD (C07) + Look Development Artist (V08)

**Research evidence for merger:**

| Criterion | Evidence | Verdict |
|-----------|----------|---------|
| **Knowledge overlap** | ALL three share PBR theory, material properties, color theory, renderer-specific shader knowledge, surface appearance physics. C06 creates the maps, C07 builds the shader network, V08 evaluates the final look. This is ONE knowledge domain (surface appearance), not three. | MERGE |
| **Communication frequency** | C06→C07 communicate on every texture map change. C07→V08 communicate on every shader parameter adjustment. V08→C07 feeds back material tweaks. This is a 24/7 conversation loop, not independent work. | MERGE |
| **Decision coupling** | Changing a texture map ALWAYS requires re-shading, which ALWAYS requires re-lookdeving. They cannot be independently modified. C06→C07→V08 is a tightly coupled chain where changes propagate 100%. | MERGE |
| **Dependency direction** | A always feeds B always feeds C (C06→C07→V08). But because they share the SAME knowledge base and have TIGHT decision coupling, criterion 4's "keep separate" recommendation is overridden by the combined weight of criteria 1-3. | MERGE (overrides criterion 4) |
| **Bottleneck analysis** | None of the three is a top-10 bottleneck. C06 has 4 connections, C07 has 4, V08 has 3. Merging creates a single agent with ~5 connections — manageable. | MERGE safe |
| **Failure isolation** | If texturing fails, shading is blocked anyway. If shading fails, lookdev is blocked. They already share a failure domain. Merging doesn't worsen failure isolation. | MERGE |

**Resulting specialist name:** Surface & Material Artist  
**Merged knowledge base:** PBR theory, shader network architecture, texture map generation (diffuse, specular, roughness, normal, displacement, AO), material layering, renderer-specific shading languages (OSL, VEX), color theory, procedural texturing (Substance Designer), hand-painted texturing (Mari, Photoshop), photorealistic surface evaluation  
**Pipeline position:** Receives UV'd geometry (C04) and reference (C01). Produces finalized lookdev materials, shader definitions, texture maps.  
**Guarded assumption:** This merger eliminates the handoff overhead between texture, shading, and lookdev — estimated to reduce material iteration time by 30-40% based on the observed tightness of this coupling.

### 2.2 Simulation & FX Artist (merged from V07 + A05 + C08 + C09)

**Merged capabilities:** FX Artist/VFX Artist (V07) + Simulation TD (A05) + Grooming TD (C08) + Creature TD (C09)

**Research evidence for merger:**

| Criterion | Evidence | Verdict |
|-----------|----------|---------|
| **Knowledge overlap** | ALL four share Houdini/VEX as primary tools, physics simulation methodology, caching strategies, collision handling, art-directed physics, wedge testing. V07 (FX) and A05 (Sim) are explicitly noted as overlapping in the capability domains document. C08 (Grooming) and C09 (Creature) are simulation-heavy sub-specialties. This is a SINGLE simulation knowledge domain. | MERGE |
| **Communication frequency** | FX sims need simulation parameters. Creature sims feed into FX environments. Grooming outputs feed into lighting/FX scenes. These capabilities work on the same shots simultaneously. | MERGE |
| **Decision coupling** | A simulation parameter change (e.g., "increase fluid resolution") simultaneously affects V07 (FX appearance), A05 (sim cost), and C09 (creature interaction). They cannot be optimized independently. | MERGE |
| **Dependency direction** | A05 feeds V07 (sim base for FX). C09 feeds A05 (creature sim into environment sim). But the flows are bidirectional during iteration — changes to FX force re-simulation. | MERGE |
| **Bottleneck analysis** | None is a top-10 bottleneck. V07 has 3 connections, A05 has 3, C08 has 3, C09 has 3. Merging creates ~5 unique connections. | MERGE safe |
| **Failure isolation** | If simulation resources are saturated, all four are blocked anyway. They share compute resources (Houdini engines, simulation caches). Merging is safe. | MERGE |

**Resulting specialist name:** Simulation & FX Artist  
**Merged knowledge base:** Physics simulation (fluids, rigid bodies, particles, cloth, destruction), Houdini/VEX, simulation caching, art-directed physics, hair/fur grooming (XGen, Yeti), creature muscle/flesh/skin simulation (FEM, spring-based), wedge testing, render optimization for FX passes  
**Pipeline position:** Receives animated assets (A01), sim-ready geometry (C04), scene context (V04). Produces simulation caches, FX render layers, groom assets, creature setups.  
**Guarded assumption:** This merger recognizes that the distinction between "FX for visual impact" and "simulation for physical accuracy" is an art-direction spectrum, not a hard boundary. One agent manages all physics-based work.

### 2.3 Environment World-Builder (merged from V01 + V02 + V03)

**Merged capabilities:** Environment Concept Artist (V01) + Production Designer (V02) + Environment Artist (V03)

**Research evidence for merger:**

| Criterion | Evidence | Verdict |
|-----------|----------|---------|
| **Knowledge overlap** | ALL three share architecture, world-building, spatial design, composition, lighting fundamentals. V01 creates the concept, V02 defines the production design, V03 builds the 3D environments. Shared understanding of architectural styles, terrain composition, and visual storytelling through space. | MERGE |
| **Communication frequency** | V01→V03 communicate on every environment pass (concept refinement for 3D build). V02 coordinates between both. This is a single department in most studios. | MERGE |
| **Decision coupling** | Changing an environment concept (V01) ALWAYS requires rebuilding the 3D environment (V03). Production design decisions (V02) cascade to both. | MERGE |
| **Dependency direction** | V01→V03→V04 (concept→build→layout). But V01 and V03 share environment knowledge. | MERGE |
| **Bottleneck analysis** | None is a top-10 bottleneck. V01 has 3 connections, V02 has 3, V03 has 3. Merged agent has ~5 connections. | MERGE safe |
| **Failure isolation** | Environment work is a single pipeline stage. Merging doesn't introduce new failure modes. | MERGE |

**Resulting specialist name:** Environment World-Builder  
**Merged knowledge base:** Architecture and architectural history, landscape design, world-building logic, mood/atmosphere communication, set design, modular level design, 3D environment modeling (Maya, Blender), terrain tools, material creation (Substance), engine-level assembly (Unreal, Unity), real-time optimization  
**Pipeline position:** Receives vis dev style (S04), director vision (D01), layout requirements (V04). Produces concept art, 3D environment meshes, engine-ready levels, production design bible, mood paintings.

### 2.4 Technical Artist (merged from C03 + P07)

**Merged capabilities:** Character Artist Game (C03) + Technical Artist Game (P07)

**Research evidence for merger:**

| Criterion | Evidence | Verdict |
|-----------|----------|---------|
| **Knowledge overlap** | Both are game-engine-oriented, real-time optimized roles. C03 creates engine-ready character assets; P07 creates shaders and tools for those assets. Shared knowledge of game engines (Unreal, Unity), polygon budgets, PBR for real-time, performance constraints. | MERGE |
| **Communication frequency** | P07 provides shader/material frameworks that C03 uses directly. They work on the same asset pipeline. | MERGE |
| **Decision coupling** | Changing engine constraints (P07) ALWAYS affects asset creation approach (C03). Changing asset requirements (C03) ALWAYS affects tool needs (P07). | MERGE |
| **Bottleneck analysis** | C03 has 2 connections. P07 has 3 connections. Neither is a bottleneck. | MERGE safe |
| **Failure isolation** | Both are game-pipeline specific. If the game pipeline is blocked, both are blocked. | MERGE |

**Resulting specialist name:** Technical Artist  
**Merged knowledge base:** Game engine pipeline (Unreal, Unity), high/low-poly sculpting (ZBrush), retopology, UV mapping, PBR texturing (Substance), shader programming (HLSL, GLSL, node-based), real-time rendering, art pipeline optimization, performance profiling  
**Pipeline position:** Receives character concept (C01), environment concept (V01), engine constraints (D10), art direction (D09). Produces engine-ready character assets, shaders, art pipeline tools, optimized materials.  
**Note:** This specialist is primarily active in game production pipelines. For film/VFX pipelines, the Surface & Material Artist (Tier 2.1) handles the equivalent function.

### 2.5 Narrative Designer (S03 — standalone integrated specialist)

**Source capability:** Narrative Designer  
**Knowledge base:** Interactive storytelling (branching narrative, player agency, emergent narrative), game design fundamentals, scripting/lua, dialogue database management, quest design, player psychology  
**Why standalone (not merged with Screenwriter):** Screenwriter (S02) owns linear narrative craft. Narrative Designer (S03) owns interactive narrative implementation. Though both work with story, their knowledge bases diverge completely at the implementation level — S02 writes scripts, S03 builds dialogue trees and quest logic in game engines. Merging them would produce a specialist that is neither a great writer nor a great systems designer.  
**Why Tier 2 (not Tier 1):** Narrow domain focused on game/interactive production. Not a bottleneck (3 connections). Can fail independently without stopping the main production chain.  
**Pipeline position:** Receives script (S02), game design direction (D03), level layouts. Produces dialogue trees, quest scripts, branching narrative maps, interactive story implementation.

### 2.6 Rendering Operations (merged from P05 + P08)

**Merged capabilities:** Rendering TD (P05) + Render Wrangler (P08)

**Research evidence for merger:**

| Criterion | Evidence | Verdict |
|-----------|----------|---------|
| **Knowledge overlap** | Both manage render output. P05 optimizes render settings and quality. P08 manages render farm operations. Shared knowledge of render engines, farm management tools, render budgets. | MERGE |
| **Communication frequency** | P05 submits jobs to P08; P08 reports farm status back. They are operationally inseparable. | MERGE |
| **Decision coupling** | Changing render settings (P05) changes farm load (P08). Farm queue decisions (P08) affect render quality strategy (P05). | MERGE |
| **Bottleneck analysis** | P05 is a non-redundant bottleneck (#6 in original ranking) — only path to final frames. Merging with P08 doesn't worsen this. | MERGE (bottleneck status preserved) |
| **Failure isolation** | P05 failure already stops rendering. Merging with P08 doesn't add new failure modes. | MERGE |

**Resulting specialist name:** Rendering Operations  
**Merged knowledge base:** Render engine configuration (RenderMan, Arnold, V-Ray, Cycles), render farm management (Deadline, Tractor, Plow, OpenCue), ray tracing and sampling theory, GPU/CPU rendering balance, render optimization (sampling, caching, denoising), farm capacity planning, job queue prioritization, troubleshooting rendering artifacts  
**Pipeline position:** Receives lit scenes (V05), materials (Surface & Material Artist), farm capacity (Systems/IT). Produces final rendered frames, optimized render settings.

---

## TIER 3: SUPPORT SPECIALISTS (5)

*Infrastructure, pipeline, QA, tools, data management. These capabilities enable all production work but operate orthogonal to the creative pipeline. They share acceptable failure domains with production infrastructure.*

### 3.1 Pipeline & Tools Engineering (merged from P04 + P06 + P10)

**Merged capabilities:** Pipeline TD (P04) + Software Engineer/Tools Developer (P06) + Systems/IT Engineer (P10)

**Research evidence for merger:**

| Criterion | Evidence | Verdict |
|-----------|----------|---------|
| **Knowledge overlap** | ALL three build and maintain technical infrastructure. P04 builds pipeline tools, P06 builds core software, P10 builds hardware infrastructure. Shared Python/C++, Linux/Unix, pipeline architecture, DCC integration (Maya, Houdini, Nuke APIs). They are three layers of the same engineering stack. | MERGE |
| **Communication frequency** | P04 needs P06's core software to build pipeline tools. P06 needs P10's infrastructure to deploy. P10 needs P04's requirements to provision hardware. | MERGE |
| **Decision coupling** | Changing infrastructure (P10) breaks tools (P04). Changing core software (P06) breaks pipelines (P04). They must be coordinated. | MERGE |
| **Bottleneck analysis** | P04 is a critical bottleneck (#9, ~47 connections). Merging with P06 and P10 creates a unified "engineering" team, which is how real studios organize (one engineering department). The bottleneck is managed by having this as a Support tier, not a Core tier. | MERGE (with clear internal roles) |
| **Failure isolation** | P04 failure already stops all departments. P06 failure already affects all departments. P10 failure already stops production. They share a universal failure domain. | MERGE |

**Resulting specialist name:** Pipeline & Tools Engineering  
**Merged knowledge base:** Python/C++, DCC APIs (Maya, Houdini, Nuke), pipeline architecture patterns, USD, version control (Perforce, Git), render farm infrastructure, storage systems, network engineering, backup/recovery, build systems, environment standardization, containerization  
**Pipeline position:** Enables ALL departments. Receives workflow requirements from all capabilities. Produces pipeline tools, plugins, scripts, automation systems, environment configurations, infrastructure.

### 3.2 Production Management (merged from P01 + P02 + P03)

**Merged capabilities:** Producer (P01) + Production Manager (P02) + Production Coordinator (P03)

**Note:** P01 (Producer at the project level) is listed here as part of Production Management. The Producer role that holds universal resource authority (47 connections) is preserved as the lead of this specialist, with the Manager and Coordinator as internal sub-capabilities.

**Research evidence for merger:**

| Criterion | Evidence | Verdict |
|-----------|----------|---------|
| **Knowledge overlap** | ALL three share production management, scheduling, tracking, resource allocation, team coordination. P01 sets strategy, P02 manages execution, P03 handles logistics. One knowledge domain (production management) at three operational levels. | MERGE |
| **Communication frequency** | P01↔P02 communicate daily on schedule/resource shifts. P02↔P03 communicate hourly on task assignments. They talk more to each other than to anyone else. | MERGE |
| **Decision coupling** | P01 budget reallocation immediately changes P02's task priorities, which changes P03's daily coordination. Tightly coupled. | MERGE |
| **Bottleneck analysis** | P01 is a top-6 bottleneck (47 connections). Merging with P02/P03 preserves the bottleneck's authority while giving it execution capacity. The Producer remains the single point of resource authority, now supported by Manager and Coordinator sub-capabilities. | MERGE (hierarchical) |
| **Failure isolation** | If production management fails, no department receives schedule or resource allocation. This is already a shared failure domain. | MERGE |

**Resulting specialist name:** Production Management  
**Merged knowledge base:** Production management, budget/schedule planning, resource allocation, risk management, shot/asset tracking (ShotGrid, ftrack), version control, dailies logistics, team coordination, milestone gate management  
**Pipeline position:** Enables ALL departments. Receives creative vision (Director), department requests, team capacity. Produces budget, schedule, task assignments, milestone gates, version tracking.

### 3.3 QA & Knowledge Management (merged from Q03 + Q04 + P11)

**Merged capabilities:** Quality Assurance/QC Specialist (Q03) + Postmortem Facilitator (Q04) + Asset Manager/Librarian (P11)

**Research evidence for merger:**

| Criterion | Evidence | Verdict |
|-----------|----------|---------|
| **Knowledge overlap** | ALL three manage process quality through evaluation and documentation. Q03 evaluates technical quality, Q04 evaluates process quality, P11 manages knowledge through asset organization. Shared evaluation/documentation/organization skills. | MERGE |
| **Communication frequency** | Q03's bug reports feed Q04's postmortem analysis. Q04's findings feed P11's asset organization strategy. | MERGE |
| **Decision coupling** | Quality issues found by Q03 inform postmortem findings (Q04). Asset organization (P11) reflects lessons learned from both. | MERGE |
| **Bottleneck analysis** | None is a bottleneck. | MERGE safe |
| **Failure isolation** | ALL operate orthogonal to production flow. A QA delay doesn't stop creative work. | MERGE safe |

**Resulting specialist name:** QA & Knowledge Management  
**Merged knowledge base:** Platform certification standards (TRC, XR, Lotcheck), bug tracking systems, playtesting methodology, performance profiling, color space/delivery spec standards, facilitation and group dynamics, postmortem methodology, asset management systems, metadata schemas, archival procedures  
**Pipeline position:** Receives builds/renders (from all departments), project data (from Production Management). Produces QA reports, bug lists, certification status, postmortem reports, organized asset library, institutional knowledge documentation.

### 3.4 Capture & Tracking (merged from A03 + A04)

**Merged capabilities:** Matchmove Artist (A03) + Motion Capture TD (A04)

**Research evidence for merger:**

| Criterion | Evidence | Verdict |
|-----------|----------|---------|
| **Knowledge overlap** | Both capture real-world data and translate it into 3D. Matchmove tracks cameras; Mocap tracks performance. Shared knowledge of 3D tracking mathematics, coordinate systems, skeleton hierarchies, solving algorithms. | MERGE |
| **Communication frequency** | Both work with the same on-set data pipeline. Matchmove creates the camera space that mocap animation operates in. | MERGE |
| **Decision coupling** | Matchmove solve quality affects mocap retargeting accuracy. They are independent in execution but coupled at the data layer. | MERGE |
| **Failure isolation** | Both can fail independently without stopping creative work (production can use keyframe animation as fallback). | MERGE safe |

**Resulting specialist name:** Capture & Tracking  
**Merged knowledge base:** Camera optics, 3D tracking mathematics, photogrammetry, motion capture hardware (Vicon, OptiTrack, Faceware), solve algorithms, retargeting mathematics, skeleton hierarchies, cleanup/denoising strategies  
**Pipeline position:** Receives live-action plates, lens metadata, on-set capture data. Produces solved camera data, tracking nulls, cleaned mocap data, retargeted animation.

### 3.5 Research Scientist (P09 — standalone)

**Source capability:** Research Scientist / R&D Researcher  
**Knowledge base:** Advanced computer graphics, simulation physics, geometry processing, machine learning, SIGGRAPH publication standards, prototype development  
**Why standalone:** Unique R&D knowledge base that operates on a 5+ year horizon — completely different cadence and methodology from production capabilities. Cannot be merged with any production role.  
**Why Tier 3:** Not on the production critical path. Research feeds future tools and techniques, not current output.  
**Pipeline position:** Receives production technology challenges, research budget. Produces publications, algorithms, prototypes.

---

## TIER 4: DIRECTION (3)

*Decision, coordination, and feedback authority. These capabilities hold final creative and resource authority, provide strategic vision, and maintain the feedback infrastructure that drives quality. Following the key architectural insight from Creative Roles as Functions — feedback MUST be separated from approval.*

### 4.1 Director (creative authority — D01/D03/D05/D06/D07/D10)

**Merged capabilities:** Film Director (D01) + Game Director (D03) + Showrunner (D05) + VFX Supervisor (D06) + CG Supervisor (D07) + Technical Director (D10)

**Research evidence for this grouping (not merger — shared TIER):**

| Criterion | Evidence | Verdict |
|-----------|----------|---------|
| **Knowledge overlap** | ALL six hold final decision authority in their domain. They share leadership/decision-making knowledge but have DIFFERENT domain expertise (film craft vs. game design vs. VFX pipeline vs. CG technology vs. engineering). | **Group in same tier, DO NOT merge** |
| **Decision coupling** | FilmDirector and VFXSup communicate constantly on shot approval. But their knowledge bases are distinct. | Group in same tier |
| **Dependency direction** | D06 depends on D01 for creative vision. D07 depends on D06 for direction. D10 depends on D03 for design vision. Clear hierarchy within the tier. | Keep separate with interfaces |
| **Bottleneck analysis** | D01 is a universal bottleneck (47 connections). D03 is a universal bottleneck for game projects. D06 is a VFX gate bottleneck. These are authority bottlenecks that CANNOT be merged because they represent different domains of authority. | **KEEP SEPARATE, same tier** |

**Resulting specialists (each INDEPENDENT within Tier 4):**

| Specialist | Domain | Authority | Key Interface |
|------------|--------|-----------|---------------|
| **Creative Director** (D01/D03/D05) | Overall creative vision | Final creative say | Receives Braintrust feedback, approves all shots |
| **VFX/CG Supervisor** (D06/D07) | Visual effects + CG pipeline | VFX quality gate, technical standards | Translates creative intent to technical specs |
| **Technical Director** (D10) | Engineering + Game tech | Tech feasibility, architecture | Validates creative vision against technical constraints |

**Why not merge Creative Director and VFX Sup?** They have DIFFERENT knowledge bases. Creative Director knows story/film craft. VFX Sup knows VFX pipeline/technique. Merging would produce a specialist that is neither a strong creative voice nor a strong technical leader. This is consistent with studio practice where the Director and VFX Supervisor are always separate people.

**Why not merge CG Sup and Tech Director?** CG Sup (D07) is film/VFX-centric (3D pipeline, render technology), while Tech Director (D10) is game-centric (engine architecture, real-time performance). They share technical authority but serve different production types.

### 4.2 Producer (resource authority — P01)

**Source capability:** Producer / Production Management Lead  
**Note:** P01 is listed here as the lead of the Production Management specialist (Tier 3.2), but retains an independent role in Tier 4 for the resource authority function. This dual-role is consistent with real studios where the Producer sits in leadership (setting budget/schedule) while the Production Manager and Coordinator execute.

**Authority:** Budget allocation, resource distribution, milestone gates, schedule viability  
**Key interface:** Receives creative vision (Director), team capacity (Production Management). Produces budget/schedule constraints for ALL departments.  
**Why Tier 4:** P01 has universal authority over 47 connections — only the Director has more. Resource decisions (budget cuts, schedule changes) cascade through every capability. This authority cannot live in a support tier.

### 4.3 Braintrust (feedback authority — Q01)

**Source capability:** Braintrust (Pixar)  
**Knowledge base:** Narrative craft principles, pattern recognition from multiple productions, genre conventions, candor delivery, cross-domain awareness, creative problem diagnosis  
**Why independent:** Per the central architectural insight from Creative Roles as Functions — "The Braintrust is a FEEDBACK function that is architecturally SEPARATE from the APPROVAL function." Braintrust MUST have zero authority to maintain psychological safety and candor. If merged with any decision-making capability, the candor contract is violated.  
**Authority:** ZERO decision authority by design. Generates feedback signals only. Cannot approve, reject, block, or mandate.  
**Key interface:** Receives work-in-progress from Director (only). Produces non-binding feedback signals TO Director (only). The Braintrust NEVER communicates directly with executing departments — feedback flows through the Director.  
**Why Tier 4:** The Braintrust sits at the top of the quality stack, providing the highest-level creative evaluation. Its feedback influences all other tiers, but it has no authority over them.

**Failure isolation:** Braintrust failure (e.g., no sessions held) degrades creative quality but does not stop production. Production can proceed without Braintrust feedback; it just makes worse creative decisions.

---

## Summary: Mergers and Keep-Separate Decisions

### 8 Strategic Mergers (20 capabilities → 6 integrated specialists)

| Merger ID | Merged Capabilities | Resulting Specialist | Tier | Primary Justification |
|-----------|-------------------|---------------------|------|----------------------|
| M1 | C06 + C07 + V08 | Surface & Material Artist | 2 | Knowledge overlap + decision coupling (strongest merge signal) |
| M2 | V07 + A05 + C08 + C09 | Simulation & FX Artist | 2 | Knowledge overlap (Houdini/physics) + shared tools |
| M3 | V01 + V02 + V03 | Environment World-Builder | 2 | Knowledge overlap (spatial design) + sequential pipeline |
| M4 | C03 + P07 | Technical Artist | 2 | Knowledge overlap (game engine pipeline) |
| M5 | P05 + P08 | Rendering Operations | 2 | Operational coupling + shared tools |
| M6 | P04 + P06 + P10 | Pipeline & Tools Engineering | 3 | Knowledge overlap (infrastructure engineering) |
| M7 | P01 + P02 + P03 | Production Management | 3 | Knowledge overlap + decision coupling (tightest) |
| M8 | Q03 + Q04 + P11 | QA & Knowledge Management | 3 | Knowledge overlap (evaluation/organization) |
| M9 | A03 + A04 | Capture & Tracking | 3 | Knowledge overlap (3D tracking/reconstruction) |

### 14 Capabilities Kept Independent (Tier 1 + Tier 4 + standalone)

| Capability | Tier | Reason for Independence |
|-----------|------|------------------------|
| C04 DigitalModeler | 1 | #1 bottleneck (10 connections), unique knowledge, non-redundant |
| C05 Rigger | 1 | #7 bottleneck (6 connections), unique knowledge, non-redundant |
| V04 LayoutArtist | 1 | #2 bottleneck (7 connections), unique cinematography knowledge |
| A01 Animator | 1 | #4 bottleneck (7 connections), unique performance knowledge |
| V05 LightingTD | 1 | #3 bottleneck (7 connections), unique lighting knowledge |
| S02 Screenwriter | 1 | Unique narrative craft knowledge, feeds all story work |
| S01 Storyboard Artist | 1 | Unique visual narrative knowledge |
| C01 Character Designer | 1 | Unique visual character design knowledge |
| D08 Compositing Supervisor | 1 | Final image gate, unique compositing knowledge |
| S03 Narrative Designer | 2 | Unique interactive narrative knowledge (can't merge with S02) |
| P09 Research Scientist | 3 | 5+ year R&D horizon, unique research knowledge |
| D01/D03/D05 Creative Director | 4 | Universal creative authority (47 connections) |
| D06/D07 VFX/CG Supervisor | 4 | Unique VFX domain authority |
| D10 Technical Director | 4 | Unique engineering/architecture authority |
| P01 Producer | 4 | Universal resource authority (47 connections) |
| Q01 Braintrust | 4 | Feedback-authority separation (architectural principle) |

### 5 Capabilities Folded as Internal Sub-Capabilities

| Capability | Absorbed By | Rationale |
|-----------|-------------|-----------|
| C02 Sculptor (Physical) | Digital Modeler (C04, Tier 1) | Narrow physical-only role; modern pipelines skip physical maquettes. The Digital Modeler includes "reference acquisition" as a sub-capability. |
| A02 Animation TD | Animator (A01, Tier 1) | Animation TD builds tools FOR the Animator. This is an internal support function within the Animation specialist. The Animator agent has an internal "tools & scripting" sub-capability. |
| D09 Art Director | Visual Language Director (merged S04+D09, Tier 1) | Art Director enforces the style that VisDev creates. They share visual language knowledge. This is a single specialist with internal creative (VisDev) and quality (ArtDir) modes. |
| D11 Animation Supervisor | Animator (A01, Tier 1) | The Animation Supervisor is a quality/senior function within the Animation discipline. The Animator agent has an internal "quality review" mode. |
| Q02 Department Lead | Each Core Specialist (Tier 1/2, internal) | Department Lead is a quality gate within each discipline. Each specialist has a "lead" mode that performs first-pass quality evaluation before Director review. |
| V06 Matte Painter | Compositing Supervisor (D08, Tier 1) | Matte painting is a compositing technique (2D projection into 3D scenes). It is a sub-capability of compositing, not an independent role requiring a specialist agent. |

---

## Final Agent Count: 23 Specialists

| Tier | Count | Specialists |
|------|-------|-------------|
| **Tier 1: Core** | 9 | DigitalModeler, Rigger, LayoutArtist, Animator, LightingTD, Screenwriter, StoryboardArtist, CharacterDesigner, CompositingSupervisor |
| **Tier 2: Integrated** | 6 | Surface&MaterialArtist, Simulation&FXArtist, EnvironmentWorldBuilder, TechnicalArtist, NarrativeDesigner, RenderingOperations |
| **Tier 3: Support** | 5 | Pipeline&ToolsEngineering, ProductionManagement, QA&KnowledgeManagement, Capture&Tracking, ResearchScientist |
| **Tier 4: Direction** | 3 | CreativeDirector, VFX/CG Supervisor, TechnicalDirector (with Producer and Braintrust as independent authority functions) |
| **Total** | **23** | (down from 37-57 flat agents — a 59-40% reduction) |

**Additional authority functions within Tier 4 that are NOT separate agents but internal capabilities:**
- Producer (resource authority — embedded within Production Management specialist as the senior role)
- Braintrust (feedback authority — embedded within QA & Knowledge Management specialist with strict feedback-vs-approval separation)

---

## Communication Architecture Between Tiers

### Direction (Tier 4) → Core (Tier 1/2): Brief + Approve
- Creative Director issues creative briefs → Core Specialists execute
- Creative Director approves/rejects work → Core Specialists iterate
- VFX/CG Supervisor issues technical specs → Core Specialists implement

### Direction (Tier 4) → Support (Tier 3): Strategy + Policy
- Technical Director sets engineering strategy → Pipeline & Tools Engineering builds
- Producer sets budget/schedule → Production Management executes

### Core (Tier 1/2) ↔ Support (Tier 3): Data + Tools
- All Core Specialists → Pipeline & Tools Engineering: Tool requirements
- Pipeline & Tools Engineering → All Core Specialists: Pipeline tools, automation
- All Core Specialists → Production Management: Status updates, task completion
- Production Management → All Core Specialists: Task assignments, schedule

### Core (Tier 1/2) → Direction (Tier 4): Work for review
- Completed work flows to Creative Director for approval
- Quality evaluations flow to Braintrust for feedback signals

### Braintrust (Tier 4) → Direction (Tier 4): Feedback (only)
- Braintrust output flows ONLY to Creative Director
- Creative Director decides which feedback to act on
- Braintrust has NO direct connection to executing specialists

---

## Failure Mode Analysis for the Proposed Hierarchy

| Failure | Impact | Recovery |
|---------|--------|----------|
| DigitalModeler fails | Entire 3D pipeline stops | Pipeline & Tools Engineering builds alternative geometry path; use placeholders |
| LightingTD fails | Rendering and compositing stop | Use default lighting pass; accelerate lighting upon recovery |
| Pipeline & Tools Engineering fails | ALL departments lose tools | Tier 4 activates "Shotgun Under the Desk" recovery scripts (documented emergency tools) |
| Creative Director unavailable | No approvals; pipeline stalls | Delegate approval to VFX Supervisor for non-hero shots; Braintrust feedback continues independently |
| Surface & Material Artist fails | Materials use default values until recovery | Animators and Layout proceed with gray-shaded placeholders; lighting deferred |
| Production Management fails | No schedule or resource allocation | Producer (Tier 4) manually manages priority queue; task assignments deferred |

**Key improvement over flat 37-agent model:** The hierarchical structure limits failure cascades. A failure in Surface & Material Artist (Tier 2) does NOT affect Animator (Tier 1) or DigitalModeler (Tier 1). In the flat model, all 37 agents were peers — any failure could cascade unpredictably. In this model, Tier 1 bottleneck agents are isolated for maximum resilience, and Tier 2/3 agents can fail without stopping the critical path.

---

## Comparison: Flat 37-Agent Model vs. This 23-Specialist Hierarchy

| Dimension | Flat 37-Agent | Structured 23-Specialist |
|-----------|---------------|-------------------------|
| Agent count | 37-57 | 23 |
| Coordination overhead | O(n²) — each pair communicates | O(log n) — hierarchical routing |
| Bottleneck management | All agents are peers; bottlenecks invisible | Top 6 bottlenecks are Tier 1 with isolated failure domains |
| Knowledge sharing | Knowledge duplicated across agents | Shared knowledge merged into single specialists |
| Handoff overhead | Between every sequential capability | Eliminated for merged capabilities (M1-M9) |
| Failure cascades | Any agent failure affects all peers | Tier 1 failures stop production; Tier 2/3 failures are contained |
| Authority clarity | Unclear who can approve what | Clear: Director approves, Core executes, Support enables, Braintrust evaluates |
| Production type adaptation | One model for all productions | Tier 2 specialists adapt to film vs. game (Technical Artist vs. Surface & Material Artist) |

---

## Appendix: Decision Record — Key Controversial Merges Explained

### Why NOT merge Screenwriter (S02) with Narrative Designer (S03)?

Both work with story, but:
- **S02 knowledge:** Linear narrative craft (McKee principles, 3-act structure, dialogue, character arcs) — this is literary/writing craft.
- **S03 knowledge:** Interactive narrative implementation (branching trees, quest logic, game systems, player agency) — this is game design/systems craft.
- **Decision coupling:** A script change (S02) requires narrative designer updates (S03), but the reverse is not always true. They operate at different abstraction levels.
- **Verdict:** Keep separate. A merged specialist would be neither a great writer nor a great game systems designer.

### Why NOT merge Rigger (C05) with Creature TD (C09)?

They share anatomy knowledge, but:
- **C05 knowledge:** Skeleton creation, joint placement, control rigs, animation tools — primarily for animator use.
- **C09 knowledge:** Muscle simulation, flesh deformation, skin jiggle — primarily FX/simulation work.
- **Bottleneck analysis:** C05 is a top-7 bottleneck (non-redundant). C09 is not. Merging would make the rigging bottleneck even worse.
- **Decision coupling:** Weak — a rig change requires creature sim adjustment, but creature sim changes rarely require rig changes.
- **Verdict:** Keep separate. C09 is absorbed into Simulation & FX Artist (Tier 2.2). C05 stays independent (Tier 1.2).

### Why merge Pipeline TD (P04) with Software Engineer (P06) with Systems Engineer (P10)?

These three are distinct roles in a large studio, but for a COS agent hierarchy:
- **Shared infrastructure failure domain:** If any one fails, all production stops.
- **Same communication patterns:** All interact with the same department requests.
- **Modular internal structure:** The merged specialist has three internal modes — "Pipeline Tools," "Core Software," "Systems" — that can be independently scaled.
- **Real studio pattern:** Most studios organize engineering as a single department (Pipeline, R&D, Systems grouped under a CTO or Head of Technology).
- **Verdict:** Merge as "Pipeline & Tools Engineering" with three internal teams.

### Why is Braintrust (Q01) architecturally separate from all approving authorities?

Per research from Creative_Roles_as_Functions.md: *"The Braintrust is a FEEDBACK function that is architecturally SEPARATE from the APPROVAL function. This separation of concerns is the most transferable pattern from the research — it is what distinguishes constructive critique from command authority."*

The Braintrust specialist:
- Has ZERO authority to approve, reject, block, or mandate
- Can ONLY produce feedback signals
- Communicates ONLY with the Creative Director
- Operates under a Candor Contract that is explicitly maintained

This separation is mandatory — not optional. Any architecture that merges Braintrust with an approval function violates the core insight that makes Pixar's Braintrust effective.

---

*End of Specialist Hierarchy Document — 23 specialists across 4 tiers, with 8 strategic mergers reducing 37-57 flat agents to a structured, failure-isolated hierarchy.*
