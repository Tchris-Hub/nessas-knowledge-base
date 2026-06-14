# Creative Roles as Functions
## A Functional Decomposition of Creative Authority, Feedback, and Execution

**Document ID:** COS-06-AA-001
**Status:** Complete
**Last Updated:** 2026-06-14
**Purpose:** Map four creative leadership roles (Pixar Braintrust, Film Director, Creative Director, VFX Supervisor) as composable software systems with clear capability boundaries, interface contracts, and failure modes.
**Key Architectural Insight:** The Braintrust is a FEEDBACK function that is architecturally SEPARATE from the APPROVAL function. This separation of concerns is the most transferable pattern from the research — it is what distinguishes constructive critique from command authority.

---

## Table of Contents

1. [Architecture Overview: The Four Systems](#1-architecture-overview)
2. [System 1: Braintrust (Feedback Authority)](#2-system-1-braintrust)
3. [System 2: FilmDirector (Vision & Approval Authority)](#3-system-2-filmdirector)
4. [System 3: CreativeDirector (Direction & Quality Evaluation)](#4-system-3-creativedirector)
5. [System 4: VFXSupervisor (Creative-Technical Bridge)](#5-system-4-vfxsupervisor)
6. [System Interaction Diagrams](#6-system-interaction-diagrams)
7. [Cross-System Comparison Matrix](#7-cross-system-comparison-matrix)
8. [Architectural Patterns & Transferable Insights](#8-architectural-patterns)

---

## 1. Architecture Overview

### The Four Systems at a Glance

| System | Primary Role | Authority Type | Key Separation |
|--------|-------------|---------------|----------------|
| Braintrust | Feedback without mandate | Influence only | FEEDBACK != APPROVAL |
| FilmDirector | Vision + Final Approval | Full creative authority | APPROVAL != FEEDBACK |
| CreativeDirector | Direction + Quality Bar | Directional authority | DIRECTION != EXECUTION |
| VFXSupervisor | Creative-Technical Bridge | Execution authority | BRIDGE != VISION |

### The Central Architectural Insight

The most transferable pattern from Pixar's Braintrust research is the **separation of the Feedback function from the Approval function**. In most software systems, feedback and approval are conflated — a code reviewer both suggests changes AND blocks merging. Pixar's innovation is isolating these:

- **Braintrust (Feedback System):** Generates signals. Has zero authority to act on them. Cannot reject, block, or mandate. Its only output is information.
- **FilmDirector (Approval System):** Receives signals. Retains full authority to accept, reject, or ignore them. Its primary output is binding decisions.

This creates psychological safety: the feedback system can be maximally candid because it bears no consequence burden. The approval system can be maximally decisive because it is not defensive.

---

## 2. System 1: Braintrust (Feedback Authority)

### 2.1 System Identity

**Name:** Braintrust
**Aliases:** Story Trust, Peer Review Engine
**Domain:** Quality (cross-domain)
**Architectural Role:** Feedback signal generator — read-only evaluator with zero write authority
**Key Constraint:** MUST NOT own any decision or gate

### 2.2 Functions

| # | Function Name | Description | Invocation Pattern |
|---|---|---|---|
| F1 | **evaluateNarrative** | Assess story structure, character arcs, pacing, emotional beats, and thematic coherence against craft principles (McKee: inciting incident, spine, crisis/climax, subtext) | Periodic review (every ~2-4 months per project); triggered by milestone |
| F2 | **identifyProblems** | Surface creative issues — narrative breaks, character inconsistencies, pacing gaps, tonal drift. Focus on WHAT is wrong, not HOW to fix it. | Output of evaluateNarrative |
| F3 | **suggestDirections** | Propose high-level resolution vectors without prescribing specific solutions. "Focus on problems, not solutions" is an operating principle, not a strict constraint — directions are permitted, mandates are not. | Output of identifyProblems |
| F4 | **headlineFeedback** | Synthesize feedback into prioritized summary: "What to blow up? What to love?" — the producer's technique for actionable critique. | Post-processing of F1-F3 |
| F5 | **maintainCompact** | Protect the psychological safety contract: enforce candor norms, prohibit personal attacks, ensure no decision authority leaks into the session. | Meta-function — always active during F1-F4 invocation |

### 2.3 Inputs

| Input | Type | Description | Source |
|-------|------|-------------|--------|
| WorkInProgress | Artifact | Current state of the creative work — story reels, rough cuts, animatics, script drafts, playblasts | Director (via Producer or ProductionCoordinator) |
| CreativeIntent | Text | The director's stated goals, thematic intentions, emotional targets for the piece | Director |
| ProductionContext | Structure | Current phase, schedule pressure, known constraints. Helps calibrate feedback scope. | Producer |
| PeerArtifacts | Reference | Comparable work or past Braintrust precedents for calibration (optional) | History store |
| SessionFormat | Configuration | Rules of engagement: timebox, rotation order, headlining request | Facilitator |

### 2.4 Outputs

| Output | Type | Description | Consumer |
|--------|------|-------------|----------|
| FeedbackSignal | Structured Notes | Candid, specific feedback organized by priority. Explicitly non-binding. Includes: identified problems, suggested directions, headlined priorities ("blow up" / "love"). | Director (only consumer) |
| SessionArtifact | Document | Record of feedback session for reference. Not automatically actionable. | Producer, History store |
| ConfidenceScore | Rating | Calibrated certainty of each feedback item (e.g., "strong signal" vs "minor note"). Prevents all feedback from being treated equally. | Director (embedded in FeedbackSignal) |

### 2.5 Decisions It Owns

**The Braintrust owns ZERO decisions by design.** This is not a limitation — it is the core architectural feature.

- It does NOT approve or reject any work.
- It does NOT block progress.
- It does NOT mandate changes.
- It does NOT allocate resources.
- It does NOT set deadlines.

The only "decision" the Braintrust owns is: **which problems to surface and how to frame them.** This means:
- It decides what constitutes a problem worth raising (editorial gate on its own output)
- It decides which directions to suggest (but not which are adopted)
- It decides the priority/severity of each issue

### 2.6 Knowledge It Requires

| Knowledge Domain | Description | Source |
|------------------|-------------|--------|
| Narrative craft principles | McKee's story principles: inciting incident, spine, subtext, crisis/climax, the negation of the negation, value swing at climax | Training data, library |
| Multiple film production experience | Pattern recognition from having seen many projects through from rough to final. The Braintrust knows what "fixable" looks like. | Historical project data |
| Genre conventions | Understanding of genre-specific audience expectations, tropes, and subversion patterns | Taxonomy, library |
| Candor delivery | Ability to separate person from work; frame critique constructively; identify root causes vs. symptoms | Operating principle (can be rule-based) |
| Cross-domain awareness | Understanding of how narrative problems cascade into animation, lighting, and scheduling impacts | Dependency graph |

### 2.7 Dependencies

| Dependency | Type | Direction | Notes |
|------------|------|-----------|-------|
| FilmDirector | Required | ← Director submits work; → Braintrust sends feedback | The Braintrust cannot exist without a director to receive its output |
| Producer | Required | ← Facilitates session logistics; → Receives session artifact | Producer role is essential for scheduling and compact protection |
| WorkInProgress | Required | ← Must have something to evaluate | Cannot operate on empty input; idle until triggered |
| ProjectHistory | Optional | ← Past Braintrust sessions for context | Informs calibration over time |

### 2.8 Failure Modes

| Failure Mode | Description | Manifestation | Mitigation |
|-------------|-------------|---------------|------------|
| AuthorityLeak | Braintrust member gives a command instead of a suggestion ("do X, not Y") | Director becomes defensive; psychological safety erodes | Compact maintainer (F5) intervenes; session can be reset |
| DesignByCommittee | Group converges on safe, mediocre feedback instead of candor | Bland notes; no bold critique | Rotate membership; enforce headlining; invite dissenting voices |
| SolutionPrescription | Group fixates on their preferred fix instead of identifying the root problem | Director feels disempowered; wrong problem may get solved | Re-frame: "what's the problem?" not "what's the solution?" |
| FalseConsensus | Loudest voice dominates; minority opinions suppressed | Critical issues missed | Structured round-robin; anonymous pre-feedback collection |
| FeedbackFatigue | Too many sessions; feedback becomes routine and shallow | Diminishing returns; team ignores Braintrust | Reduce cadence; only call when there's real unfinished work to review |
| AuthorityDrift | Over time, Braintrust output is treated as de facto mandates | Director stops pushing back; feedback system gains effective authority | Re-certify the compact periodically; explicitly document non-binding nature |

### 2.9 Interface

```
// Braintrust System Interface
// Feedback Authority — zero write access to any production system

interface Braintrust {
    // Core evaluation
    evaluate(input: {
        workInProgress: Artifact,
        creativeIntent: CreativeBrief,
        productionContext: ProductionPhase,
        sessionConfig?: SessionConfiguration
    }): Promise<FeedbackPackage>;

    // Feedback retrieval (non-blocking, read-only)
    getLatestFeedback(projectId: ProjectID): FeedbackPackage;
    getFeedbackHistory(projectId: ProjectID, limit?: number): FeedbackPackage[];
}

// Data types
type FeedbackPackage = {
    sessionId: string;
    timestamp: DateTime;
    artifacts: {
        problems: Problem[];
        directions: Direction[];
        headline: { blowUp: string[]; love: string[] };
        confidence: Map<ProblemID, ConfidenceLevel>;
    };
    meta: {
        participants: AgentID[];
        duration: Duration;
        compactViolations?: number;
    };
};

type Problem = {
    id: ProblemID;
    domain: 'narrative' | 'character' | 'pacing' | 'tone' | 'structure' | 'execution';
    description: string;          // What is wrong
    rootCauseHypothesis?: string;  // Possible underlying cause
    severity: Criticality;
};

type Direction = {
    problemId: ProblemID;
    suggestedVector: string;   // High-level direction (not a specific solution)
    alternatives?: string[];
};

enum ConfidenceLevel { STRONG_SIGNAL, PLAUSIBLE, MINOR_NOTE, UNSURE }
enum Criticality { BLOCKING, SIGNIFICANT, NOTABLE, COSMETIC }
```

**Key interface contract:** The Braintrust interface is PURELY READ-ONLY with respect to the creative work. It cannot invoke any mutating API on artifacts, pipelines, or schedules. It produces signals, not commands.

---

## 3. System 2: FilmDirector (Vision & Approval Authority)

### 3.1 System Identity

**Name:** FilmDirector
**Aliases:** Director, Creative Authority
**Domain:** Direction (creative)
**Architectural Role:** Vision setter, final approver, creative decision-maker
**Key Constraint:** Holds final say but must remain receptive to feedback from Braintrust

### 3.2 Functions

| # | Function Name | Description | Invocation Pattern |
|---|---|---|---|
| F1 | **setCreativeVision** | Define the artistic North Star: story direction, emotional intent, tone, visual style. Produce look books, tone packets, and creative briefs. | On project start; refreshed at key transitions |
| F2 | **approveShot** | "Final" a shot — give binding approval for it to move forward in the pipeline. This is a GATE function: nothing downstream proceeds without it. | Continuous during dailies; per-shot basis |
| F3 | **rejectShot** | Send a shot back for revision with specific notes. Not a destructive action — creates a rework signal. | Paired with approveShot |
| F4 | **makeCreativeDecision** | Resolve ambiguity or conflict between department proposals. Choose between alternatives. | Ad-hoc; when department recommendations conflict |
| F5 | **evaluateFeedback** | Receive, interpret, and decide which Braintrust feedback to act on. Convert external feedback into internal directives. | After each Braintrust session |
| F6 | **protectCore** | Distinguish between negotiable elements and non-negotiable core story/emotional elements. "Know which hill to die on." | Continuous — meta-decision across all other functions |
| F7 | **communicateVision** | Translate abstract creative intent into concrete direction for each department: performance notes for animators, look references for lighting, pacing notes for editorial. | Continuous; shifts mode by audience |

### 3.3 Inputs

| Input | Type | Description | Source |
|-------|------|-------------|--------|
| Script | Document | Narrative blueprint — dialogue, scene description, structure | Screenwriter |
| DepartmentProposals | Artifact[] | Work-in-progress from each department seeking approval | All departments via dailies |
| BraintrustFeedback | FeedbackPackage | Non-binding peer critique from Braintrust sessions | Braintrust system |
| ResourceConstraints | Structure | Schedule, budget, team capacity from production | Producer |
| ShotStatus | Status[] | Current state of each shot in the pipeline | ProductionCoordinator / ShotGrid |

### 3.4 Outputs

| Output | Type | Description | Consumer |
|--------|------|-------------|----------|
| ApprovedShots | ShotID[] | Binding approval signals — shots cleared to proceed | All downstream departments |
| RejectedShots | Rejection[] | Shots sent back for revision with director notes | Department that submitted shot |
| CreativeDirection | Directive[] | Notes, look references, performance guidance, intentionality | All departments |
| VisionArtifacts | Artifact[] | Look books, tone packets, mood boards, creative briefs | All departments (foundation) |
| DecisionRecord | Log | Record of creative decisions for traceability | Producer, History |

### 3.5 Decisions It Owns

| Decision | Scope | Finality |
|----------|-------|----------|
| Shot approval (finalling) | Per-shot | Absolute — cannot be overridden |
| Creative direction | Project-wide | Absolute within project |
| Which Braintrust feedback to act on | Per-feedback | Absolute — no obligation |
| Resource allocation (creative) | Per-department priority | Shared with Producer (budget) |
| Core vs. negotiable elements | Project-wide | Absolute — defines what must be protected |

### 3.6 Knowledge It Requires

| Knowledge Domain | Description | Source |
|------------------|-------------|--------|
| Story structure & McKee principles | Inciting incident, spine, subtext, crisis/climax, beat/scene/act architecture | Training, experience |
| Cinematography | Camera angles, lens choice, composition, depth of field, lighting theory | Training, experience |
| Performance direction | Actor communication vocabulary: beat, subtext, motivation, intensity, commit | Training, experience |
| All department workflows | Working knowledge of every pipeline stage — enough to give actionable notes | Cross-training, experience |
| Creative compromise calculus | When to fight, when to concede; strategic sacrifice patterns | Experience |
| Braintrust calibration | How to weight feedback signals from different Braintrust members | Experience, history |

### 3.7 Dependencies

| Dependency | Type | Direction | Notes |
|------------|------|-----------|-------|
| Braintrust | Optional | ← Receives feedback signals | Can operate without Braintrust but quality degrades |
| Screenwriter | Required | ← Script | Can co-write but usually separate |
| Producer | Required | ← Budget, schedule, protection | Essential resource constraint input |
| Department Leads | Required | ← Execution; ← Work for approval | The approval function needs something to approve |
| ProductionCoordinator | Required | ← Shot tracking, dailies logistics | Information pipeline |

### 3.8 Failure Modes

| Failure Mode | Description | Manifestation | Mitigation |
|-------------|-------------|---------------|------------|
| VisionVacuum | Director fails to articulate clear creative intent | Departments work at cross-purposes; rework cascades | Force concrete vision artifacts early; "I'll know it when I see it" is creative theft |
| ApprovalBottleneck | Director becomes gate for too many decisions | Pipeline stalls; artists idle while waiting for sign-off | Delegate approval authority to department leads for non-hero shots; reserve director approval for finalling gates |
| Defensiveness | Director ignores or resists feedback | Braintrust atrophies; candid feedback stops | Architectural fix: Braintrust has zero authority, so there's nothing to resist against. If defensiveness persists, it's a culture/trust issue. |
| ScopeCreepByFiat | Director keeps making changes late in pipeline | Massive rework; schedule and budget overrun | Couple creative decisions with producer-provided cost estimates; force trade-off awareness |
| AnalysisParalysis | Director can't decide between alternatives | Team waits; momentum lost | Timebox decisions; default to most audacious option |
| Micromanagement | Director makes granular decisions instead of setting vision | Department leads disempowered; bottleneck forms | Push decision authority to department leads; director only sets intent and finals shots |
| DelegationFailure | Director delegates core story decisions | Loss of coherent vision; project drifts | Distinguish core (protect) from negotiable (delegate); maintain final say on core |

### 3.9 Interface

```
// FilmDirector System Interface
// Vision & Approval Authority — owns GATE functions

interface FilmDirector {
    // Creative vision
    setVision(input: VisionBrief): Promise<VisionArtifact>;
    getCurrentVision(projectId: ProjectID): VisionArtifact;

    // Shot approval (gate function)
    approveShot(shotId: ShotID, notes?: Note[]): Promise<Approval>;
    rejectShot(shotId: ShotID, notes: Note[]): Promise<Rejection>;
    batchReview(shots: ShotReview[]): Promise<ReviewBatch>;

    // Decision making
    makeDecision(alternatives: Alternative[], context: DecisionContext): Promise<Decision>;
    protectCore(proposal: Proposal, coreConstraints: CoreElement[]): Promise<Decision>;

    // Feedback reception (from Braintrust)
    receiveFeedback(feedback: FeedbackPackage): Promise<void>;
    resolveFeedback(feedbackId: FeedbackID, actions: Action[]): Promise<Resolution>;

    // Communication
    issueDirective(target: Department | AgentID, intent: CreativeDirection): Promise<void>;
    broadcastDirection(directives: Directive[]): Promise<void>;
}

// Data types
type Approval = {
    shotId: ShotID;
    status: 'APPROVED' | 'APPROVED_WITH_NOTES';
    timestamp: DateTime;
    notes?: Note[];
    nextReviewGate?: DateTime;
};

type Rejection = {
    shotId: ShotID;
    status: 'REJECTED';
    timestamp: DateTime;
    notes: Note[];           // Must specify what to fix
    severity: 'MINOR_RESHOT' | 'MAJOR_RESHOT' | 'SCRAP_AND_RESTART';
    priority: Priority;
};

type VisionArtifact = {
    briefs: CreativeBrief[];
    lookBooks: Reference[];
    tonePackets: Media[];
    coreElements: CoreElement[];
};

type Decision = {
    id: DecisionID;
    selected: Alternative;
    rejected: Alternative[];
    rationale: string;
    binding: boolean;
};
```

**Key interface contract:** The FilmDirector owns all MUTATING operations on shot/artifact state. It is the only system that can change the status of work from "in progress" to "approved." It is also the ONLY consumer of Braintrust output — feedback flows directionally to the director, not to executing departments.

---

## 4. System 3: CreativeDirector (Direction & Quality Evaluation)

### 4.1 System Identity

**Name:** CreativeDirector
**Aliases:** Creative Lead, Vision Keeper (Game), "One who owns the heart"
**Domain:** Direction (creative, game/interactive focus)
**Architectural Role:** Direction setter and quality evaluator — defines the "what" and evaluates the "how well," shared decision authority with GameDirector
**Key Distinction:** Unlike FilmDirector who owns both vision AND approval, CreativeDirector owns vision/direction but shares approval with a GameDirector (production/scope counterpart). "One owns the heart. One owns the spine."

### 4.2 Functions

| # | Function Name | Description | Invocation Pattern |
|---|---|---|---|
| F1 | **setEmotionalIdentity** | Define the core emotional experience: what the player should feel, the tonal palette, the emotional arc across the experience | Project start; refreshed at phase transitions |
| F2 | **evaluateQuality** | Assess work against the emotional identity and tonal consistency bar. "Does this feel like the game we're making?" | Continuous; reviewed during milestone checkpoints |
| F3 | **defineArtDirection** | Set visual style, color philosophy, shape language, world-building rules, character identity guidelines | Pre-production; updated as vision refines |
| F4 | **alignStoryAndMechanics** | Ensure narrative and gameplay reinforce each other. Story-mechanic alignment is the core quality filter for interactive work. | Throughout; critical at design review gates |
| F5 | **evaluateTonalConsistency** | Check that every element (art, audio, narrative, UI, gameplay) speaks the same tonal language | Milestone reviews, vertical slices |
| F6 | **provideDirectionFeedback** | Give creative guidance to discipline leads (art, narrative, audio, animation) without overriding their execution authority | Dailies, discipline-specific reviews |

### 4.3 Inputs

| Input | Type | Description | Source |
|-------|------|-------------|--------|
| GameDesignDirection | DesignDoc | Core gameplay loop, feature set, scope — from GameDirector | GameDirector |
| ConceptArtAndVisDev | Artifact[] | Visual exploration of the game world and characters | Art department |
| NarrativeScripts | Document[] | Story, dialogue, character arcs | Writers, Narrative Designers |
| GameplayPrototypes | Prototype[] | Interactive builds for evaluating feel and alignment | Engineering, Design |
| ProductionConstraints | Structure | Milestone deadlines, scope limits, team capacity | Producer, GameDirector |
| PlaytestResults | Feedback[] | Player reaction data for calibration | QA, User Research |

### 4.4 Outputs

| Output | Type | Description | Consumer |
|--------|------|-------------|----------|
| QualityEvaluation | Evaluation[] | Per-element quality assessment against creative vision. "Pass" / "Needs Work" / "Does Not Fit." | All disciplines |
| ArtDirectionGuidelines | Document | Style guides, color scripts, shape language bibles, world-building rules | Art, Animation, UI, Audio |
| AlignmentFeedback | Note[] | Cross-discipline notes ensuring story-mechanic alignment, tonal consistency | Design, Art, Narrative, Audio |
| EmotionalIdentityBrief | Brief | The definitive statement of what the player should feel and when | All disciplines (foundation) |
| TonalExceptions | Exception[] | Explicit allowances for tonal deviation (e.g., comedy beat in a dramatic scene) | All disciplines |

### 4.5 Decisions It Owns

| Decision | Scope | Shared With |
|----------|-------|-------------|
| Emotional/tonal direction | Project-wide | GameDirector (veto on feasibility) |
| Art style & visual identity | Project-wide | Art Director (execution) |
| Quality bar definition | Project-wide | GameDirector (scope feasibility) |
| Story-theme alignment | Narrative + systems | Narrative Director (execution) |
| What "feels like our game" | All elements | No shared authority — this is the CD's unique decision |
| **Does NOT own:** scope, schedule, budget, technical feasibility | — | GameDirector, Producer, Technical Director |

### 4.6 Knowledge It Requires

| Knowledge Domain | Description | Source |
|------------------|-------------|--------|
| Narrative craft | Story structure, character arcs, thematic development, dialogue | Training, experience |
| Visual arts | Color theory, composition, design principles, art history | Training, experience |
| Game design fundamentals | Core loop design, player psychology, interactivity principles | Training, experience |
| Cross-discipline awareness | Understanding of art, design, engineering, audio, animation pipelines enough to give relevant feedback | Cross-training, experience |
| Player psychology | What makes interactive experiences emotionally resonant; player agency, game feel, player motivation | Research, playtesting data |
| Genre conventions | Deep knowledge of genre-specific audience expectations and innovation opportunities | Experience |
| Tone calibration | Ability to distinguish tonal consistency from monotony; know when to break the rules | Experience |

### 4.7 Dependencies

| Dependency | Type | Direction | Notes |
|------------|------|-----------|-------|
| GameDirector | Required | ↔ Shared creative vision; CD sets emotional direction, GD sets scope/feasibility | Symbiotic relationship |
| Art Director | Required | ← Art execution; → Art direction guidelines | Translates emotional identity into visual execution |
| Writers / Narrative Designers | Required | ← Narrative content; → Alignment feedback | Story mechanics alignment |
| Producer | Required | ← Schedule/budget constraints | Feasibility boundary for creative decisions |
| PlaytestSystem | Required | ← Player feedback data | Grounds quality evaluation in real user data |

### 4.8 Failure Modes

| Failure Mode | Description | Manifestation | Mitigation |
|-------------|-------------|---------------|------------|
| VisionWithoutFeasibility | Sets emotional direction impossible to deliver within constraints | Team demoralized; scope crisis at milestone | Pair with GameDirector who provides feasibility check |
| QualityAsRebound | Evaluates everything as "not good enough" — never signs off | Team trapped in infinite polish; never ships | Set clear "pass" criteria per phase; distinguish polish from direction change |
| TonalDogmatism | Demands strict tonal consistency that excludes all variety | World feels flat; no emotional contrast or surprise | Define allowable tonal range, not a single note; encourage controlled contrast |
| StoryMechanicsConflict | Pushes narrative that contradicts gameplay loop | Players feel friction between story and what they do | Prototype story-mechanic interactions early; fix one or the other |
| CreativeDirectorTrap | CD tries to act as GameDirector (owns scope/feasibility) | Confused priorities; team gets mixed signals | Clear role boundaries; CD says "what feels right," GD says "what we have resources for" |
| FeedbackOverload | Gives detailed notes on everything | No prioritization; team can't distinguish critical from cosmetic | Adopt Braintrust headlining technique: what to blow up, what to love |

### 4.9 Interface

```
// CreativeDirector System Interface
// Direction & Quality Evaluation — "Owner of the Heart"

interface CreativeDirector {
    // Emotional identity
    setEmotionalIdentity(input: EmotionalBrief): Promise<EmotionalIdentityArtifact>;
    getEmotionalIdentity(projectId: ProjectID): EmotionalIdentityArtifact;

    // Quality evaluation
    evaluate(element: Artifact | Element, context: EvaluationContext): Promise<Evaluation>;
    batchEvaluate(elements: Artifact[], context: EvaluationContext): Promise<Evaluation[]>;
    getQualityBar(domain: QualityDomain): QualityCriteria;

    // Art direction
    setArtDirection(guidelines: ArtDirectionGuide): Promise<void>;
    validateStyle(proposal: ArtProposal): Promise<StyleValidation>;

    // Story-mechanics alignment
    evaluateAlignment(narrative: NarrativeElement, mechanics: GameplayElement): Promise<AlignmentScore>;
    resolveConflict(conflict: AlignmentConflict): Promise<Resolution>;

    // Tonal consistency
    checkConsistency(element: Artifact, tonalBaseline: TonalProfile): Promise<ConsistencyCheck>;
    approveException(element: Artifact, justification: string): Promise<Exception>;
}

// Data types
type Evaluation = {
    elementId: ID;
    status: 'PASS' | 'NEEDS_WORK' | 'DOES_NOT_FIT' | 'EXCEPTION';
    score: number;                 // 0-100 quality score
    breakdown: {
        emotionalAlignment: number;
        tonalConsistency: number;
        narrativeCoherence: number;
        craftExecution: number;
    };
    notes: Note[];
    priority: Priority;
};

type EmotionalIdentityArtifact = {
    coreEmotion: string;           // What the player should feel
    tonalPalette: ToneProfile[];   // Primary, secondary, and accent tones
    emotionalArc: Beat[];          // Emotional journey from start to end
    forbiddenEmotions: string[];   // What the game should NOT feel like
};

type AlignmentScore = {
    score: number;                 // 0-100
    conflicts: AlignmentConflict[];
    opportunities: AlignmentOpportunity[];
};
```

**Key interface contract:** The CreativeDirector evaluates but does not gate-keep in the same way as FilmDirector. It produces quality signals that feed into the GameDirector's scope/feasibility decisions and the Art Director's execution priorities. The CD is an advisor with strong directional authority but NO binding approval on schedule or budget.

---

## 5. System 4: VFXSupervisor (Creative-Technical Bridge)

### 5.1 System Identity

**Name:** VFXSupervisor
**Aliases:** VFX Sup, On-Set VFX Supervisor, Visual Effects Supervisor
**Domain:** Direction (creative-technical hybrid)
**Architectural Role:** Bidirectional translation layer between creative intent and technical execution. The critical bridge that converts "what we want" into "how we'll achieve it."
**Key Constraint:** Works BOTH on-set (during production, advising Director/DP) AND in-studio (during post-production, managing VFX pipeline). Operates in a client-driven service model.

### 5.2 Functions

| # | Function Name | Description | Invocation Pattern |
|---|---|---|---|
| F1 | **translateCreativeToTechnical** | Convert film director's artistic vision into specific technical instructions for VFX departments. This is THE defining function — bidirectional translation. | Continuous; critical at shot review and on-set |
| F2 | **adviseOnSet** | On production set: advise Director and DP on VFX requirements (camera placement, greenscreen, lighting for VFX, tracking markers). Ensure data capture quality. | During principal photography |
| F3 | **approveVFXShot** | Final quality approval on VFX shots before client (director) delivery. Gate function for VFX output. | Continuous during post-production |
| F4 | **determineTechnique** | Decide which technique for each effect: practical vs. digital, full CG vs. 2D projection, simulation approach. Technical strategy ownership. | Pre-production through production |
| F5 | **manageClientRelationship** | Interface with film production's client-side VFX supervisor and director. Bid notes, manage expectations, present work-in-progress. | Throughout production |
| F6 | **bidAndPlan** | Scope VFX work during bidding phase: estimate shot complexity, budget, timeline. Translate script breakdown into VFX tasks. | Pre-production, bidding |
| F7 | **leadTechnicalR&D** | Identify technical challenges requiring new tools or approaches. Direct CG Supervisor and Pipeline TDs on R&D priorities. | Pre-production, early production |

### 5.3 Inputs

| Input | Type | Description | Source |
|-------|------|-------------|--------|
| DirectorVision | CreativeBrief | Film director's artistic intent for VFX sequences | Film Director |
| ScriptBreakdown | Beat[] | Script analyzed beat-by-beat; each beat identifies VFX requirements | Pre-production team |
| OnSetData | Data[] | Plate footage, HDR environment maps, LIDAR scans, lens metadata, reference photography | On-set capture team |
| DepartmentProposals | Proposal[] | Technical approaches and visual results from VFX departments | CG Supervisor, Department Leads |
| ClientNotes | Note[] | Feedback from film production's client-side VFX supervisor or director | External (client) |
| ProductionConstraints | Structure | Budget, schedule, render resources, team capacity | VFX Producer |

### 5.4 Outputs

| Output | Type | Description | Consumer |
|--------|------|-------------|--------|
| TechnicalDirection | Directive[] | Translated creative notes into specific technical instructions for each department | All VFX departments |
| ShotApprovals | Approval[] | Final sign-off on VFX shots before client delivery | Compositing Sup, CG Sup |
| OnSetGuidance | Directive[] | Real-time direction to set crew for VFX-optimal capture | On-set crew, DP, Director |
| TechniqueDecisions | Decision[] | Which methodology for each VFX challenge | All departments |
| ClientPresentations | Presentation[] | Curated shot progress for client review, with commentary | Client (film production) |
| BiddingEstimates | Estimate[] | Shot complexity, budget, timeline projections | VFX Producer, Client |

### 5.5 Decisions It Owns

| Decision | Scope | Shared With |
|----------|-------|-------------|
| VFX technique selection (practical vs. digital, which approach) | Per-shot | CG Supervisor (technical feasibility input) |
| VFX shot quality approval | Per-shot (before client) | No shared authority — final VFX quality gate |
| On-set technical guidance | Per-production day | Director, DP (can override for non-VFX reasons) |
| Client note interpretation | Per-note | CG Supervisor (technical translation) |
| Scope of VFX work for bidding | Project | VFX Producer (budget) |
| Presentation priority (what client sees) | Per-review | Client-side VFX Supervisor |

### 5.6 Knowledge It Requires

| Knowledge Domain | Description | Source |
|------------------|-------------|--------|
| Full VFX pipeline | End-to-end understanding of every stage: matchmove → modeling → rigging → texturing → lookdev → animation → FX → lighting → compositing | 10+ years production experience |
| Cinematography & photography | Camera optics, lens distortion, exposure, color temperature, lighting theory | Cross-training, experience |
| Practical & digital VFX | Knowledge of on-set practical effects AND digital techniques; knows when to use each | Experience |
| Client management | Negotiation, expectation management, note interpretation, presentation skills | Experience |
| On-set protocol | Set etiquette, safety, communication with DP and Director | Experience |
| Bidding & negotiation | Shot complexity estimation, budget modeling, scope management | Experience |
| All DCC tooling | Working knowledge of Maya, Houdini, Nuke, Katana, RenderMan, tracking tools | Training, experience |

### 5.7 Dependencies

| Dependency | Type | Direction | Notes |
|------------|------|-----------|-------|
| Film Director | Required | ← Creative vision; → Technical direction | Primary client of VFX Sup's translation function |
| CG Supervisor | Required | ← Technical execution; → Technical direction | CG Sup executes the technical plan; VFX Sup directs |
| VFX Producer | Required | ← Budget/schedule; → Technical decisions with cost context | Shared authority on scope/budget |
| On-set crew | Required | ← Execute VFX capture | VFX Sup directs but doesn't operate camera |
| Department Leads | Required | ← Department proposals; → Department direction | Translates creative to technical for each discipline |
| Client-side VFX Sup | Required (external) | ← Client notes; → Client presentations | External stakeholder above studio VFX Sup in chain |

### 5.8 Failure Modes

| Failure Mode | Description | Manifestation | Mitigation |
|-------------|-------------|---------------|------------|
| TranslationLoss | Creative intent degrades through technical translation | VFX doesn't match director's vision | Create lookdev reference earlier; VFX Sup stays in direct communication with director |
| OnSetAbsence | VFX Sup not present during critical capture moments | Missing or poor data makes VFX impossible/expensive later | VFX Sup or designated on-set rep MUST be present during VFX-heavy shoots |
| YesEverything | Agrees to every director request without feasibility check | Team overwhelmed; impossible deadline | Always couple acceptance with cost estimate: "Yes, and here's what that costs" |
| BottleneckReview | VFX Sup becomes sole quality gate; approvals pile up | Production stalls waiting for sign-off | Delegate to CG Supervisor for non-hero shots; VFX Sup only gates hero + client-ready |
| ClientOveradaptation | Over-interprets client notes to please rather than protect quality | VFX quality degrades chasing every note | Preserve the "note behind the note" diagnosis; don't implement literally |
| TechnicalDogmatism | Always chooses familiar technique over novel but better approach | Work is reliable but never innovative | Allocate R&D budget; rotate technique selection criteria |
| MissingOnSetData | Fails to capture essential data during production | VFX shots require massive reconstruction effort | Checklist-driven on-set capture; data review before leaving set |

### 5.9 Interface

```
// VFXSupervisor System Interface
// Creative-Technical Bridge — Translation + Technical Gate

interface VFXSupervisor {
    // Translation (core function)
    translateCreativeToTechnical(input: {
        creativeIntent: CreativeBrief,
        shotData: ShotContext,
        constraints: TechnicalConstraints
    }): Promise<TechnicalDirection[]>;

    translateTechnicalToCreative(input: {
        technicalResult: RenderedPass,
        targetIntent: CreativeBrief
    }): Promise<CreativeEvaluation>;

    // On-set guidance
    adviseOnSet(input: {
        scenePlan: ScenePlan,
        vfxRequirements: VFXRequirement[],
        currentSetup: SetConfiguration
    }): Promise<OnSetDirective[]>;

    verifyDataCapture(input: {
        capturedData: DataPackage,
        requirements: DataRequirement[]
    }): Promise<DataQualityReport>;

    // Technique selection
    selectTechnique(input: {
        creativeGoal: CreativeBrief,
        availableResources: ResourcePool,
        constraints: TechnicalConstraints,
        alternatives: TechniqueOption[]
    }): Promise<TechniqueDecision>;

    // Shot approval (gate)
    approveVFXShot(shotId: ShotID, evaluation: CreativeEvaluation): Promise<Approval>;
    rejectVFXShot(shotId: ShotID, technicalDirection: TechnicalDirection[]): Promise<Rejection>;
    batchApprove(criteria: BatchCriteria): Promise<BatchApproval[]>;

    // Client management
    prepareClientPresentation(shots: ShotID[], narrative: string): Promise<Presentation>;
    interpretClientNotes(notes: Note[], shotContext: ShotContext): Promise<InterpretedNote[]>;

    // Planning
    estimateShotComplexity(scriptBreakdown: Beat[]): Promise<ComplexityEstimate[]>;
    generateBid(bids: ComplexityEstimate[]): Promise<BidPackage>;
}

// Data types
type TechnicalDirection = {
    department: Department;
    priority: Priority;
    instructions: string[];      // Specific technical approach
    creativeRationale: string;   // WHY this approach (for artist understanding)
    constraints: {
        budget: TimeBudget;
        qualityFloor: QualityStandard;
    };
    references: Reference[];
};

type TechniqueDecision = {
    shotId: ShotID;
    selected: TechniqueOption;
    rejected: TechniqueOption[];
    rationale: string;
    confidence: number;          // 0-100 — how confident this will work
    fallbackPlan?: TechniqueOption;
};

type DataQualityReport = {
    adequate: boolean;
    missing: DataRequirement[];
    compromised: DataRequirement[];
    notes: string[];
};

type InterpretedNote = {
    originalNote: string;
    directorFear: string;        // Diagnosed "note behind the note"
    technicalAction: string;     // What to do about it
    priority: Priority;
};
```

**Key interface contract:** The VFXSupervisor owns the TRANSLATION function — it is the only system that can convert creative intent into technical instructions AND technical results back into creative evaluations. It also owns the VFX quality GATE (approve/reject before client delivery), but this gate operates within the scope defined by the Film Director's creative vision.

---

## 6. System Interaction Diagrams

### 6.1 Feedback Flow: Braintrust → Director

```
Timeline: Every ~2-4 months during production

  Director                       Braintrust                    Producer
     |                              |                              |
     |--- WorkInProgress ---------->|                              |
     |--- CreativeIntent ---------->|                              |
     |                              |                              |
     |                              |--- evaluateNarrative()       |
     |                              |--- identifyProblems()        |
     |                              |--- suggestDirections()       |
     |                              |--- headlineFeedback()        |
     |                              |                              |
     |<---- FeedbackPackage --------|                              |
     |                              |                              |
     |--- resolveFeedback() ------->|                              |
     |                              |                              |
     |--- evaluateFeedback() ---->[INTERNAL]                       |
     |--- convert to directives -->[Department Leads]              |
```

**Key:** Braintrust output flows ONLY to Director. Director decides which feedback to act on. Braintrust has NO connection to executing departments.

### 6.2 Approval Flow: Film Director Gate

```
  Director                       Department                     Pipeline
     |                              |                              |
     |                              |--- submitShot() ------------>|
     |<---- shotForReview ---------|                              |
     |                              |                              |
     |--- approveShot() ----------->|                              |
     |      OR                      |                              |
     |--- rejectShot() ------------>|                              |
     |                              |                              |
     |                              |--- (if approved) ----------->| [Next Stage]
     |                              |--- (if rejected) ----------->| [Rework Loop]
```

**Key:** Approval is a binary gate. No ambiguity. "Approved" means proceed. "Rejected" means rework.

### 6.3 Shared Direction: CreativeDirector ↔ GameDirector

```
  CreativeDirector                GameDirector                  Team
     |                              |                              |
     |--- setEmotionalIdentity()    |                              |
     |                              |--- validateFeasibility()     |
     |<---- feasibilityCheck -------|                              |
     |                              |                              |
     |--- evaluateQuality() ------->|                              |
     |                              |--- adjustScope()             |
     |                              |                              |
     |                              |--- Joint Directive --------->| [All Disciplines]
```

**Key:** CD and GD are co-equal in their domains. CD says "what feels right." GD says "what we can deliver." Neither can fully override the other.

### 6.4 Translation Bridge: VFXSupervisor Pipeline

```
  Film Director                   VFXSupervisor                  VFX Departments
     |                              |                              |
     |--- CreativeBrief ----------->|                              |
     |                              |                              |
     |                              |--- translateCreativeToTechnical()
     |                              |                              |
     |                              |--- TechnicalDirection ------>| [Matchmove]
     |                              |--- TechnicalDirection ------>| [Modeling]
     |                              |--- TechnicalDirection ------>| [FX]
     |                              |--- TechnicalDirection ------>| [Lighting]
     |                              |                              |
     |                              |<---- DepartmentResults ------|
     |                              |                              |
     |                              |--- translateTechnicalToCreative()
     |                              |                              |
     |--- ShotPresentations -------|                              |
     |                              |                              |
     |--- ClientNotes ------------->|                              |
     |                              |--- interpretClientNotes()    |
     |                              |--- TechnicalDirection ------->| [Revise]
```

**Key:** VFXSupervisor is the ONLY connection between Film Director and the executing VFX pipeline. This insulating layer prevents the director from making technically infeasible demands and prevents the pipeline from producing work that doesn't match the creative intent.

---

## 7. Cross-System Comparison Matrix

### 7.1 Authority Types

| Dimension | Braintrust | FilmDirector | CreativeDirector | VFXSupervisor |
|-----------|-----------|-------------|------------------|---------------|
| **Authority type** | Influence (zero binding) | Absolute creative | Shared directional | Execution + Translation |
| **Can approve?** | NO | YES (final on all) | YES (creative quality only) | YES (VFX shots before client) |
| **Can reject?** | NO | YES | YES (quality only) | YES (VFX pipeline only) |
| **Can mandate?** | NO | YES (creative) | Partial (directional) | Partial (on-set + pipeline) |
| **Can block?** | NO | YES (by not approving) | YES (quality gate) | YES (VFX quality gate) |
| **Can ignore?** | N/A (output is optional input) | YES (ignores Braintrust) | YES (if overridden by GameDirector) | YES (if overridden by Film Director) |

### 7.2 Input/Output Symmetry

| Dimension | Braintrust | FilmDirector | CreativeDirector | VFXSupervisor |
|-----------|-----------|-------------|------------------|---------------|
| **Primary input** | Work + Intent | Script + Proposals | Design + Prototypes | Director vision + On-set data |
| **Primary output** | Feedback signals | Approved/rejected shots | Quality evaluations | Technical direction |
| **Output binding?** | No | Yes | Partially | Yes (within scope) |
| **Feedback loops?** | Outgoing only | Incoming from BT + Incoming from departments | Incoming from playtests, outgoing to disciplines | Bidirectional (creative ↔ technical) |

### 7.3 Dependency Architecture

| System | Depends On | Depended Upon By |
|--------|-----------|------------------|
| Braintrust | Director (work to review), Producer (facilitation) | Director (optional) |
| FilmDirector | Screenwriter, Producer, Dept Leads, Braintrust (optional) | ALL departments |
| CreativeDirector | GameDirector, Art Director, Writers, Playtest system | Art, Narrative, Audio, Design |
| VFXSupervisor | Film Director, CG Supervisor, VFX Producer | All VFX departments |

### 7.4 Failure Mode Comparison

| Failure Class | Braintrust | FilmDirector | CreativeDirector | VFXSupervisor |
|--------------|-----------|-------------|------------------|---------------|
| **Authority drift** | Starts issuing de facto commands | Delegates core decisions | Overrides GameDirector on scope | Approves without quality check |
| **Bottleneck** | N/A (no gate) | Approval backlog | Quality evaluation backlog | Single review gate |
| **Quality degradation** | Becomes too polite (loss of candor) | Vision becomes unclear | Quality bar drifts | Translation fidelity degrades |
| **Communication failure** | Feedback too vague | Vision not articulated | Direction not actionable | Creative intent lost in translation |
| **Resource misalignment** | N/A | Approves without constraint awareness | Demands quality without scope context | Accepts too much work |

---

## 8. Architectural Patterns & Transferable Insights

### 8.1 The Separation of Feedback from Approval (Most Important Pattern)

**The insight:** In most creative systems, the person giving feedback is also the person who can say "no." This conflates two fundamentally different functions:

- **Feedback:** The generation of improvement signals. Requires candor, expertise, and safety.
- **Approval:** The binding decision to proceed. Requires authority, accountability, and judgment.

**When these are combined:**
- Feedback becomes cautious (fear of consequences of a "no")
- Approval becomes defensive (attached to personal ownership of work)
- The system optimizes for safety over excellence

**When these are separated (Pixar's model):**
- Feedback is maximally candid (no consequence)
- Approval is maximally decisive (no defensiveness)
- The system optimizes for truth over harmony

**How to implement in software:**

```
// Anti-pattern: Reviewer both reviews AND merges
class AntiPatternReviewer {
    review(code): Comments;
    approve(code): Boolean;    // Same person both suggests AND blocks
    merge(code): void;          // Same person changes state
}

// Pattern: Separate Feedback from Gate functions
class BraintrustReviewer {
    review(work): FeedbackPackage;  // Read-only, zero side effects
    // Has NO approve() or merge() methods
}

class DirectorApprover {
    approve(work, feedback?): Decision;  // Gate function, owns state change
    // May or may not consider feedback
}
```

### 8.2 The Translation Layer Pattern (VFXSupervisor)

The VFX Supervisor is a **bidirectional translation layer** between two systems that cannot communicate directly:

- **Creative System** (Director): Speaks in emotions, intentions, and artistic references
- **Technical System** (Pipeline): Speaks in parameters, constraints, and render budgets

Without this layer:
- Creative demands become technically infeasible
- Technical output becomes creatively irrelevant

With this layer:
- Creative intent is converted into actionable technical specs
- Technical results are converted back into creative evaluations
- Both systems can operate in their native language

**Software analogy:** An API Gateway that translates between a RESTful frontend and a gRPC/Protobuf backend. Each side speaks its own protocol; the gateway handles the transformation.

### 8.3 The Heart vs. Spine Pattern (CreativeDirector + GameDirector)

The Creative Director / Game Director split creates a healthy tension:

- **CreativeDirector (Heart):** Pushes quality, emotional truth, artistic ambition
- **GameDirector (Spine):** Pushes feasibility, scope discipline, delivery reality

Each has authority in their domain but cannot fully override the other. This creates a **constraint satisfaction system** where the final output must satisfy both:
- Pass the CD's quality bar ("does this feel right?")
- Pass the GD's feasibility bar ("can we deliver this?")

**Software analogy:** A multi-objective optimizer with two competing objective functions. No single solution dominates; the optimal solution is found at the Pareto frontier where both objectives are balanced.

### 8.4 The Candor Contract (Braintrust Operating Principle)

The Braintrust's effectiveness depends on a **psychological safety contract** that is explicitly maintained:

```
CandorContract = {
    rules: [
        "You are not your idea" (decouple identity from work),
        "Focus on problems, not solutions" (diagnose before prescribe),
        "No authority to mandate" (feedback is suggestion, not command),
        "Candor is required, not optional" (silence is failure),
        "Headline: what to blow up, what to love" (prioritize)
    ],
    enforcer: Producer (maintains the compact),
    violationResponse: "Session pause and reset"
};
```

**Software analogy:** An explicit protocol contract between services. If the Braintrust service starts returning commands instead of suggestions, the producer service throws a protocol violation error.

### 8.5 Summary: When to Use Each Pattern

| Pattern | Use When | Avoid When |
|---------|----------|------------|
| Feedback ≠ Approval | Psychological safety is critical; you need maximum candor | Speed is the only priority; feedback slows things down |
| Translation Layer | Two systems speak fundamentally different languages | Both sides already share a common language |
| Heart + Spine Split | Quality and feasibility are in tension; you need balanced outcomes | One dimension clearly dominates (e.g., pure technical project) |
| Candor Contract | Team is risk-averse and needs permission to critique | Team already has a healthy critique culture |

---

## Appendix A: Glossary

| Term | Definition |
|------|-----------|
| **Finalling (Finalling a shot)** | The director's binding approval that a shot is complete and can move forward in the pipeline |
| **Dailies** | Daily review sessions where work-in-progress is presented for feedback and approval |
| **Headlining** | The Braintrust technique of distilling feedback into "what to blow up" (critical issues) and "what to love" (what's working) |
| **The Ugly Baby** | Early-stage creative work that is unformed, fragile, and ugly but has potential — needs protection |
| **The Hungry Beast** | The business/process side — schedules, budgets, deliverables — that demands to be fed |
| **The Note Behind the Note** | Diagnosing what an executive/feedback-giver is really afraid of, beneath the surface of their note |
| **Vertical Slice** | A playable/demoable chunk of the game that demonstrates final quality across all dimensions |
| **Core Loop** | The fundamental cycle of action the player repeats throughout a game |
| **Story-Mech Alignment** | The degree to which narrative and gameplay reinforce rather than contradict each other |
| **AOVs** | Arbitrary Output Variables — separate render passes (diffuse, specular, SSS, z-depth) that give compositors control |

## Appendix B: Source Documents

This specification synthesizes research from:
- `Pixar_Production_Pipeline.md` — Braintrust operation, Director authority, pipeline stages
- `Directors_Creative_Leadership.md` — Director mental frameworks, communication vocabulary, creative decision patterns
- `Game_Studio_Pipeline.md` — Creative Director vs Game Director split, iterative development, feedback culture
- `VFX_House_Pipeline.md` — VFX Supervisor role, translation function, on-set protocols, client-driven model
- `Specialist_Capability_Domains.md` — Capability decomposition of all specialist roles across 7 domains
