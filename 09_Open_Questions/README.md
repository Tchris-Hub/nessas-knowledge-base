# Open Questions

Emerged from Wave 1 research (Pipeline Studies). Updated Jun 14, 2026.

## Foundational Questions

### Q1: Pipeline as Metaphor — Is the linear pipeline the right model?
**Context:** Every studio describes its work as a "pipeline" with discrete stages. But game studios operate iteratively (micro-loops within macro-stages). VFX houses have "loop not line" — shots circle between departments. Pixar's Braintrust creates non-linear feedback into any stage.
**Question:** Is the Creative Operating System a pipeline, a graph, a network, or something else? What happens when a user says "I want a cinematic shot" without any preceding stages? Does the system need to support non-linear creation from any starting point?

### Q2: Intent Translation — How does creative intent survive the pipeline?
**Context:** At Pixar, the director's vision is maintained through the entire 4-year process through the Braintrust, daily reviews, and a shared narrative culture. In VFX, the VFX supervisor and client director maintain intent through a strict approval hierarchy. In games, the creative director's vision is documented in the GDD but constantly tested against playability.
**Question:** How does a non-human system maintain fidelity to creative intent across 10+ specialist transformations? What mechanisms prevent "telephone game" degradation? Does the system need a persistent creative intent model that travels with the project?

### Q3: The Role of Resistance — When should the system push back?
**Context:** The Braintrust's power comes from candor — telling hard truths without authority to enforce them. The best creative decisions often come from resistance: "that character doesn't work," "that shot doesn't read."
**Question:** How does a system designed to serve user intent also know when to push back? When does "do what I say" become "you're making a mistake"? Is there a creative confidence framework the system should apply?

### Q4: Degrees of Autonomy — Who decides what?
**Context:** In professional studios, different specialists have different decision authority. A compositor can decide color balance but not change the lighting direction. A modeler can optimize topology but not redesign the character.
**Question:** What does decision authority look like in the COS? Does the user set the "director level" of involvement? Some users want full control, others want to say "make something beautiful in this style" and walk away.

## Domain-Specific Questions

### Q5: Specialist Identity
**Context:** Each research document identifies 25+ distinct specialist roles. But where are the boundaries between specialists? A texture artist and a look development artist share skills. A story artist and a concept artist overlap.
**Question:** What is the minimal set of distinct capabilities? Can we identify irreducible specialist competencies that can't be further decomposed?

### Q6: Tool Abstraction
**Context:** Blender, Maya, Houdini, Nuke, Unreal — each tool has its own paradigm, data model, and workflow. A system that sits above all of them needs an abstraction layer.
**Question:** What is the universal data model that all creative tools share? Can we define a "creative scene" data structure that any tool can be mapped to?

### Q7: Feedback Modeling
**Context:** Studios have structured feedback (dailies, reviews, Braintrust) and unstructured feedback (hallway conversations, lunch discussions).
**Question:** Can feedback be modeled as a structured system? What are the irreducible components of a creative critique? (e.g., observation → interpretation → suggestion vs. praise → critique → next steps)

### Q8: Quality Subjectivity
**Context:** In professional production, "ship quality" is a negotiated standard — it changes based on deadline, budget, and creative context.
**Question:** How does a system measure quality when quality is context-dependent? Is there a universal quality framework or does each project get its own?

## Meta Questions

### Q9: User Expertise Spectrum
**Question:** The system's promise is "no technical expertise required." But different users will have different levels of creative expertise. Does the system adapt to the user's creative sophistication? A novice needs hand-holding; a professional needs speed and precision. Is there a "creative skill calibration" mechanism?

### Q10: Learning From Mistakes
**Context:** Pixar's postmortem culture is legendary. Game studios write lengthy postmortems. VFX houses iterate on pipeline failures.
**Question:** How does the COS learn from its own mistakes? What's the equivalent of a postmortem for an AI-orchestrated creative system?

## Questions Added to Research Queue
- See 08_Research_Queue/ for prioritization
- These open questions link to specific research items
