# Specialist Capability Domains

## Derived from Elite Production Studio Research

**Source Documents:** Pixar_Production_Pipeline, VFX_House_Pipeline, Game_Studio_Pipeline, Directors_Creative_Leadership, Story_Concept_Artists, Technical_Directors_Pipeline

**Purpose:** Map every specialist role across film, VFX, and game studio pipelines into cohesive capability domains for the Creative Operating System. Each capability describes what decisions it makes, what knowledge it requires, what inputs it consumes, what outputs it produces, and how it depends on other capabilities.

---

## DOMAIN 1: STORY DOMAIN

**Scope:** Narrative development, script creation, storyboarding, pitching, character narrative arcs, pacing, emotional structure.

### 1.1 Story Artist / Storyboard Artist

| Attribute | Description |
|-----------|-------------|
| **Name** | Story Artist |
| **Also Known As** | Storyboard Artist, Story Reel Artist (in live-action: Storyboard Artist; in animation: Story Artist) |
| **Core Responsibility** | Translate script/narrative into sequential visual panels (storyboards) that communicate story beats, character emotion, pacing, and visual clarity. |
| **Decisions It Makes** | Camera placement and angle per shot; staging and character blocking; shot-to-shot transitions; pacing (panel count per action); expression and body language choices; what to emphasize visually vs. leave implied; which emotional beats to amplify |
| **Knowledge It Requires** | Cinematic language (shot types, camera angles, transitions); narrative structure (3-act, Kishotenketsu); character expression and body language; timing and pacing intuition; staging and composition; acting fundamentals (to "perform" boards); script analysis |
| **Inputs Needed** | Script or outline; verbal direction from director; character designs and environment concepts; temporary music/dialogue for animatic |
| **Outputs Produced** | Storyboard panels (rough to clean); story reels/animatics (panels timed to audio); shot breakdowns; pitch presentations |
| **Dependencies** | Depends on: Screenwriter (script), Director (creative direction), Character/Environment Concept (visual reference). Provides inputs to: Layout, Animation, Editorial |

### 1.2 Screenwriter / Writer

| Attribute | Description |
|-----------|-------------|
| **Name** | Screenwriter |
| **Also Known As** | Writer, Scriptwriter, Staff Writer (TV) |
| **Core Responsibility** | Create the written narrative blueprint — dialogue, scene description, character arcs, and story structure. |
| **Decisions It Makes** | Story structure (acts, turning points, climax); character arcs and motivations; dialogue; scene content and ordering; thematic through-line; pacing at the script level |
| **Knowledge It Requires** | Dramatic structure (McKee principles: inciting incident, spine, crisis/climax, subtext); character development; dialogue craft; genre conventions; pacing; theme and subtext |
| **Inputs Needed** | Pitch/treatment; director creative vision; existing IP or adaptation source material; character bibles |
| **Outputs Produced** | Script (multiple drafts); treatment; story spine; character bibles; dialogue lists |
| **Dependencies** | Depends on: Director (vision), Producer (approval). Provides inputs to: Story Artist, Narrative Designer, Director |

### 1.3 Narrative Designer (Game)

| Attribute | Description |
|-----------|-------------|
| **Name** | Narrative Designer |
| **Core Responsibility** | Implement story through gameplay systems, dialogue trees, branching narratives, and quest logic. Translate script into interactive form. |
| **Decisions It Makes** | Branching narrative structure and consequences; dialogue tree design; quest logic and progression; how story is revealed through gameplay; narrative constraints on game systems; pacing of story beats within gameplay |
| **Knowledge It Requires** | Interactive storytelling (branching narrative, player agency, emergent narrative); game design fundamentals; scripting/lua; dialogue database management; quest design; player psychology |
| **Inputs Needed** | Script/story bible; game design document; character designs; gameplay systems documentation; level layouts |
| **Outputs Produced** | Dialogue trees and databases; quest logic scripts; branching narrative maps; interactive story implementation; cutscene scripts |
| **Dependencies** | Depends on: Writer (script), Game Designer (systems), Level Designer (spaces). Provides inputs to: Animator (cinematic), Audio Designer (dialogue), QA (testing) |

### 1.4 Visual Development Artist (Story-Facing)

| Attribute | Description |
|-----------|-------------|
| **Name** | Visual Development Artist |
| **Also Known As** | Vis Dev Artist (in animation); Concept Artist (in games/live-action — overlapping) |
| **Core Responsibility** | Establish the overall visual language, style, and world of a project early in pre-production. Work on overall visual system rather than specific asset design. |
| **Decisions It Makes** | Overall art direction and style; color philosophy and emotional palette; shape language of the world; style consistency across the project; mood and atmosphere of the entire piece |
| **Knowledge It Requires** | Color theory and color scripts; composition; visual storytelling; world-building; art history; style exploration; mood/atmosphere communication; shape language |
| **Inputs Needed** | Script or treatment; director creative brief; reference collection; genre/style guidelines |
| **Outputs Produced** | Mood paintings; color scripts; style guides; key art; world exploration sheets; color keys |
| **Dependencies** | Depends on: Director (vision), Screenwriter (script/narrative). Provides inputs to: Character Designer, Environment Concept Artist, Production Designer |

---

## DOMAIN 2: CHARACTER DOMAIN

**Scope:** Character design, sculpting, 3D modeling, rigging, surfacing/shading, texturing, grooming, creature setup.

### 2.1 Character Designer

| Attribute | Description |
|-----------|-------------|
| **Name** | Character Designer |
| **Core Responsibility** | Design the appearance, personality, and function of characters — silhouette, shape language, proportions, costume, color identity. |
| **Decisions It Makes** | Silhouette readability; shape language (round/friendly, sharp/dangerous, blocky/strong); proportion and scale; costume and equipment design; color identity and palette; personality expression through design; production constraints (can this be modeled/animated?) |
| **Knowledge It Requires** | Anatomy and proportion; silhouette design; shape language theory; color theory; costume/fashion design; character archetypes; personality encoding through visual design; 80/20 rule (80% reference, 20% original) |
| **Inputs Needed** | Character description/brief; director creative direction; visual development style guide; reference collection; narrative context (personality, backstory, role) |
| **Outputs Produced** | Full-body turnarounds; expression sheets (5-10 expressions); action pose sheets (3-6 poses); detail sheets (costume, equipment, weapons); color palette; orthographic views; callout sheets |
| **Dependencies** | Depends on: Director/Creative Director (vision), Vis Dev (style guide), Writer (character description). Provides inputs to: Sculptor, Digital Modeler, Texture Artist |

### 2.2 Sculptor (Physical Maquette)

| Attribute | Description |
|-----------|-------------|
| **Name** | Sculptor |
| **Core Responsibility** | Create physical clay maquettes of characters for 3D reference before digital modeling. |
| **Decisions It Makes** | Physical form and volume; proportion in 3D space; surface quality and texture reference; expression exploration in 3D |
| **Knowledge It Requires** | Traditional sculpting; anatomy; proportion; material properties (clay); understanding of downstream digital pipeline |
| **Inputs Needed** | Character design sheets; director feedback; reference materials |
| **Outputs Produced** | Physical clay maquettes; scanned 3D data (for seeding digital models) |
| **Dependencies** | Depends on: Character Designer (design). Provides inputs to: Digital Modeler (via scan) |

### 2.3 Character Artist (Game)

| Attribute | Description |
|-----------|-------------|
| **Name** | Character Artist |
| **Core Responsibility** | Create 3D character models and textures for interactive games — high-poly sculpts, retopology, UV mapping, texture baking, engine implementation. |
| **Decisions It Makes** | Polygon budget allocation; topology for deformation; UV layout; texture resolution priorities; LOD (level of detail) strategy; real-time shader/material selection |
| **Knowledge It Requires** | High-poly sculpting (ZBrush); retopology; UV mapping; PBR texturing (Substance Painter/Designer); game engine material systems; polycount optimization; real-time rendering constraints; human/creature anatomy |
| **Inputs Needed** | Character concept art; art style guide; technical specifications (polygon budget, texture sizes); engine requirements |
| **Outputs Produced** | High-poly sculpt; low-poly game model; UV maps; PBR texture sets (albedo, normal, roughness, metalness, AO); engine-ready character asset |
| **Dependencies** | Depends on: Character Designer (concept), Technical Artist (shader/performance). Provides inputs to: Rigger, Animator |

### 2.4 Digital Modeler

