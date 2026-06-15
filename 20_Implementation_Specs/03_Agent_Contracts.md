# COS Implementation Specifications — Agent Contracts

**Date:** June 15, 2026
**Author:** Chioma (Systems Architect)
**Reference:** [Creative_Roles_as_Functions.md](../06_Agent_Architecture/Creative_Roles_as_Functions.md), [COS_Architecture_v4_Creativity_First.md](../01_Capability_Architecture/COS_Architecture_v4_Creativity_First.md) §3.3

---

## 1. Orchestrator Agent

The orchestrator is not a creative function — it is the execution coordinator. It sequences agent calls, manages state transitions, and enforces the workflow.

**Not a specialist.** The orchestrator is a router, not a creative agent.

```
interface Orchestrator {
    // Entry point
    runWorkflow(raw_input: string, project_id: string): Promise<WorkflowResult>;
    
    // Workflow lifecycle
    startWorkflow(project_id: string): Promise<void>;
    getWorkflowStatus(project_id: string): WorkflowStatus;
    cancelWorkflow(project_id: string): Promise<void>;
    
    // Agent coordination
    invokeAgent(agent_id: AgentID, payload: AgentPayload): Promise<AgentResult>;
    handleError(work_item_id: string, error: Error): Promise<void>;
    
    // State persistence
    saveCheckpoint(project_id: string): Promise<string>;  // returns checkpoint path
    loadCheckpoint(checkpoint_path: string): Promise<WorkflowState>;
}
```

**State diagram (orchestrator level):**

```
IDLE → INTAKE → FRAMING → EXPLORATION → SELECTION → REALIZATION → EVALUATION → [APPROVED | REVISION → REALIZATION] → COMPLETE
```

---

## 2. Frame Agent Contract

**Creative Function:** Framing — "Defining what needs to be created, constraints, and success criteria"

**Composed from AGE^T:** Attend(raw_input) + Generate(intent_structure) + Evaluate(completeness) + Transform(clarify_gaps)

```
interface FrameAgent {
    // Primary
    frameIntent(input: {
        raw_text: string,
        references?: ImageRef[],
        constraints?: Constraint[]
    }): Promise<FramingResult>;
    
    // Clarification loop
    identifyGaps(intent_token: IntentToken): Promise<Gap[]>;
    askQuestion(gap: Gap): Promise<Question>;
    incorporateAnswer(intent_token: IntentToken, answer: Answer): Promise<IntentToken>;
    
    // Validation
    validateCompleteness(intent_token: IntentToken): Promise<ValidationReport>;
}

type FramingResult = {
    intent_token: IntentToken;
    confidence: number;           // 0.0-1.0 — how confident the frame is complete
    gaps_identified: Gap[];       // questions still needing answers
    suggested_beats: Beat[];      // parsed story beats from the input
};

type Gap = {
    field: string;
    reason: string;
    question: string;
    severity: 'blocking' | 'optional';
};

type ValidationReport = {
    is_complete: boolean;
    missing_fields: string[];
    ambiguous_fields: string[];
    confidence_score: number;
};
```

**MVP Notes:**
- Frame agent is a prompt to an LLM, not a standalone service
- Gaps are identified by evaluating Intent Token completeness against required fields
- Clarification loop is optional — only triggers if confidence < 0.7

---

## 3. Explore Agent Contract

**Creative Function:** Exploration — "Generating possibilities without commitment"

**Composed from AGE^T:** Attend(domain/constraints) + Generate(many variations) + Evaluate(loose criteria)

```
interface ExploreAgent {
    // Primary
    exploreVariations(input: {
        intent_token: IntentToken,
        beat: BeatDescription,
        count: number           // number of options to generate (default: 5)
    }): Promise<ExplorationResult>;
    
    // Variation expansion
    expandDirection(input: {
        intent_token: IntentToken,
        seed_option: PanelOption,
        count: number
    }): Promise<ExplorationResult>;
}

type ExplorationResult = {
    beat_id: string;
    options: PanelOption[];
    generation_report: {
        total_generated: number;
        quality_filtered: number;
        diversity_score: number;
    };
};

type PanelOption = {
    id: string;
    image_url?: string;       // may be null if using pure text generation
    description: string;
    camera_note: string;
    composition: 'wide' | 'medium' | 'close_up' | 'extreme_close_up';
    timing: string;
    emotional_target: string;
    confidence: number;        // 0.0-1.0 — self-assessed match to intent
};
```

