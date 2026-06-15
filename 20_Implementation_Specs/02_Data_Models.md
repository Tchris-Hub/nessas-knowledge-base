# COS Implementation Specifications — Data Models

**Date:** June 15, 2026
**Author:** Chioma (Systems Architect)
**Reference:** [COS_Architecture_v4_Creativity_First.md](../01_Capability_Architecture/COS_Architecture_v4_Creativity_First.md) §6.3 — Intent Token

---

## 1. Intent Token Schema (v1.0 — MVP)

The Intent Token is the spine of the system. Every agent reads from it, writes state updates to it, and validates output against it.

**Format:** JSON file, stored at `./projects/{project_id}/intent_token.json`

```json
{
  "$schema": "cos-intent-token-v1.schema.json",
  "meta": {
    "id": "cos-20260615-storyboard-001",
    "project": "fantasy-quest-opening",
    "created_at": "2026-06-15T14:30:00Z",
    "updated_at": "2026-06-15T15:45:00Z",
    "version": 1
  },

  "intent": {
    "domain": "storyboard",
    "subject": "fantasy quest opening scene",
    "script": "A young hero wakes in a small village at dawn. The village is quiet, mist hangs over the thatched roofs. They pack a bag, take an old sword from a hiding place, and leave without waking anyone. The camera follows them through the village gates into a vast unknown landscape beyond.",

    "mood": ["hopeful", "melancholic", "mysterious"],
    "style": "cinematic realism with warm golden-hour light",
    "audience": "film pre-visualization, director's pitch deck",
    "quality_bar": "concept-level clarity — narrative beats must be readable, visual polish secondary",

    "constraints": {
      "panel_count": { "min": 5, "max": 15, "recommended": 8 },
      "aspect_ratio": "16:9",
      "format": "png",
      "output_dir": "./output/fantasy-quest-opening/"
    }
  },

  "state": {
    "stage": "exploration",
    "overall_completion": 0.3,
    "intent_fidelity": 0.0,
    "agents_engaged": ["frame_agent"],
    "agents_completed": ["frame_agent"]
  },

  "history": [
    {
      "timestamp": "2026-06-15T14:30:00Z",
      "event": "intent_formed",
      "actor": "frame_agent",
      "detail": "Parsed user pitch into structured Intent Token",
      "intent_fidelity": 0.85
    }
  ],

  "storyboard": {
    "beats": [
      {
        "id": "beat-01",
        "description": "Wide shot of sleeping village at dawn, mist over thatched roofs",
        "status": "pending",
        "panels": [],
        "evaluation": null
      },
      {
        "id": "beat-02",
        "description": "Interior shot of hero waking, golden light through window",
        "status": "pending",
        "panels": [],
        "evaluation": null
      },
      {
        "id": "beat-03",
        "description": "Hero packs bag, takes old sword from hiding place",
        "status": "pending",
        "panels": [],
        "evaluation": null
      },
      {
        "id": "beat-04",
        "description": "Hero leaves through village gates, looks back one last time",
        "status": "pending",
        "panels": [],
        "evaluation": null
      },
      {
        "id": "beat-05",
        "description": "Wide shot of hero walking into vast landscape beyond village",
        "status": "pending",
        "panels": [],
        "evaluation": null
      }
    ]
  },

  "iterations": [
    {
      "iteration": 0,
      "agent": "explore_agent",
      "timestamp": "2026-06-15T15:00:00Z",
      "options": 5,
      "selected": 2,
      "notes": "User selected option 2 — 'more dramatic light through mist'"
    }
  ],

  "quality": {
    "criteria": {
      "silhouette_readability": { "score": null, "weight": 0.2 },
      "emotional_beat_clarity": { "score": null, "weight": 0.3 },
      "narrative_coherence": { "score": null, "weight": 0.3 },
      "pacing_rhythm": { "score": null, "weight": 0.1 },
      "tonal_consistency": { "score": null, "weight": 0.1 }
    },
    "overall_score": null,
    "assessments": []
  }
}
```