| Attribute | Description |
|-----------|-------------|
| **Name** | Digital Modeler |
| **Also Known As** | 3D Modeler, Poly Modeler, Character Modeler, Environment Modeler |
| **Core Responsibility** | Create virtual 3D wireframe geometry of characters, props, and environments using mathematical surface definitions. Build at multiple quality levels (high-res for final renders, medium for animation proxy, low for previs). |
| **Decisions It Makes** | Topology flow (edge loops for deformation); polygon distribution; NURBS vs. polygon vs. subdivision surfaces; level-of-detail strategy; hard surface vs. organic modeling approach; model efficiency vs. detail trade-off |
| **Knowledge It Requires** | 3D modeling (Maya, Blender, Houdini); topology and edge flow; subdivision surfaces; NURBS; hard surface and organic modeling; anatomy (for characters); spatial reasoning; UV mapping basics |
| **Inputs Needed** | Concept art or design sheets; sculpted maquette or scan data; technical specifications; reference photography |
| **Outputs Produced** | 3D wireframe models (high, medium, low resolution); organized geometry with proper topology; clean geometry for downstream departments |
| **Dependencies** | Depends on: Character Designer/Concept Artist (reference), Sculptor/Scan TD (3D reference). Provides inputs to: Rigger, Texture Artist, Lookdev |

### 2.5 Rigger / Rigging TD

| Attribute | Description |
|-----------|-------------|
| **Name** | Rigger / Rigging TD |
| **Core Responsibility** | Build digital skeletons, joint systems, muscle deformations, and control rigs. Create the technical interface between modeling and animation. |
| **Decisions It Makes** | Skeleton hierarchy and joint placement; deformation system design (skin weighting, blend shapes, muscle systems); control rig design (what animators can manipulate); facial rig architecture; constraint system design; how the rig responds to extreme poses; performance vs. fidelity trade-offs |
| **Knowledge It Requires** | Anatomy and kinesiology; joint/deformation mathematics; skin weighting; blend shapes; constraint systems; character mechanical design; Maya/Houdini rigging toolsets; Python scripting for rig automation; animation principles (to design rigs animators love) |
| **Inputs Needed** | Clean 3D model with proper topology; character design sheets (poses, expressions); animation requirements (range of motion, special needs); technical specifications |
| **Outputs Produced** | Animation-ready rig (skeleton, controls, deformers); facial rig; muscle/simulation systems; rig documentation; test animations |
| **Dependencies** | Depends on: Digital Modeler (geometry). Provides inputs to: Animator, Animation TD |

### 2.6 Texture Artist

| Attribute | Description |
|-----------|-------------|
| **Name** | Texture Artist |
| **Core Responsibility** | Create 2D surface detail maps (diffuse color, specular, roughness, bump, displacement, ambient occlusion) that define the look of 3D model surfaces. |
| **Decisions It Makes** | Texture resolution allocation (hero vs. background); map type priorities; UV space utilization; color palette and variation; wear/aging/weathering patterns; procedural vs. hand-painted approach; tileable vs. unique textures |
| **Knowledge It Requires** | Digital painting (Photoshop, Mari, Substance Painter); PBR material theory; UV mapping; color theory; material properties (metal, fabric, skin, stone); photorealistic painting techniques; procedural texturing (Substance Designer) |
| **Inputs Needed** | 3D model with clean UVs; concept art/color keys; on-set reference photos (film); material specs from lookdev; texture resolution/format requirements |
| **Outputs Produced** | Texture maps (diffuse, specular, roughness, normal, displacement, AO, etc.) at appropriate resolutions (2K-8K+); substance files; layered source files |
| **Dependencies** | Depends on: Digital Modeler (UVs), Lookdev Artist (material specs), Concept Art (reference). Provides inputs to: Lookdev Artist, Shading TD |

### 2.7 Shading TD / Surfacing TD

| Attribute | Description |
|-----------|-------------|
| **Name** | Shading TD / Surfacing TD |
| **Core Responsibility** | Develop the final surface appearance of 3D models — color, texture, roughness, transparency, subsurface scattering, clearcoat. Combine texture maps with shader networks. |
| **Decisions It Makes** | Shader network architecture; material layering (layered shaders); renderer-specific shader setup (RenderMan, Arnold, V-Ray); subsurface scattering parameters; anisotropy and clearcoat settings; surface response to different lighting conditions |
| **Knowledge It Requires** | Shader theory and implementation; renderer-specific shading languages (OSL, VEX, C++ for custom shaders); PBR materials; light transport physics; material layering; tools: Katana, Houdini, Maya, RenderMan, Arnold |
| **Inputs Needed** | 3D model; texture maps from Texture Artist; lookdev reference/target images; lighting environment for testing; renderer specs |
| **Outputs Produced** | Shader networks/setups; shaded lookdev renders; material definitions; shader documentation |
| **Dependencies** | Depends on: Texture Artist (maps), Digital Modeler (geometry), Lighting TD (for lookdev lighting). Provides inputs to: Lookdev Artist, Lighting TD, Rendering TD |

### 2.8 Grooming TD