**MVP Notes:**
- For MVP, "exploration" is text-based: Explore Agent generates text descriptions of 5 possible panel compositions
- Image generation is deferred to the Realize Agent
- Diversity scoring is simple: deduplicate similar descriptions, ensure each option explores a different aspect

---

## 4. Select Agent Contract

**Creative Function:** Selection — "Converging on a direction. Choosing among possibilities."

**Composed from AGE^T:** Attend(options, user_preference)

```
interface SelectAgent {
    // Primary
    presentOptions(input: {
        exploration_result: ExplorationResult,
        user_id: string
    }): Promise<Presentation>;
    
    // User interaction
    recordSelection(input: {
        presentation_id: string,
        selected_option_id: string,
        user_feedback?: string
    }): Promise<SelectionResult>;
}

type Presentation = {
    presentation_id: string;
    beat_id: string;
    options: PanelOption[];
    display_hints: {
        show_individual: boolean;    // true — show each option
        sort_by?: 'diversity' | 'confidence';
    };
};

type SelectionResult = {
    selected_option: PanelOption;
    runner_up?: PanelOption;
    user_feedback?: string;
    updated_intent_token: IntentToken;
};
```

**MVP Notes:** Selection is always human-mediated in MVP. The agent presents options and records the choice. No auto-selection logic.

---

## 5. Realize Agent Contract

**Creative Function:** Realization — "Manifesting an idea into a tangible form"

**Composed from AGE^T:** Attend(focus) + Generate(form) + Evaluate(against_intent) + Transform(adjust)

```
interface RealizeAgent {
    // Primary
    realize(input: {
        intent_token: IntentToken,
        beat_id: string,
        selected_option: PanelOption,
        quality_target: number
    }): Promise<RealizationResult>;
    
    // Iteration — triggered by Evaluate feedback
    refine(input: {
        existing_panel: Panel,
        feedback: string,
        intent_token: IntentToken
    }): Promise<RealizationResult>;
}

type RealizationResult = {
    beat_id: string;
    panels: Panel[];
    generation_log: {
        model_used: string;
        prompt: string;
        parameters: object;
        generation_time_ms: number;
    };
    self_evaluation: {
        intent_match: number;
        technical_quality: number;
    };
};

type Panel = {
    id: string;
    image_path: string;
    description: string;
    camera_note: string;
    timing_seconds: number;
    metadata: {
        prompt: string;
        seed: number;
        model: string;
        generation_params: object;
    };
};
```

**MVP Notes:**
- Realize Agent calls a single image generation API (e.g., Stable Diffusion, DALL-E)
- Self-evaluation is a lightweight LLM check: "Does this panel match the beat description?"
- Refine uses the same API with adjusted prompt based on feedback

---

## 6. Evaluate Agent Contract

**Creative Function:** Evaluation — "Judging quality against intent"

**Composed from AGE^T:** Evaluate(against_intent)

```
interface EvaluateAgent {
    // Primary
    evaluate(input: {
        intent_token: IntentToken,
        panels: Panel[],
        criteria: QualityCriteria
    }): Promise<EvaluationResult>;
    
    // Comparison
    compare(input: {
        option_a: Panel,
        option_b: Panel,
        criteria: QualityCriteria
    }): Promise<Comparison>;
    
    // Good-enough detection
    assessDiminishingReturns(input: {
        iteration_history: Iteration[],
        current_scores: QualityScores
    }): Promise<ReturnAssessment>;
}

type EvaluationResult = {
    beat_id: string;
    scores: QualityScores;
    overall: number;
    feedback: FeedbackItem[];
    recommendation: 'approve' | 'revise' | 'restructure';
};

type QualityScores = {
    silhouette_readability: number;
    emotional_beat_clarity: number;
    narrative_coherence: number;
    pacing_rhythm: number;
    tonal_consistency: number;
};

type FeedbackItem = {
    criterion: string;
    score: number;
    what_works: string;
    what_to_improve: string;
    suggested_direction: string;  // NOT a specific solution — per Braintrust principle
};

type Comparison = {
    winner: string;            // panel id
    rationale: string;
    differences: string[];
};

type ReturnAssessment = {
    diminishing_returns_detected: boolean;
    improvement_trend: 'improving' | 'flat' | 'degrading';
    recommended_action: 'continue' | 'accept_current' | 'change_approach';
};
```

**MVP Notes:** Evaluate agent recommends only — the Director always has final say (Braintrust pattern from [Creative_Roles_as_Functions.md](../06_Agent_Architecture/Creative_Roles_as_Functions.md) §2).

---

*Next document: [04_Memory_Architecture.md](04_Memory_Architecture.md)*
