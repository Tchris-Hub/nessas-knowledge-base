# COS v3: Capability-First Architecture

**Research Date:** June 15, 2026
**Status:** Draft
**Links:** [01_Capability_Architecture/COS_Architecture_v2.md](COS_Architecture_v2.md), [10_Assumptions/README.md](../10_Assumptions/README.md) (B2), [11_Decisions/Architecture_Changing_Discoveries.md](../11_Decisions/Architecture_Changing_Discoveries.md)

## Key Finding

The current COS architecture (v2) treats **specialists as the fundamental unit** — each specialist corresponds to ~3-5 capabilities, and adding a new domain means adding a new specialist.

This models a studio's org chart (humans as the unit).

The goal is not "recreate a Blender team" but "compress human expertise into a system."

These are different goals. They require different architectures.

## The Five Layers

| Layer | Definition | Scale | Example |
|-------|-----------|-------|---------|
| **Tool** | Software environment providing interface for creative manipulation | ~5-15 | Blender, Substance, Nuke, Unreal |
| **Action** | Atomic executable command on a tool. Single operator. | ~10k-50k | `bpy.ops.mesh.loopcut()`, "Set keyframe" |
| **Capability** | Meaningful transform: Input State → Output State. Has pre/post conditions. | ~1k-5k | "Retopologize quad mesh from high-poly sculpt" |
| **Skill** | Procedure chaining capabilities into reproducible outcome. The *how*. | ~2k-10k+ | "Hero weapon pipeline: blockout → game-ready" |
| **Specialist** | Bounded agent owning a domain. Decides which skill to apply. The *who*. | ~12-20 | "Rigging Specialist" |

## Proposed Hierarchy

```
Creative Domain [Film / Game-Art / Product Viz]
  ↓
  Specialist [12-20] — bounded agent, decision-maker
  ↓
  Capability Cluster [100-500] — shared across specialists
  ↓
  Capability [1,000-5,000] — the unit of coverage
  ↓
  Skill / Recipe [2,000-10,000+] — emerges from usage
  ↓
  Action [10,000-50,000+] — atomic executable
  ↓
  Tool [5-15] — software environment
  ↓
  Artifact
```

## Core Insight: Decouple Specialist Count from Capability Count

- **Specialist count** → optimize for **manageable handoff complexity.** N specialists = N×(N-1)/2 pairwise interactions. 23 specialists = 253 edges. 57 specialists = 1,596 edges. Keep 12-20.
- **Capability count** → optimize for **workflow coverage.** Does the system have the capability to produce the output? Maximize this. Target 1,000-5,000.

**These are independent variables.**

12 specialists covering 2,000 capabilities >> 57 specialists covering 500.

## Capability Estimates by Workflow

| Workflow | Capability Clusters | Capabilities | Key Domains |
|----------|-------------------|-------------|-------------|
| **Blender-only** | ~60 | ~750-1,200 | Modeling, Rigging, Animation, Shading, Lighting, Compositing, Rendering |
| **Animation** | ~85 | ~1,200-1,800 | Blender core + facial animation, lip-sync, body mechanics, acting/timing, mocap pipeline, crowd animation |
| **VFX** | ~110 | ~2,000-3,000 | Animation base + matchmove/tracking, deep compositing, pyro/fire, destruction, fluid integration, set extension, ACES |
| **Game-art** | ~95 | ~1,500-3,000 | Low-poly, PBR, real-time shaders, TA, environment art, game animation, platform optimization |
| **Film (Full Pipeline)** | ~130 | ~2,000-3,500 | Animation + VFX + production pipeline, dailies, render farm, DCP delivery |

## COS v2 Coverage Gap

Under the specialist-as-unit model, each specialist holds ~3-5 capabilities across ~1-2 clusters. With 23-57 specialists:

- **Estimated v2 coverage:** ~150-200 capabilities across ~30-40 clusters
- **Professional need:** ~2,000-3,500 capabilities across ~130 clusters (film)
- **Gap:** v2 covers ~5-8% of the professional capability space