### Intent Token JSON Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "$id": "cos-intent-token-v1",
  "type": "object",
  "required": ["meta", "intent", "state", "history"],
  "properties": {
    "meta": {
      "type": "object",
      "required": ["id", "project", "created_at"],
      "properties": {
        "id": { "type": "string", "pattern": "^cos-\\d{8}-[a-z-]+-\\d{3}$" },
        "project": { "type": "string" },
        "created_at": { "type": "string", "format": "date-time" },
        "updated_at": { "type": "string", "format": "date-time" },
        "version": { "type": "integer", "minimum": 1 }
      }
    },
    "intent": {
      "type": "object",
      "required": ["domain", "subject", "script"],
      "properties": {
        "domain": { "type": "string", "enum": ["storyboard", "environment", "character", "cinematic_shot"] },
        "subject": { "type": "string" },
        "script": { "type": "string" },
        "mood": { "type": "array", "items": { "type": "string" } },
        "style": { "type": "string" },
        "audience": { "type": "string" },
        "quality_bar": { "type": "string" },
        "constraints": {
          "type": "object",
          "properties": {
            "panel_count": {
              "type": "object",
              "properties": {
                "min": { "type": "integer" },
                "max": { "type": "integer" },
                "recommended": { "type": "integer" }
              }
            },
            "aspect_ratio": { "type": "string" },
            "format": { "type": "string" },
            "output_dir": { "type": "string" }
          }
        }
      }
    },
    "state": {
      "type": "object",
      "required": ["stage"],
      "properties": {
        "stage": { 
          "type": "string", 
          "enum": ["intake", "framing", "exploration", "selection", "realization", "evaluation", "refinement", "approved", "rejected"] 
        },
        "overall_completion": { "type": "number", "minimum": 0, "maximum": 1 },
        "intent_fidelity": { "type": "number", "minimum": 0, "maximum": 1 },
        "agents_engaged": { "type": "array", "items": { "type": "string" } },
        "agents_completed": { "type": "array", "items": { "type": "string" } }
      }
    },
    "history": {
      "type": "array",
      "items": {
        "type": "object",
        "required": ["timestamp", "event", "actor"],
        "properties": {
          "timestamp": { "type": "string", "format": "date-time" },
          "event": { "type": "string" },
          "actor": { "type": "string" },
          "detail": { "type": "string" },
          "intent_fidelity": { "type": "number", "minimum": 0, "maximum": 1 }
        }
      }
    },
    "storyboard": {
      "type": "object",
      "properties": {
        "beats": {
          "type": "array",
          "items": {
            "type": "object",
            "required": ["id", "description", "status"],
            "properties": {
              "id": { "type": "string" },
              "description": { "type": "string" },
              "status": { "type": "string", "enum": ["pending", "exploring", "generating", "evaluating", "approved", "revising"] },
              "panels": {
                "type": "array",
                "items": {
                  "type": "object",
                  "properties": {
                    "id": { "type": "string" },
                    "image_path": { "type": "string" },
                    "camera_note": { "type": "string" },
                    "timing": { "type": "string" },
                    "generation_params": { "type": "object" }
                  }
                }
              },
              "evaluation": {
                "type": "object",
                "properties": {
                  "silhouette_readability": { "type": "number" },
                  "emotional_clarity": { "type": "number" },
                  "narrative_coherence": { "type": "number" },
                  "notes": { "type": "string" }
                }
              }
            }
          }
        }
      }
    },
    "iterations": {
      "type": "array",
      "items": {
        "type": "object",
        "required": ["iteration", "agent", "timestamp"],
        "properties": {
          "iteration": { "type": "integer" },
          "agent": { "type": "string" },
          "timestamp": { "type": "string", "format": "date-time" },
          "options": { "type": "integer" },
          "selected": { "type": "integer" },
          "user_feedback": { "type": "string" },
          "notes": { "type": "string" }
        }
      }
    },
    "quality": {
      "type": "object",
      "properties": {
        "criteria": {
          "type": "object",
          "patternProperties": {
            "^[a-z_]+$": {
              "type": "object",
              "properties": {
                "score": { "type": ["number", "null"], "minimum": 0, "maximum": 1 },
                "weight": { "type": "number", "minimum": 0, "maximum": 1 }
              }
            }
          }
        },
        "overall_score": { "type": ["number", "null"], "minimum": 0, "maximum": 1 },
        "assessments": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "timestamp": { "type": "string", "format": "date-time" },
              "agent": { "type": "string" },
              "score": { "type": "number" },
              "notes": { "type": "string" }
            }
          }
        }
      }
    }
  }
}
```

---

## 2. Agent Message Contract

Every agent communicates via a standard message envelope:

```json
{
  "message_id": "msg-001",
  "correlation_id": "cos-20260615-storyboard-001",
  "sender": "orchestrator",
  "recipient": "frame_agent",
  "message_type": "request",
  "action": "frame_intent",
  "payload": {
    "raw_input": "Create a storyboard for...",
    "intent_token_path": "./projects/fantasy-quest-opening/intent_token.json"
  },
  "timestamp": "2026-06-15T14:30:00Z",
  "ttl_seconds": 300
}
```

Response:

```json
{
  "message_id": "msg-002",
  "correlation_id": "cos-20260615-storyboard-001",
  "sender": "frame_agent",
  "recipient": "orchestrator",
  "message_type": "response",
  "status": "success",
  "payload": {
    "intent_token_path": "./projects/fantasy-quest-opening/intent_token.json",
    "summary": "Parsed into 5 story beats. Identified mood vector: hopeful/melancholic/mysterious."
  },
  "timestamp": "2026-06-15T14:30:05Z"
}
```

---

## 3. Work Item Data Model

Represents a single unit of work in the pipeline:

```json
{
  "work_item_id": "wi-beat-01-explore",
  "project_id": "fantasy-quest-opening",
  "type": "explore_beat",
  "status": "in_progress",
  "assigned_agent": "explore_agent",
  "input": {
    "beat_id": "beat-01",
    "description": "Wide shot of sleeping village at dawn, mist over thatched roofs",
    "intent_reference": "./projects/fantasy-quest-opening/intent_token.json"
  },
  "output": null,
  "options_count": 5,
  "created_at": "2026-06-15T15:00:00Z",
  "started_at": "2026-06-15T15:00:01Z",
  "completed_at": null,
  "error": null,
  "retry_count": 0
}
```

---

## 4. Agent State File

Each agent maintains a lightweight state file:

```json
{
  "agent_id": "explore_agent",
  "status": "idle",
  "current_work": null,
  "completion_count": 0,
  "error_count": 0,
  "last_active": "2026-06-15T15:00:01Z",
  "capabilities": ["explore_variations", "generate_concepts"]
}
```

---

## 5. Capability Registry (v0 — Hardcoded for MVP)

```json
{
  "capabilities": {
    "frame_intent": {
      "agent": "frame_agent",
      "primitives": ["attend", "generate"],
      "input": "raw_text",
      "output": "intent_token",
      "domain": "universal"
    },
    "explore_beats": {
      "agent": "explore_agent",
      "primitives": ["attend", "generate", "evaluate"],
      "input": "intent_token + beat_description",
      "output": "panel_options",
      "domain": "storyboard"
    },
    "select_option": {
      "agent": "select_agent",
      "primitives": ["attend"],
      "input": "panel_options + user_preference",
      "output": "selected_option",
      "domain": "universal"
    },
    "realize_panels": {
      "agent": "realize_agent",
      "primitives": ["attend", "generate", "evaluate", "transform"],
      "input": "intent_token + selected_beat",
      "output": "panel_images",
      "domain": "storyboard",
      "tool_binding": {
        "tool": "image_generation_api",
        "binding": "Maps beat_description to image generation prompt"
      }
    },
    "evaluate_quality": {
      "agent": "evaluate_agent",
      "primitives": ["evaluate"],
      "input": "intent_token + output",
      "output": "quality_scores",
      "domain": "universal"
    }
  }
}
```

---

*Next document: [03_Agent_Contracts.md](03_Agent_Contracts.md)*