| Attribute | Description |
|-----------|-------------|
| **Name** | Grooming TD |
| **Core Responsibility** | Develop fur/hair simulation workflows and create groom assets (fur, hair, feathers) for characters. |
| **Decisions It Makes** | Groom guide placement and density; hair/fur type and behavior; interpolation strategies for varying LOD; cache management; groom style and silhouette; simulation parameters |
| **Knowledge It Requires** | Grooming tools (XGen, Yeti, Houdini grooming tools, proprietary like Weta's Barbership); hair/fur physics; simulation systems; stylized hair sculpting; guide curve manipulation |
| **Inputs Needed** | Character model; concept art (hair/fur reference); simulation requirements; render budget for hair |
| **Outputs Produced** | Groom guides; hair/fur simulation setups; groom caches; LOD versions |
| **Dependencies** | Depends on: Digital Modeler (base mesh), Simulation TD (physics setup). Provides inputs to: Lookdev Artist, Lighting TD |

### 2.9 Creature TD

| Attribute | Description |
|-----------|-------------|
| **Name** | Creature TD |
| **Core Responsibility** | Hybrid rigging/FX role building complex creature setups — muscle, flesh, skin simulation systems for realistic creature movement. |
| **Decisions It Makes** | Muscle simulation approach (FEM, spring-based, pose-driven); skin/flesh deformation system; fat jiggle simulation; secondary motion systems; creature locomotion constraints |
| **Knowledge It Requires** | Anatomy (comparative); biomechanics; FEM simulation; soft body dynamics; rigging; muscle/skin deformation; Houdini, Maya |
| **Inputs Needed** | Creature model and rig; animation requirements; reference footage; simulation specs |
| **Outputs Produced** | Muscle/flesh/skin simulation setups; creature deformation systems; secondary motion rigs |
| **Dependencies** | Depends on: Rigger (skeleton), Digital Modeler (geometry). Provides inputs to: Animator, Simulation TD |

---

## DOMAIN 3: VISUAL DOMAIN

**Scope:** Concept art (environments), production design, layout/cinematography, lighting, look development, matte painting, VFX/effects, environment modeling.

### 3.1 Environment Concept Artist

| Attribute | Description |
|-----------|-------------|
| **Name** | Environment Concept Artist |
| **Also Known As** | Environment Designer, World Concept Artist |
| **Core Responsibility** | Design locations, worlds, architecture, and atmosphere. Solve visual problems: "What does this world look like? What is its mood, scale, and history?" |
| **Decisions It Makes** | Scale and atmosphere of spaces; lighting direction and quality; architecture style and cultural/technological level; terrain and flora composition; color palette and mood; focal points and visual hierarchy; narrative context (what happened here?); day/night variations |
| **Knowledge It Requires** | Architecture and architectural history; landscape design; lighting theory; color theory; composition; world-building logic; cultural/technological level design; perspective and spatial reasoning; mood/atmosphere communication |
| **Inputs Needed** | Script or brief; director/world-building guidelines; reference collection; visual development style guide; time period/genre constraints |
| **Outputs Produced** | Mood paintings; area overviews (bird's-eye, 3/4 view); focal point studies; material/lighting references; annotated architectural breakdowns; key moments (day/night, weather variants) |
| **Dependencies** | Depends on: Director/Creative Director (vision), Vis Dev (style/color guide). Provides inputs to: Environment Artist/Modeler, Matte Painter, Layout Artist, Lighting Artist |

### 3.2 Production Designer

| Attribute | Description |
|-----------|-------------|
| **Name** | Production Designer |
| **Core Responsibility** | Oversee the entire visual look of the film or project. Coordinate between all art departments — sets, costumes, props, color palette, visual consistency. |
| **Decisions It Makes** | Overall visual aesthetic and consistency across all departments; color palette for entire production; set design direction; prop and costume style; visual tone and mood standards; department coordination priorities |
| **Knowledge It Requires** | Architecture and interior design; art history; color theory; visual storytelling; set design; costume design; prop making; cross-departmental coordination; budget management for art departments |
| **Inputs Needed** | Script breakdown; director creative vision; visual development materials; budget and schedule constraints |
| **Outputs Produced** | Production design bible; set designs and elevations; color palettes; prop and costume direction; visual consistency documentation |
| **Dependencies** | Depends on: Director (vision), Vis Dev (initial style). Provides inputs to: Environment Artist, Set Designer, Prop Designer, Costume Designer, Lighting Director/DP |

### 3.3 Environment Artist (Game/Modeling)

| Attribute | Description |
|-----------|-------------|
| **Name** | Environment Artist |
| **Core Responsibility** | Create 3D environments for games — terrain, buildings, props, vegetation — optimized for real-time rendering and game interaction. |
| **Decisions It Makes** | Modular kit design (reusable asset pieces); terrain sculpting and material blending; prop placement and distribution; optimization (polygon budget, draw calls); LOD strategy; material and shader selection for environment surfaces |
| **Knowledge It Requires** | 3D modeling (Maya, Blender); material creation (Substance Designer/Painter); engine-level assembly (Unreal, Unity, proprietary); terrain tools; modular level design; real-time optimization; lighting fundamentals |
| **Inputs Needed** | Environment concept art; level layout/blockmesh; technical specs (polygon budget, texture memory); engine requirements |
| **Outputs Produced** | 3D environment meshes; modular kit pieces; terrain materials and textures; engine-ready environment levels; lighting and post-processing setups |
| **Dependencies** | Depends on: Environment Concept Artist (reference), Level Designer (layout). Provides inputs to: Lighting Artist, VFX Artist (context), Level Designer |

### 3.4 Layout Artist

| Attribute | Description |
|-----------|-------------|
| **Name** | Layout Artist |
| **Also Known As** | Sets and Camera Artist, Set Staging Artist (Pixar); Previz Artist (VFX) |
| **Core Responsibility** | Establish virtual camera placement, framing, composition, and blocking for each shot. Translate storyboards into 3D scenes. Determine cinematography — perspective, depth, scale, camera movement. |
| **Decisions It Makes** | Camera placement and movement per shot; lens selection (focal length, depth of field); framing and composition; blocking of characters in 3D space; spatial relationships between elements; scale of environments vs. characters; 3D vs. 2.5D/cheat decisions; shot-to-shot spatial continuity |
| **Knowledge It Requires** | Cinematography (camera angles, lens choice, composition); spatial reasoning; blocking and staging; storytelling through camera; continuity editing; 3D scene assembly; Maya, Houdini, Unreal Engine; Previs tools |
| **Inputs Needed** | Storyboards or animatics; character and environment models; camera specs and constraints; director notes on shot intent |
| **Outputs Produced** | 3D layout scenes with camera placement; camera animation; scene-blocking setups; previz animations; shot framing references for downstream departments |
| **Dependencies** | Depends on: Story Artist (boards), Digital Modeler (assets), Director (shot intent), Matchmove Artist (camera data for VFX). Provides inputs to: Animator, Lighting TD, FX TD |

### 3.5 Lighting TD / Lighting Artist

| Attribute | Description |
|-----------|-------------|
| **Name** | Lighting TD / Lighting Artist |
| **Core Responsibility** | Place and configure virtual lights; balance illumination across shots; enhance mood, believability, and storytelling through light. In VFX: match CG lighting to live-action plates. |
| **Decisions It Makes** | Lighting direction, quality (hard/soft), and color temperature; key/fill/rim light placement; exposure and contrast; mood and emotional tone via light; shadow behavior (density, softness, color); render sampling and noise management; render budget allocation (samples for different light types); image-based lighting from HDR environments |
| **Knowledge It Requires** | Lighting theory (3-point, practical, motivated, artistic); color temperature and light physics; renderer-specific lighting (RenderMan, Arnold, V-Ray, Katana); HDR image-based lighting; exposure and color grading; shadow theory; mood/atmosphere communication; DCC lighting tools |
| **Inputs Needed** | Layout scene/camera setup; shaded models and environments; HDR environment maps (from on-set capture for VFX); reference photography; director/DP lighting references; render specs and budgets |
| **Outputs Produced** | Lit shots; render layers/AOVs (diffuse, specular, SSS, emission, z-depth, motion vectors); lighting templates; lighting reference documentation; render optimization passes |
| **Dependencies** | Depends on: Layout Artist (camera/scene), Shading TD (materials), FX Artist (simulation validation). Provides inputs to: Rendering TD, Compositor (via AOVs) |

### 3.6 Matte Painter

| Attribute | Description |
|-----------|-------------|
| **Name** | Matte Painter |
| **Core Responsibility** | Create photorealistic digital backdrops and environments where full 3D set construction isn't necessary. Projected onto simple geometry for parallax. |
| **Decisions It Makes** | Where to use 2D projection vs. full 3D; perspective and camera match; lighting and atmosphere integration with plate; level of detail vs. camera distance; color and grain match with footage |
| **Knowledge It Requires** | Photorealistic digital painting; perspective and projection mapping; photography (lens characteristics, grain, exposure); color grading; compositing basics; Nuke, Photoshop |
| **Inputs Needed** | Plate photography or 3D render; camera matchmove data; lighting reference; environment concept art |
| **Outputs Produced** | Matte paintings (2D environment projections); projected environment setups; camera-mapped 3D geometry |
| **Dependencies** | Depends on: Matchmove Artist (camera data), Environment Concept (reference). Provides inputs to: Compositor |

### 3.7 FX Artist / VFX Artist (Simulation)

| Attribute | Description |
|-----------|-------------|
| **Name** | FX Artist / VFX Artist / Effects Artist |
| **Also Known As** | Simulation Artist, FX TD |
| **Core Responsibility** | Create physically believable dynamic effects — fire, smoke, water, explosions, cloth, destruction, particles, magic. Art-directed physics for visual impact. |
| **Decisions It Makes** | Simulation approach (particles, rigid-body, fluids); simulation resolution vs. quality trade-off; art direction of physics (silhouette, timing, readability); caching and iteration strategy; shot-to-shot consistency; render budget for FX passes |
| **Knowledge It Requires** | Physics simulation (fluids, rigid bodies, particles, cloth); Houdini (industry standard); art-directed physics; particle systems; fluid dynamics; destruction mechanics; caching and file management; render optimization for FX passes; Python/VEX scripting |
| **Inputs Needed** | Animated scene/shots requiring FX; reference footage; simulation specs; render budget and output requirements; art direction/feedback |
| **Outputs Produced** | Simulation caches; particle systems; fluid simulations; destruction sequences; environmental effects; FX render layers/AOVs |
| **Dependencies** | Depends on: Animator (animated assets for FX interaction), Layout Artist (scene context). Provides inputs to: Lighting TD (lighting integration), Compositor |

### 3.8 Look Development Artist (Lookdev)

| Attribute | Description |
|-----------|-------------|
| **Name** | Look Development Artist |
| **Also Known As** | Lookdev Artist |
| **Core Responsibility** | Combine texture maps with shaders and reference lighting to define final material properties — shininess, reflectivity, subsurface scatter, anisotropy, clearcoat. Create the definitive "look" of a material or asset. |
| **Decisions It Makes** | Material properties (shininess, reflectivity, roughness, SSS depth/color, anisotropy); shader network architecture; lighting setup for hero lookdev renders; material variation and aging; interaction between material and light types |
| **Knowledge It Requires** | PBR theory (energy conservation, microfacet models); light transport physics; renderer-specific shader architecture; Maya, Katana, Houdini; material layering; color theory; photographic reference analysis |
| **Inputs Needed** | 3D model with UVs; texture maps from Texture Artist; lighting environment (HDR or studio setup); reference photography of real materials; renderer specs |
| **Outputs Produced** | Finalized lookdev renders; shader definitions; material library entries; lookdev reference for lighting and comp |
| **Dependencies** | Depends on: Texture Artist (maps), Shading TD (shader framework), Lighting TD (lighting for review). Provides inputs to: Lighting TD, Compositor |

---

## DOMAIN 4: ANIMATION DOMAIN

**Scope:** Character animation (keyframe and motion capture), performance, motion, physics simulation, matchmoving.

### 4.1 Animator

| Attribute | Description |
|-----------|-------------|
| **Name** | Animator |
| **Also Known As** | Character Animator (film); Gameplay Animator, Cinematic Animator (game) |
| **Core Responsibility** | Bring characters to life through movement and expression. Create performance through keyframe animation. In games: create responsive, blendable, reactive animation systems. |
| **Decisions It Makes** | Performance choices (how a character moves, reacts, expresses emotion); timing and spacing of motion; pose strength and silhouette readability; weight, balance, and physicality; facial expression and lip-sync; in games: animation states, blend trees, transition logic, additive/animation layering |
| **Knowledge It Requires** | 12 Principles of Animation (squash/stretch, anticipation, staging, follow-through, timing, exaggeration, etc.); acting and performance; body mechanics and motion; facial expression and emotion; body language; film: keyframe animation (Maya, Presto); games: animation state machines, blend trees (Unreal, proprietary engines); motion blur understanding |
| **Inputs Needed** | Rigged character (with controls); layout scene and camera; storyboard or performance reference; audio (dialogue track for lip-sync); director notes on performance intent; game: animation state machine specs |
| **Outputs Produced** | Animated shots/sequences; animation curves and keyframes; game: animation clips, state machines, blend spaces, additive animation layers; playblasts for review; final animation data |
| **Dependencies** | Depends on: Rigger (functional rig), Layout Artist (camera/scene), Director (performance direction). Provides inputs to: FX Artist (simulation input), Lighting TD, Compositor |

### 4.2 Animation TD

| Attribute | Description |
|-----------|-------------|
| **Name** | Animation TD |
| **Core Responsibility** | Build animation tools, scripts, and workflows to support animators. Troubleshoot technical issues; solve DCC performance problems; develop constraints, pickers, automation scripts. |
| **Decisions It Makes** | Tool design for animator workflows; automation of repetitive tasks; performance optimization strategies; constraint and picker system architecture; scripted animation assists |
| **Knowledge It Requires** | Deep DCC knowledge (Maya, Presto, MotionBuilder); Python/C++ scripting; animation principles (to build useful tools); constraint and deformation math; UI/UX for creative tools |
| **Inputs Needed** | Animator workflow pain points; rigs that need support; tool requests from animation team; production schedule for tooling priorities |
| **Outputs Produced** | Animation tools and scripts; picker UIs; automation scripts; constraint systems; performance optimizations |
| **Dependencies** | Depends on: Animator (requirements), Rigger (rigs). Provides inputs to: Animator (tools), Pipeline TD (integration) |

### 4.3 Matchmove Artist / Camera Tracker

| Attribute | Description |
|-----------|-------------|
| **Name** | Matchmove Artist |
| **Also Known As** | Camera Tracker, 3D Tracker, Body Tracker, Tracking Artist |
| **Core Responsibility** | Match CG scenes to live-action footage by recreating camera movement, lens distortion, and object motion in 3D space. |
| **Decisions It Makes** | Tracking point selection and quality; solve method selection (auto vs. manual); lens distortion model; coordinate system and scale; body/object tracking accuracy tolerance; which shots need matchmove vs. simpler approach |
| **Knowledge It Requires** | Camera optics (focal length, distortion, sensor size); 3D tracking mathematics; photogrammetry; 3D space and coordinate systems; body mechanics (for body tracking); tools: 3DEqualizer, PFTrack, Boujou, Syntheyes, Maya |
| **Inputs Needed** | Live-action plates; lens metadata (focal length, distortion profile, sensor specs); on-set measurements; tracking markers reference |
| **Outputs Produced** | Solved camera with motion data; animated tracking nulls; body/object tracking data; lens distortion information; 3D scene with tracked camera |
| **Dependencies** | Depends on: Editorial (plates), On-Set Data (lens metadata). Provides inputs to: Layout Artist, Animator, Compositor |

### 4.4 Motion Capture TD

| Attribute | Description |
|-----------|-------------|
| **Name** | Motion Capture TD |
| **Core Responsibility** | Process motion capture data; manage solve quality, retargeting, cleanup, and pipeline integration of performance capture data. |
| **Decisions It Makes** | Solve quality standards; retargeting approach (skeleton mapping); cleanup/denoising strategies; performance vs. cleanup time trade-off; integration with keyframe animation workflow |
| **Knowledge It Requires** | Motion capture hardware (Vicon, OptiTrack, Faceware); solve algorithms; retargeting mathematics; skeleton hierarchies; animation fundamentals; cleanup tools (MotionBuilder, custom); Python scripting |
| **Inputs Needed** | Raw mocap data from stage; actor skeleton definition; target rig skeleton; reference video takes |
| **Outputs Produced** | Cleaned mocap data; retargeted animation to target rig; face capture solves; performance capture integration |
| **Dependencies** | Depends on: On-Set Capture Team. Provides inputs to: Animator (base motion), Rigger (retarget specs) |

### 4.5 Simulation TD

| Attribute | Description |
|-----------|-------------|
| **Name** | Simulation TD |
| **Also Known As** | FX TD (overlapping) |
| **Core Responsibility** | Create and manage physics-based simulation systems for cloth, hair, fur, water, fire, smoke, destruction, and crowds. Write and run simulation software. |
| **Decisions It Makes** | Simulation approach (position-based dynamics, FEM, SPH, grid-based); resolution and quality budget; caching strategies; iteration methodology (wedge tests for param sweeps); collision handling; art-directed physics parameters |
| **Knowledge It Requires** | Physics simulation (rigid bodies, soft bodies, fluids, cloth, hair); numerical methods; Houdini (VEX, Python, HDK); cache management; render farm submission for simulation; code performance optimization (C++, Python) |
| **Inputs Needed** | Animated assets requiring simulation; reference footage; physics parameters (density, stiffness, friction, etc.); render budget; farm resources |
| **Outputs Produced** | Simulation caches (simulated cloth/hair/water/etc.); simulation setups (reproducible); wedge test results; optimized simulation parameters |
| **Dependencies** | Depends on: Animator (animated base), Modeler (sim-ready geometry). Provides inputs to: Lighting TD, Compositor |

---

## DOMAIN 5: DIRECTION DOMAIN

**Scope:** Creative vision, authority decisions, feedback giving, quality setting, team leadership, translation of intent to execution.

### 5.1 Film Director

| Attribute | Description |
|-----------|-------------|
| **Name** | Film Director |
| **Also Known As** | Director |
| **Core Responsibility** | Ultimate creative authority on the project. Owns the creative vision, story, performance, visual composition, and pacing. Makes final creative decisions on all aspects. |
| **Decisions It Makes** | Final say on all creative decisions: story direction, character design, shot composition, animation performance, lighting, tone, pacing; which ideas move forward; casting and key creative hires; what to protect vs. compromise; shot finaling (approval to move forward) |
| **Knowledge It Requires** | Story structure (McKee principles); performance direction; cinematography; visual composition; editing/pacing; working knowledge of all departments; actor communication vocabulary; creative compromise calculus |
| **Inputs Needed** | Script; production schedule and budget; department heads' proposals; dailies reviews (shots looking for approval); Braintrust/peer feedback |
| **Outputs Produced** | Creative vision and direction; approved/ finalled shots; notes and feedback to all departments; look books, tone packets; final cut of the film |
| **Dependencies** | Depends on: Screenwriter (script), Producers (budget/schedule), Department Leads (execution). Provides inputs to: ALL departments (direction) |

### 5.2 CCO / Chief Creative Officer

| Attribute | Description |
|-----------|-------------|
| **Name** | Chief Creative Officer (CCO) |
| **Core Responsibility** | Set overall creative vision for the studio. Approve which projects/films move forward. Ensure studio-wide creative quality and coherence across multiple productions. |
| **Decisions It Makes** | Which films/projects are greenlit; studio-wide creative direction; allocation of creative resources across projects; when a project is ready for production; high-level quality bar for the studio |
| **Knowledge It Requires** | Deep creative judgment across all disciplines; understanding of market and audience; strategic portfolio management; talent evaluation; production process understanding |
| **Inputs Needed** | Project pitches; production status reports; department head recommendations; studio performance data |
| **Outputs Produced** | Greenlight decisions; studio creative strategy; project prioritization; creative standards guidance |
| **Dependencies** | Depends on: Director (project vision), Producers (project feasibility). Provides inputs to: Directors, Studio Leadership |

### 5.3 Game Director

| Attribute | Description |
|-----------|-------------|
| **Name** | Game Director |
| **Core Responsibility** | Own creative vision and design decision-making for a game project. Focus on WHY and WHAT — why should we do this, what are we building. Has final say on gameplay, story, tone, features. |
| **Decisions It Makes** | Core gameplay loop and mechanics; feature set and scope; game feel and interaction design; narrative direction; tone and emotional identity; milestone content and quality; what gets cut when time runs out |
| **Knowledge It Requires** | Game design and mechanics; player psychology; production pipeline management; cross-discipline leadership; scope management; iterative design processes; team synchronization |
| **Inputs Needed** | Game design documents; prototype feedback and playtest results; milestone deliverables; team capacity and velocity data; technical feasibility reports |
| **Outputs Produced** | Creative vision and direction; feature decisions; scope decisions; milestone targets; design documentation; feedback on all game systems |
| **Dependencies** | Depends on: Game Designer (systems design), Technical Director (feasibility), Producer (schedule). Provides inputs to: All disciplines (Art, Design, Engineering, Animation) |

### 5.4 Creative Director (Game)

| Attribute | Description |
|-----------|-------------|
| **Name** | Creative Director |
| **Core Responsibility** | Oversee narrative, art direction, and tonal consistency. Shape the emotional identity of the game — feel, look, expression. "One owns the heart. One owns the spine." |
| **Decisions It Makes** | Story direction and narrative tone; visual style and art direction; character identity and thematic consistency; emotional world-building; how story and mechanics align |
| **Knowledge It Requires** | Narrative craft; visual arts; game design understanding; cross-discipline collaboration; thematic consistency; tone management |
| **Inputs Needed** | Game design direction; concept art and vis dev; narrative scripts; gameplay prototypes |
| **Outputs Produced** | Creative vision; tonal and narrative direction; art style guidelines; feedback on story/art/audio |
| **Dependencies** | Depends on: Game Director (shared vision), Writer (narrative), Art Director (visuals). Provides inputs to: Art, Narrative Design, Animation, Audio |

### 5.5 Showrunner (TV)

| Attribute | Description |
|-----------|-------------|
| **Name** | Showrunner |
| **Also Known As** | Executive Producer / Head Writer (TV) |
| **Core Responsibility** | Top-level creative and management authority for a television series. Manage the writers' room, oversee all episodes, navigate network relations, sustain quality across seasons. |
| **Decisions It Makes** | Multi-season narrative arc and coherence; episode-level story decisions; writer assignments; which notes to accept from network; budget allocation per episode; tone consistency across episodes/seasons; casting and key creative hires |
| **Knowledge It Requires** | Story structure (long-form serialization); writers' room management; budget/production management; network politics; episodic pacing; multi-season arc planning; the "soul" of the series |
| **Inputs Needed** | Scripts from writers' room; network notes; production status; editor's cuts; episode performances; budget reports |
| **Outputs Produced** | Series vision and arc; episode outlines and scripts; creative notes; final episode approval; season plan |
| **Dependencies** | Depends on: Writers (scripts), Episodic Directors (execution), Producers (budget). Provides inputs to: Writers, Directors, Post-Production |

### 5.6 VFX Supervisor

| Attribute | Description |
|-----------|-------------|
| **Name** | VFX Supervisor |
| **Also Known As** | On-Set VFX Supervisor, Overall VFX Supervisor |
| **Core Responsibility** | Achieve the creative aims of the director/producers through visual effects. Central bridge between creative intent and technical execution. Make final creative calls on VFX look, quality, and shot approval. |
| **Decisions It Makes** | Which VFX technique to use (practical vs. digital); final approval on VFX shots before client delivery; how to translate director's creative notes into technical instructions; on-set: camera placement, greenscreen, lighting for VFX; which shots are ready for client review; VFX budget and scope |
| **Knowledge It Requires** | Full VFX pipeline knowledge; cinematography and photography; directing; practical and digital VFX techniques; client management; bidding and negotiation; on-set protocol and safety; 10+ years production experience |
| **Inputs Needed** | Film director's vision; script breakdown; plates and on-set data; department lead proposals; client notes; production schedule and budget |
| **Outputs Produced** | Creative direction for all VFX departments; shot approvals/rejections; client-facing shot presentations; translated creative notes into technical specs; on-set guidance |
| **Dependencies** | Depends on: Director (overall vision), Producer (budget/schedule), CG Supervisor (technical execution). Provides inputs to: All VFX departments |

### 5.7 CG Supervisor

| Attribute | Description |
|-----------|-------------|
| **Name** | CG Supervisor |
| **Also Known As** | Computer Graphics Supervisor, VFX CG Supervisor |
| **Core Responsibility** | Ultimate responsibility for delivery and quality of all 3D CG elements. Design the pipeline, manage TDs, oversee all 3D departments. Bridge between creative intent and technical execution. |
| **Decisions It Makes** | Which software/pipeline to use; how assets flow between departments; technical standards (polygon budgets, texture resolution, naming conventions); tool development priorities with Pipeline TDs; hiring for CG departments; technical approach to CG problems |
| **Knowledge It Requires** | Expert knowledge of full 3D pipeline (modeling, lookdev, FX, lighting, animation, compositing); Python/C++ programming; leadership and personnel management; Linux/Unix; pipeline architecture; cross-departmental workflow |
| **Inputs Needed** | Creative direction from VFX Supervisor; artist capacity and skill data; tool performance metrics; production schedule and milestones; R&D output |
| **Outputs Produced** | Pipeline technical standards; tool development priorities; department assignments; CG quality bar; technical feasibility assessments |
| **Dependencies** | Depends on: VFX Supervisor (creative direction), Pipeline TDs (infrastructure). Provides inputs to: All 3D departments (Modeling, Rigging, FX, Lighting, Lookdev) |

### 5.8 Compositing Supervisor

| Attribute | Description |
|-----------|-------------|
| **Name** | Compositing Supervisor |
| **Core Responsibility** | Lead the compositing team. Ensure final image quality — seamless integration of all CG elements with live-action plates. Approve comps before VFX Sup review. |
| **Decisions It Makes** | Whether a comp is done and ready for VFX Sup; comp workflow and approach; AOV usage and light integration strategy; team task assignments; comp quality standards |
| **Knowledge It Requires** | Deep compositing (Nuke); color theory and grading; cinematography; light integration; creative eye for realism; team leadership; production workflow |
| **Inputs Needed** | Rendered AOVs from Lighting; plates from editorial; reference footage; VFX supervisor direction |
| **Outputs Produced** | Final shot composites; comp team assignments; comp quality reviews; feedback to lighting/FX |
| **Dependencies** | Depends on: VFX Supervisor (direction), Lighting TD (AOVs), Compositor (execution). Provides inputs to: Client/VFX Supervisor (final review) |

### 5.9 Art Director

| Attribute | Description |
|-----------|-------------|
| **Name** | Art Director |
| **Core Responsibility** | Define and maintain visual identity, style guide adherence, and art quality bar across the project. Ensure visual consistency across all art assets. |
| **Decisions It Makes** | Art style adherence and consistency; quality bar for all art output; art direction deviations and creative exceptions; team execution alignment with visual vision; style guide updates |
| **Knowledge It Requires** | Visual arts (painting, sculpture, design); art history; color theory; composition; lighting; all art discipline pipelines; team leadership; production constraints awareness |
| **Inputs Needed** | Creative director/director vision; concept art and vis dev; art team output for review; production schedules and resources |
| **Outputs Produced** | Art direction guidelines; style guide enforcement; art quality bar; feedback to all art disciplines |
| **Dependencies** | Depends on: Director/Creative Director (vision). Provides inputs to: All art disciplines (Character, Environment, VFX, UI) |

### 5.10 Technical Director / Engineering Director (Game)

| Attribute | Description |
|-----------|-------------|
| **Name** | Technical Director / Engineering Director |
| **Core Responsibility** | Own technical feasibility, architecture decisions, and engineering strategy for the project. Determine what is technically possible within constraints. |
| **Decisions It Makes** | Engine and technology choices; architectural approach to game systems; performance targets and budgets; technical feasibility of features; tool and pipeline engineering priorities; code quality and engineering standards |
| **Knowledge It Requires** | Game engine architecture (custom, Unreal, Unity); programming (C++, C#, systems programming); rendering pipelines; performance optimization; build systems; team leadership; cross-discipline technical communication |
| **Inputs Needed** | Game design requirements; performance targets; team capacity; technical constraints (platform, hardware) |
| **Outputs Produced** | Technical architecture; engine/tech decisions; performance budgets; feasibility assessments; engineering roadmap |
| **Dependencies** | Depends on: Game Director (design vision), Producer (schedule). Provides inputs to: Engineering teams, Technical Artists |

### 5.11 Animation Supervisor

| Attribute | Description |
|-----------|-------------|
| **Name** | Animation Supervisor |
| **Core Responsibility** | Lead the animation team. Ensure animation quality, performance consistency, and creative direction alignment. Translate director's performance vision into animation execution. |
| **Decisions It Makes** | Animation quality bar and style; team assignments; performance direction interpretation; shot approval within animation; animation pipeline decisions |
| **Knowledge It Requires** | Animation principles and acting; performance direction; team leadership; animation pipeline; character performance critique |
| **Inputs Needed** | Director performance direction; rigged characters; layout scenes; animator capacity |
| **Outputs Produced** | Animation quality reviews; team direction; approved animation shots; feedback to animators |
| **Dependencies** | Depends on: Director (performance vision), Rigger (functional rigs). Provides inputs to: Animators, FX (simulation input) |

---

## DOMAIN 6: QUALITY DOMAIN

**Scope:** Review, critique, standards enforcement, braintrust evaluation, quality gatekeeping, postmortems.

### 6.1 Braintrust (Pixar)

| Attribute | Description |
|-----------|-------------|
| **Name** | Braintrust |
| **Also Known As** | Story Trust (Pixar) |
| **Core Responsibility** | Provide candid, high-level creative feedback on films in production. Group of senior creatives (directors, writers, heads of story) who review work-in-progress and offer solutions to creative problems — but cannot mandate changes. |
| **Decisions It Makes** | NO decision authority (by design) — provides recommendations only. Identifies creative problems; suggests directions; flags narrative issues; diagnoses root causes. Director retains all authority. |
| **Knowledge It Requires** | Deep narrative and film craft judgment; experience across multiple productions; ability to separate personal taste from objective critique; candor without authority; focus on problems, not solutions |
| **Inputs Needed** | Film's current story reels, rough cuts, or script; presentation from the director; production status context |
| **Outputs Produced** | Candid creative feedback; identified problems and directions; notes for the director to act on (or not); "headlining" feedback (what to blow up, what to love) |
| **Dependencies** | Depends on: Director (presents work, implements chosen feedback), Producer (facilitates sessions). Provides inputs to: Director (non-binding recommendations) |

### 6.2 Department Lead (Quality Gate)

| Attribute | Description |
|-----------|-------------|
| **Name** | Department Lead / Supervisor |
| **Also Known As** | Lead Animator, Lead Lighter, Lead Modeler, Department Supervisor |
| **Core Responsibility** | Own quality and process within their discipline. Act as first filter — supervisor should never see bad work. Approve internal rounds before dailies. Maintain quality bar and team mentorship. |
| **Decisions It Makes** | Internal shot approval (before departmental review); quality standards within discipline; task assignments within team; team mentorship priorities; which technical approaches to use; when work is ready for supervisor/dailies review |
| **Knowledge It Requires** | Deep expertise in their discipline (animation, lighting, modeling, etc.); quality discernment; team leadership; production process; mentorship ability |
| **Inputs Needed** | Artist work-in-progress; department quality standards; supervisor/director creative direction; production schedule |
| **Outputs Produced** | Approved internal rounds; quality feedback to artists; redirection of off-track work; task assignments |
| **Dependencies** | Depends on: Director/Supervisor (quality vision), Artists (execution). Provides inputs to: Artists (feedback), Supervisors (curated work) |

### 6.3 Producer (Quality Bridge)

| Attribute | Description |
|-----------|-------------|
| **Name** | Producer |
| **Also Known As** | Executive Producer, VFX Producer |
| **Core Responsibility** | Bridge creative and production management. Protect the director from organizational pressure while ensuring the project stays on budget and schedule. Ensure feedback doesn't derail scope or schedule. |
| **Decisions It Makes** | Budget and resource allocation; schedule viability; when to push back on scope changes; team composition and size; milestone gate decisions |
| **Knowledge It Requires** | Production management; budget and schedule planning; cross-discipline coordination; risk management; negotiation; understanding of creative process (to protect it) |
| **Inputs Needed** | Creative plan and milestones; budget and resources; team capacity data; department heads' reports; Braintrust/feedback outcomes |
| **Outputs Produced** | Production schedule and budget; resource allocation decisions; milestone gates; risk assessments; protected creative process |
| **Dependencies** | Depends on: Director (creative vision), Department Leads (execution capacity). Provides inputs to: All departments (schedule/budget), Director (protection) |

### 6.4 Quality Assurance / QC Specialist

| Attribute | Description |
|-----------|-------------|
| **Name** | Quality Assurance / QC |
| **Also Known As** | QA Tester (Game), QC Specialist (Film/VFX) |
| **Core Responsibility** | Ensure technical and creative quality standards are met. Bug finding, performance testing, platform certification compliance. For film/VFX: technical QC (bit depth, resolution, codec, color space); creative QC (continuity, realism, story intent). |
| **Decisions It Makes** | Whether a build/shot passes QC standards; severity classification of issues; what must be fixed before release; certification compliance |
| **Knowledge It Requires** | Platform-specific certification requirements (TRC, XR, Lotcheck); bug tracking systems; game: playtesting methodology, performance profiling; film: color space, codec, delivery spec standards; attention to detail |
| **Inputs Needed** | Game build or film shot/output; platform certification requirements; delivery specifications; bug reporting tools |
| **Outputs Produced** | QA reports and bug lists; certification status; quality sign-off; issue severity ratings |
| **Dependencies** | Depends on: Development team (builds/renders), Producers (schedule for fixes). Provides inputs to: Development team (bug reports) |

### 6.5 Postmortem Facilitator

| Attribute | Description |
|-----------|-------------|
| **Name** | Postmortem Facilitator |
| **Also Known As** | Retrospective Lead |
| **Core Responsibility** | Conduct structured post-project reviews to capture lessons learned. Stimulate discussion without assigning blame. Document what went well, what didn't, and what to change. |
| **Decisions It Makes** | What metrics to review; session structure and facilitation approach; what gets documented as key findings; recommendation priority |
| **Knowledge It Requires** | Facilitation and group dynamics; psychological safety; production process understanding; data analysis (metrics, rework counts); documentation |
| **Inputs Needed** | Project data (schedules, rework rates, milestone performance); team availability; postmortem template/format |
| **Outputs Produced** | Postmortem report (top 5 keep, top 5 change); action items for next project; institutional knowledge documentation |
| **Dependencies** | Depends on: All departments (participation), Production (data). Provides inputs to: Studio leadership, Future project teams |

---

## DOMAIN 7: PRODUCTION DOMAIN

**Scope:** Coordination, scheduling, pipeline infrastructure, resource management, technical tooling, asset management, render management.

### 7.1 Producer (Production Management)

| Attribute | Description |
|-----------|-------------|
| **Name** | Producer |
| **Also Known As** | Line Producer, VFX Producer, Executive Producer |
| **Core Responsibility** | Manage budget, schedule, and resources for a project. Bridge creative and production management. Protect the creative process from organizational pressure. |
| **Decisions It Makes** | Budget allocation across departments; schedule milestones and gates; resource distribution (staffing); vendor/outsource selection; priority when conflicts arise (which shots get resources); when to escalate issues |
| **Knowledge It Requires** | Production management; budget planning (bidding, cost tracking); scheduling and milestone planning; resource allocation; risk management; negotiation; understanding creative processes |
| **Inputs Needed** | Creative plan and deliverables; budget allocation; team availability and skill sets; department lead requests; schedule from production management |
| **Outputs Produced** | Production budget and schedule; resource allocation plan; milestone gate definitions; risk register; team structure |
| **Dependencies** | Depends on: Director (creative vision). Provides inputs to: All departments (budget/schedule constraints), Production Coordinator (execution) |

### 7.2 Production Manager

| Attribute | Description |
|-----------|-------------|
| **Name** | Production Manager |
| **Core Responsibility** | Day-to-day management of departmental workflow. Ensure tasks are assigned, tracked, and delivered on schedule. Remove operational blockers. |
| **Decisions It Makes** | Daily task prioritization; staffing adjustments within schedule; workflow optimization; inter-department handoff timing; escalation decisions |
| **Knowledge It Requires** | Production tracking tools (ShotGrid, ftrack, Jira); project management methodology; cross-department communication; scheduling; team dynamics |
| **Inputs Needed** | Department task lists; shot/asset tracking data; resource availability; milestone targets; department lead requests |
| **Outputs Produced** | Daily/weekly task assignments; status reports; blocker identification and escalation; schedule adherence tracking |
| **Dependencies** | Depends on: Producer (budget/schedule), Department Leads (task requirements). Provides inputs to: Production Coordinator (tracking), Department Leads (status) |

### 7.3 Production Coordinator

| Attribute | Description |
|-----------|-------------|
| **Name** | Production Coordinator |
| **Also Known As** | Shot Coordinator (VFX), Production Assistant |
| **Core Responsibility** | Track assets, shots, versions, and notes. Manage dailies logistics. Ensure correct versions are reviewed and delivered. Maintain communication flow between departments. |
| **Decisions It Makes** | Dailies session order and preparation; version tracking and organization; scheduling of reviews and meetings; note/documentation organization |
| **Knowledge It Requires** | Production tracking tools (ShotGrid, ftrack); version control concepts; asset tracking; meeting coordination; documentation; attention to detail |
| **Inputs Needed** | Shot/asset lists from departments; version submissions; review schedules; notes from reviews; delivery specs |
| **Outputs Produced** | Organized dailies sessions; tracked asset/shot versions; review notes documentation; status reports; delivery packages |
| **Dependencies** | Depends on: Production Manager (task priorities), Department Leads (submissions). Provides inputs to: All departments (version tracking, notes) |

### 7.4 Pipeline TD

| Attribute | Description |
|-----------|-------------|
| **Name** | Pipeline TD |
| **Also Known As** | Pipeline Technical Director, Tools TD, Pipeline Engineer |
| **Core Responsibility** | Build and maintain the technical infrastructure (pipeline) that enables all departments to work efficiently. Handle data communication between departments — save/load, import/export, plugins, environment standardization, automation. |
| **Decisions It Makes** | Pipeline tool architecture and design; automation priorities (what to automate); naming conventions and directory structures; publishing and validation standards; tool integration strategy between DCCs; build vs. buy vs. hack decisions for pipeline tools |
| **Knowledge It Requires** | Python (essential), C++ (common); Linux/Unix; deep understanding of multiple DCC tools (Maya, Houdini, Nuke, Katana); pipeline architecture patterns; asset management systems; version control (Perforce, Git); file formats (Alembic, OpenEXR, USD, FBX); problem-solving; cross-departmental workflow knowledge |
| **Inputs Needed** | Department workflow requirements; artist pain points and tool requests; production schedule for tooling priorities; CG supervisor technical direction; existing pipeline infrastructure |
| **Outputs Produced** | Pipeline tools, plugins, scripts; automation systems (publish, validate); environment configurations; naming conventions and standards; documentation and training; bug fixes and technical support |
| **Dependencies** | Depends on: CG Supervisor (technical direction), All Departments (requirements). Provides inputs to: All Departments (tools/infrastructure) |

### 7.5 Rendering TD

| Attribute | Description |
|-----------|-------------|
| **Name** | Rendering TD |
| **Also Known As** | Render TD, Rendering Engineer |
| **Core Responsibility** | Work at the tail end of the pipeline — churn out final-quality shots, optimize render times, manage render farm resources, investigate rendering artifacts. |
| **Decisions It Makes** | Render farm job prioritization; render optimization strategies (sampling, caching, denoising); render budget allocation per shot; render layer/AOV setup; resolution of rendering artifacts and crashes |
| **Knowledge It Requires** | Render engine configuration (RenderMan, Arnold, V-Ray, proprietary); render farm management (Deadline, Tractor, Plow); shading and lighting integration; ray tracing and sampling theory; GPU/CPU rendering balance; debugging and optimization |
| **Inputs Needed** | Lit and shaded scenes from Lighting TD; render farm capacity data; shot delivery deadlines; render budget specifications |
| **Outputs Produced** | Final rendered frames; optimized render settings; render farm job management; rendered AOVs; troubleshooting of render issues |
| **Dependencies** | Depends on: Lighting TD (scene setup), Shading TD (materials), Pipeline TD (farm integration). Provides inputs to: Compositor (final frames) |

### 7.6 Software Engineer / Tools Developer

| Attribute | Description |
|-----------|-------------|
| **Name** | Software Engineer / Tools Developer |
| **Also Known As** | R&D Engineer, Software R&D, Tools Engineer |
| **Core Responsibility** | Develop proprietary applications, systems, and frameworks used across the entire studio. Build the core technology stack (e.g., Presto, RenderMan, USD at Pixar; Zeno at ILM; Gazebo at Weta). |
| **Decisions It Makes** | Software architecture and API design; core technology investments; rendering algorithm approach; system performance optimization priorities; open-source vs. proprietary technology decisions |
| **Knowledge It Requires** | Computer science (algorithms, data structures, graphics); rendering technology; geometry processing; simulation science; machine learning (for research track); C++, Python, GPU programming; USD architecture; software engineering best practices |
| **Inputs Needed** | Studio technology roadmap; film/project technical requirements; artist workflow needs; R&D research directions |
| **Outputs Produced** | Proprietary software systems and frameworks; rendering technology; simulation tools; scene description frameworks (USD); production applications; tool updates and improvements |
| **Dependencies** | Depends on: CTO/VPE (technology strategy), Pipeline TD (integration requirements). Provides inputs to: All Departments (core tools) |

### 7.7 Technical Artist (Game)

| Attribute | Description |
|-----------|-------------|
| **Name** | Technical Artist (Game) |
| **Also Known As** | Tech Artist, Shader Writer, VFX Tech Artist |
| **Core Responsibility** | Bridge between artists and programmers in game development. Create shaders, tools, automation scripts, pipeline optimizations. Solve rendering/performance problems for art. |
| **Decisions It Makes** | Shader approach and material architecture; art pipeline optimization priorities; tool design for artist workflows; performance budget allocation for visuals; automation of art tasks; engine-art integration strategy |
| **Knowledge It Requires** | Game engine (Unreal, Unity, proprietary); shader programming (HLSL, GLSL, node-based); Python scripting; DCC tools (Maya, Houdini, Substance); real-time rendering; performance profiling; pipeline automation |
| **Inputs Needed** | Artist workflow requirements; engine capabilities and constraints; performance targets (frame budget); art direction requirements |
| **Outputs Produced** | Shaders and material systems; art pipeline tools and automation; performance optimization documentation; engine-art integration setup; visual debugging tools |
| **Dependencies** | Depends on: Engineering Director (engine constraints), Art Director (visual direction). Provides inputs to: All art disciplines (shaders, tools), Engineering (art requirements) |

### 7.8 Render Wrangler

| Attribute | Description |
|-----------|-------------|
| **Name** | Render Wrangler |
| **Also Known As** | Render Farm Operator, Render Technician |
| **Core Responsibility** | Manage the render farm — monitor jobs, troubleshoot failures, prioritize renders, ensure optimal utilization of computing resources. |
| **Decisions It Makes** | Render job priority and queue management; which failed renders to retry vs. escalate; render farm capacity allocation across shows/departments |
| **Knowledge It Requires** | Render farm management tools (Deadline, Tractor, Plow, OpenCue); render engine basics; Linux/Unix system administration; batch job management; troubleshooting |
| **Inputs Needed** | Render jobs from departments (rendering TDs, lighting TDs); render farm status and capacity; priority levels from production |
| **Outputs Produced** | Completed renders; farm utilization reports; job failure diagnostics; prioritized job queue |
| **Dependencies** | Depends on: Rendering TD (scene setup), Infrastructure/IT (farm hardware). Provides inputs to: All departments (completed renders) |

### 7.9 Research Scientist

| Attribute | Description |
|-----------|-------------|
| **Name** | Research Scientist |
| **Also Known As** | R&D Researcher |
| **Core Responsibility** | Push frontiers in rendering, simulation, geometry processing, machine learning. Work on technologies that may not be used for 5+ years. PhD-level research integrated with production needs. |
| **Decisions It Makes** | Research directions and priorities; publication strategy; which emerging technologies to explore; technology readiness for production transfer |
| **Knowledge It Requires** | Advanced computer science (graphics, simulation, ML, geometry); PhD-level research methodology; SIGGRAPH publication standards; understanding of production needs and constraints |
| **Inputs Needed** | Production technology challenges; industry research landscape; studio technology roadmap; research funding and resources |
| **Outputs Produced** | Research publications (SIGGRAPH); new algorithms and techniques; prototypes for production evaluation; internal knowledge transfer to engineering team |
| **Dependencies** | Depends on: CTO (research direction), Production (real problems to solve). Provides inputs to: Software R&D (new techniques), Production TD (new capabilities) |

### 7.10 Systems / IT Engineer

| Attribute | Description |
|-----------|-------------|
| **Name** | Systems Engineer / IT |
| **Also Known As** | Infrastructure Engineer, Platform Engineer, Foundation Team (Pixar) |
| **Core Responsibility** | Maintain studio infrastructure — render farm, storage systems, network, workstations, operating systems. Ensure seamless access and smooth operation of all technical resources. |
| **Decisions It Makes** | Storage architecture (tiered: hot/warm/nearline/archive); hardware procurement and lifecycle; network topology and bandwidth allocation; system security policies; backup and disaster recovery strategy |
| **Knowledge It Requires** | Linux/Unix system administration; storage systems (NAS, SAN, tiered storage); network engineering; render farm hardware; backup and recovery; performance monitoring; cloud infrastructure (for remote studios) |
| **Inputs Needed** | Studio hardware budget; department computing requirements; render farm capacity needs; storage growth projections |
| **Outputs Produced** | Maintained infrastructure and systems; storage management; render farm operations; workstation support; backup and recovery systems |
| **Dependencies** | Depends on: Studio leadership (budget). Provides inputs to: All departments (infrastructure) |

### 7.11 Asset Manager / Librarian

| Attribute | Description |
|-----------|-------------|
| **Name** | Asset Manager / Librarian |
| **Also Known As** | Asset Coordinator, Digital Asset Manager |
| **Core Responsibility** | Maintain the shared asset library — ensure correct versions, proper naming, access permissions, and metadata integrity across all digital assets. |
| **Decisions It Makes** | Asset organization and taxonomy; metadata schema; access control; archival and deletion policies; asset naming convention enforcement |
| **Knowledge It Requires** | Asset management systems; database organization; naming convention design; metadata schemas; version control concepts; production workflow understanding |
| **Inputs Needed** | Published assets from all departments; asset tracking system (ShotGrid, custom); naming convention guidelines; storage capacity data |
| **Outputs Produced** | Organized and searchable asset library; asset metadata and version tracking; access-controlled environments; archived projects |
| **Dependencies** | Depends on: Pipeline TD (asset management system), All Departments (published assets). Provides inputs to: All departments (asset access) |

---

## DOMAIN CROSS-REFERENCE MATRIX

| Capability | Domain | Creative/Technical Split | Primary Pipeline Stage |
|------------|--------|------------------------|----------------------|
| Story Artist | Story | Creative | Pre-Production |
| Screenwriter | Story | Creative | Pre-Production |
| Narrative Designer | Story | Creative-Technical | Production |
| Vis Dev Artist | Story | Creative | Pre-Production |
| Character Designer | Character | Creative | Pre-Production |
| Sculptor | Character | Creative | Pre-Production |
| Character Artist (Game) | Character | Creative-Technical | Production |
| Digital Modeler | Character | Technical-Creative | Production |
| Rigger/Rigging TD | Character | Technical | Production |
| Texture Artist | Character | Creative-Technical | Production |
| Shading/Surfacing TD | Character | Technical | Production |
| Grooming TD | Character | Technical | Production |
| Creature TD | Character | Technical | Production |
| Environment Concept Artist | Visual | Creative | Pre-Production |
| Production Designer | Visual | Creative | Pre-Production |
| Environment Artist | Visual | Creative-Technical | Production |
| Layout Artist | Visual | Creative-Technical | Production |
| Lighting TD/Artist | Visual | Creative-Technical | Post-Production |
| Matte Painter | Visual | Creative-Technical | Post-Production |
| FX/VFX Artist | Visual | Creative-Technical | Production/Post |
| Lookdev Artist | Visual | Creative-Technical | Production |
| Animator | Animation | Creative | Production |
| Animation TD | Animation | Technical | Production |
| Matchmove Artist | Animation | Technical | Post-Production |
| Motion Capture TD | Animation | Technical | Production |
| Simulation TD | Animation | Technical | Production |
| Film Director | Direction | Creative | All |
| CCO | Direction | Creative-Strategic | Pre-Production |
| Game Director | Direction | Creative | All |
| Creative Director (Game) | Direction | Creative | All |
| Showrunner | Direction | Creative-Management | All |
| VFX Supervisor | Direction | Creative-Technical | All |
| CG Supervisor | Direction | Technical | All |
| Compositing Supervisor | Direction | Creative-Technical | Post-Production |
| Art Director | Direction | Creative | All |
| Technical Director (Game) | Direction | Technical | All |
| Animation Supervisor | Direction | Creative | Production |
| Braintrust | Quality | Creative-Strategic | All |
| Department Lead | Quality | Creative-Technical | Production |
| QA/QC Specialist | Quality | Technical | Post-Production/Launch |
| Postmortem Facilitator | Quality | Process | Post-Production |
| Producer | Production | Management | All |
| Production Manager | Production | Management | All |
| Production Coordinator | Production | Management | All |
| Pipeline TD | Production | Technical | All |
| Rendering TD | Production | Technical | Post-Production |
| R&D/Tools Engineer | Production | Technical | All |
| Technical Artist (Game) | Production | Technical | All |
| Render Wrangler | Production | Technical | Post-Production |
| Research Scientist | Production | Technical-Research | Pre-Production |
| Systems/IT Engineer | Production | Technical | All |
| Asset Manager | Production | Technical-Management | All |

---

## DEPENDENCY GRAPH (Capability-Level)

```
Screenwriter → Story Artist → Layout Artist → Animator → FX Artist → Lighting TD → Rendering TD → Compositor
                  ↓                ↓              ↓                                        ↑
Character Designer → Sculptor → Digital Modeler → Rigger → Animator                    Lookdev
                   ↘                          ↘                          ↗                ↑
Environment Concept → Environment Artist → Layout Artist            Shading TD ← Texture Artist
                                                                            ↑
                                                                   Lookdev Artist
```

**Cross-Domain Dependencies:**

- **Story Domain** feeds ALL visual domains (character/environment briefs)
- **Character Domain** feeds Animation Domain (rigged character = pre-requisite)
- **Visual Domain** feeds Compositing (final render elements)
- **Direction Domain** oversees ALL domains (vision, approval, feedback)
- **Quality Domain** evaluates ALL domains (review, standards)
- **Production Domain** enables ALL domains (pipeline, scheduling, tools)
- **Animation Domain** feeds Visual Domain (animated assets to light/composite)

---

## KEY INSIGHTS FOR CAPABILITY ARCHITECTURE

1. **Creative-Technical Spectrum:** Capabilities span from pure creative (Screenwriter, Character Designer) through hybrid (Technical Artist, VFX Supervisor) to pure technical (Pipeline TD, Systems Engineer). The COS must accommodate all these modes.

2. **Decision Authority Gradient:** Direction capabilities hold final authority; Quality capabilities provide influence without authority; Production capabilities enable constraints; Creative capabilities propose and execute.

3. **Sequential Handoff with Iteration Feedback:** Despite the linear appearance of the pipeline, every capability feeds back to upstream capabilities when issues are found downstream.

4. **The Bridge Roles:** VFX Supervisor, CG Supervisor, Technical Director, Technical Artist, Pipeline TD — these roles are the critical connective tissue between creative and technical domains. They translate intent into execution.

5. **Domain Overlap:** Many capabilities sit at the boundary of domains (e.g., Shading TD straddles Character and Visual domains; FX Artist straddles Visual and Animation domains). The domain assignment reflects their primary function.

6. **Scalability Pattern:** As studios scale (50 → 500 → 2000+), the Production Domain and Pipeline TD capabilities become proportionally more critical. The infrastructure must scale with the creative ambition.

7. **External vs. Internal:** VFX capabilities are client-driven (service model); Animation/Games capabilities are internally-driven (IP ownership model). Direction Domain patterns differ significantly between these models.

---

*Generated from 6 research documents: Pixar_Production_Pipeline, VFX_House_Pipeline, Game_Studio_Pipeline, Directors_Creative_Leadership, Story_Concept_Artists, Technical_Directors_Pipeline*
*Total capabilities mapped: 47 specialist roles across 7 domains*