**To reach full coverage under the v2 model, you'd need 200+ specialists with 1,596+ handoff pairs.** The system becomes coordination-bound before it becomes capable.

## Proposed v3: 15 Specialists, ~1,600-2,300 Capabilities

| # | Specialist | Capability Clusters | Capabilities | Key Clusters |
|---|-----------|-------------------|-------------|-------------|
| 1 | Modeling Specialist | ~8 | ~180-250 | Primitive, Hard Surface, Retopology, UV, Modifiers, Procedural, LOD |
| 2 | Character Specialist | ~9 | ~200-280 | Base Mesh, Sculpt, Retopology (deformation), Rigging, Blendshapes, Skin, Hair, Cloth |
| 3 | Rigging Specialist | ~8 | ~90-130 | Armature, FK/IK, Constraints, Weights, Drivers, Shape Keys, Rig Systems |
| 4 | Animation Specialist | ~7 | ~120-170 | Keyframing, Graph Editor, NLA, Motion, Body Mechanics, Acting |
| 5 | Shading Specialist | ~8 | ~120-160 | Core Shaders, Procedural Textures, PBR, Volumes, Painting |
| 6 | Lighting Specialist | ~6 | ~60-80 | Light Types, Techniques, Indirect, Volumetric, Light Groups |
| 7 | Cinematography Specialist | ~6 | ~60-80 | Camera Setup, Motion, Focus, Shot Design, Visual Hierarchy |
| 8 | Compositing Specialist | ~5 | ~70-100 | Render Layers, Color Grading, Keying, Blending, Deep Comp |
| 9 | FX Specialist | ~10 | ~150-250 | Particles, Rigid Bodies, Soft Bodies, Cloth, Fluids, Smoke, Destruction, Ocean, Hair, Volumes |
| 10 | Environment Specialist | ~8 | ~180-250 | Blockout, Hero Assets, Terrain, Foliage, Set Dressing, Atmosphere |
| 11 | Pipeline/Tech Specialist | ~6 | ~100-150 | Data Exchange, Asset Management, Scripting, Batch Processing |
| 12 | Game-Optimization Specialist | ~6 | ~100-150 | LOD, Draw Calls, Texture Budgeting, Shader Complexity, Memory |
| 13 | Real-Time Shader Specialist | ~6 | ~80-120 | Shader Graphs, Master Materials, Custom HLSL/GLSL, Post-Process |
| 14 | Audio Specialist | ~4 | ~40-60 | Sound Design, Foley, Dialogue Sync, Audio Editor |
| 15 | Production Management Specialist | ~5 | ~60-80 | Scheduling, Shot Tracking, Versioning, Dailies, Delivery |

**Total:** 15 specialists, 105 handoff pairs (vs 1,596 at 57), ~1,600-2,300 capabilities.

## Design Principles for v3

1. **Specialists are bounded agents, not people.** Don't give each specialist what one human would do. Give them what one cognitive domain contains.
2. **Capabilities are the optimization target.** Measure coverage, not headcount.
3. **Skills emerge from usage.** Architect capabilities deliberately. Let skills populate from how the specialist chains them.
4. **One specialist can own hundreds of capabilities.** A specialist's worth is how well it selects/sequences/quality-checks capabilities, not how many it has.
5. **Capability clusters are shared.** Specialists share clusters. Same capability in multiple clusters is intentional — different specialists access it differently.
6. **Capability registry, not specialist roster.** A single capability database with `{name, inputs, outputs, preconditions, postconditions, tool_actions[], specialist_owner, skill_references[]}`. Specialists reference capabilities — capabilities don't "belong" to specialists.

## Next Steps

- [ ] Validate estimates against real-world Blender/Film/Game pipelines
- [ ] Decompose top 5 capability clusters into capability-level detail
- [ ] Define handoff contracts between specialists (shared clusters)
- [ ] Prototype capability registry data model
- [ ] Build v0 capability set (~660 caps for launch)
