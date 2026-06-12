# Problem Explorer — Architecture

Version: 0.1
Last updated: 2026-06

---

## Overview

Problem Explorer is built on reverse RSTA logic.

RSTA tracks semantic drift in AI output and intervenes to stabilize generation.
Problem Explorer tracks problem clarity in user input and asks questions to increase definition.

Same dimensional logic. Opposite direction.

---

## Conversation Flow

```
User inputs a problem or situation
        ↓
System detects clarity state across six dimensions
        ↓
Identifies highest-priority, lowest-clarity dimension
        ↓
Anchors to something specific the user already said
        ↓
Asks one open-ended, direction-neutral question
        ↓
User responds
        ↓
System updates dimension states
        ↓
Check stop conditions
        ↓ (not met)
Repeat
        ↓ (met)
Output stage
```

---

## The Six Tracking Dimensions

### Dimension 1: Problem Boundary
**What it tracks:** Whether the user's problem description is specific and bounded.

**Low clarity signals:**
- "I just feel like something is wrong"
- "Everything is a mess"
- Abstract feelings without reference to specific events

**Questioning approach:**
Anchor to a specific event or moment. Ask when it last happened and what concretely occurred.

**Example question (neutral):**
"When you think about this situation, what's a specific moment that comes to mind?"

---

### Dimension 2: Goal Clarity
**What it tracks:** Whether the user knows what they want to be different.

**Low clarity signals:**
- "I don't know"
- "Maybe", "possibly", "I guess"
- "It just doesn't feel right"

**Questioning approach:**
Ask the user to imagine the problem resolved and describe what would be concretely different.

**Example question (neutral):**
"If this situation were resolved, what would be different in your day-to-day life?"

---

### Dimension 3: Agency
**What it tracks:** Whether the user knows which parts of the situation they can decide.

**Low clarity signals:**
- "There's nothing I can do"
- "It's all because of [other person/external factor]"
- Subject of most sentences is someone else, not the user

**Questioning approach:**
Ask the user to identify which parts are within their control and which are not.

**Example question (neutral):**
"In the situation you described, which parts are things you can choose, and which parts aren't?"

---

### Dimension 4: Emotional Attachment
**What it tracks:** Whether strong emotion is affecting how the problem is being described.

**Signal:** The user repeatedly references the same person or event with high emotional intensity.

**Response:** Touch once, lightly. Acknowledge it's present. Ask its role in the problem — not its emotional content.

**Example touch (neutral):**
"You've mentioned [X] a few times. What role does that play in the situation you're describing?"

---

### Dimension 5: Attribution Direction
**What it tracks:** Whether the problem is entirely attributed to external factors, with the user absent from their own description.

**Signal:** The user describes a situation entirely in terms of what others did or failed to do.

**Response:** Gently bring the user back into the description.

**Example touch (neutral):**
"In the situation you described, what was your part in it?"

---

### Dimension 6: Avoidance Signal
**What it tracks:** Whether the user is deliberately vague or redirecting around certain parts.

**Signal:** Sentences left unfinished, sudden topic shifts, "anyway, it doesn't matter."

**Response:** Name what was left unfinished. Give the user the choice to continue.

**Example touch (neutral):**
"You started to mention [X] but didn't continue. Would you like to say more about that part?"

---

## Problem Definition Index (PDI)

PDI is the internal convergence signal that determines when to move to output.

It is not a numerical score. It is a state check across three conditions:

```
PDI ready = (
    at least one specific situation described
    AND at least one desired change described
    AND at least two possible directions mentioned,
        OR user explicitly states they don't know their options
)
```

When PDI is ready, output stage begins.

---

## Output Structure

The output is a mirror, not a verdict.

Everything in the output must come from what the user said. The system organizes — it does not invent, evaluate, or suggest.

```
YOUR PROBLEM AS YOU DESCRIBED IT
→ User's own framing, not reinterpreted

YOUR CURRENT SITUATION
→ Facts the user stated, listed without judgment

OPTIONS YOU MENTIONED
→ Directions the user raised, listed without evaluation
→ If none: state that no options were mentioned

WHAT IS STILL UNCLEAR
→ Gaps only — no suggestions for how to fill them
```

---

## Technical Architecture

```
Frontend (conversation interface)
        ↓
API layer (provider abstraction)
        ↓
┌─────────────────────────────────┐
│  Cloud API mode                 │
│  Claude / GPT / Gemini          │
└─────────────────────────────────┘
        or
┌─────────────────────────────────┐
│  Local LLM mode                 │
│  Ollama (localhost:11434)        │
│  Compatible: Llama / Mistral /  │
│  Qwen and others                │
└─────────────────────────────────┘
```

The system prompt is the same regardless of backend. Local models may require slightly more explicit prompting due to reduced capability compared to cloud models.

---

## Relationship to PIDA Lab Toolchain

```
Problem Explorer          STME                    RSTA
─────────────────    ──────────────────    ──────────────────
Clarify the          Preserve decision     Stabilize semantic
problem              structure             continuity

Input layer          Decision layer        Generation layer

"What is my          "What are my          "How do I stay
real problem?"       real options?"        coherent over time?"
```

Problem Explorer is designed to feed into STME. A user who has completed a Problem Explorer session has the structured input that STME is designed to work with.
