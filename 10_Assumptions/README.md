# Assumptions — Creative Operating System Project

Tracked from the project brief, research findings, and ongoing analysis.

## Verified Assumptions (supported by research)

### A1: Technical skill is the current bottleneck
**Source:** Project brief + confirmed by all three pipeline studies. Every studio interviewed confirms that the hardest part of creative production is technical mastery — modeling, rigging, lighting, compositing. The creative vision exists; executing it is where people fail.
**Confidence:** High ✓

### A2: Production studios operate as specialist networks
**Source:** Project brief + confirmed by Pixar (pod system), VFX houses (department structure), game studios (discipline teams). Every studio decomposes creative work into specialist domains.
**Confidence:** High ✓

### A3: Specialist roles have distinct knowledge, decision processes, and workflows
**Source:** Confirmed by all six research documents. A director thinks differently than a concept artist, who thinks differently than a TD. Each role has unique mental models.
**Confidence:** High ✓

### A4: Creativity is not a linear pipeline
**Source:** Open Questions Q1. Research shows that production pipelines are described as linear but actually contain loops, iterations, non-linear feedback, and parallel workstreams. Game studios are explicitly iterative.
**Confidence:** Medium-High — the pipeline metaphor is useful but incomplete.

## Questionable Assumptions (need more evidence)

### B1: A single user can replace a director's creative authority
**Question:** The brief assumes one "user" with intent. But in real studios, creative direction is collaborative — directors consult with department heads, producers, and the Braintrust. Can one user (potentially non-expert) effectively direct a complex creative process?
**Research needed:** User studies, creative collaboration models, single-creator vs team production workflows.

### B2: Capabilities can be cleanly decomposed into independent modules
**Question:** The brief assumes a modular architecture where each capability works independently. But research shows tight coupling between roles. A character design affects modeling, which affects rigging, which affects animation. Clean decomposition may be an ideal that real creativity resists.
**Research needed:** Dependency analysis between capabilities, tight vs loose coupling in production workflows.

### B3: "No technical expertise required" is achievable
**Question:** The visionary promise. But even in elite studios, every specialist has deep technical knowledge in their domain. A concept artist knows color theory, perspective, anatomy, composition. Can a non-expert communicate intent precisely enough for professional output?
**Research needed:** Intent communication frameworks, human-to-AI creative direction studies, the precision-ambiguity tradeoff.

### B4: A capability orchestration layer above existing tools is feasible
**Question:** The brief assumes the COS sits above Blender, Unreal, etc. But studio tools have radically different data models, APIs, and paradigms. USD is a step toward unification, but most tools have limited programmatic control.
**Research needed:** USD deep dive, each tool's extensibility and API surface, existing automation frameworks.

## Emerging Assumptions (from research)

### C1: Feedback systems can be structured
**Observation:** Pixar's Braintrust, VFX dailies, and game studio playtests all follow identifiable patterns. Feedback may be more structured than the creative industry acknowledges.
**To be tested:** Can we define a universal feedback grammar?

### C2: Quality signals are learnable
**Observation:** Across all six documents, experienced professionals share consistent quality criteria. They disagree on taste but agree on craftsmanship.
**To be tested:** Can quality heuristics be codified?

### C3: The director/curator role may be the right UX model
**Observation:** The COS user is essentially a director — they communicate intent, review output, give feedback, and make decisions. The director role in studios is the closest parallel to what the COS user does.
**To be tested:** Is the director-UX model the right interface paradigm?

## Assumption Review Schedule
- Reviewed: Jun 14, 2026 (initial)
- Next review: after Wave 3 (Feedback & Quality Systems)
