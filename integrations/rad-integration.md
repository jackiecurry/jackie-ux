# RAD + Jackie UX — Integration Guide

## What This Integration Does

Jackie UX Agent and RAD address different layers of the same problem. RAD provides the component vocabulary for building responsible agentic interfaces. Jackie UX provides the reasoning layer for evaluating whether a design decision is actually sound — not just compliant with a checklist.

Used together, RAD tells you *what to build*. Jackie UX tells you *whether the way you are building it is correct*.

---

## When to Use Each

| Situation | Use |
|---|---|
| Selecting which components to include in an agentic interface | RAD (`/rad:suggest`) |
| Evaluating whether a specific design decision is defensible | Jackie UX |
| Auditing an existing interface for compliance gaps | RAD (`/rad:audit`) |
| Pressure-testing a design direction before finalizing | Jackie UX (Provocative Mode) |
| Understanding what a component does and when to use it | RAD (`/rad:explain`) |
| Analyzing the trade-offs between two RAD-compliant approaches | Jackie UX (Strategic Mode) |
| Getting scaffolding for a specific component | RAD (`/rad:new`) |
| Determining if a design decision satisfies user needs, not just RAD rules | Jackie UX |

---

## Setup

### Step 1: Install the RAD Plugin

Copy the `rad-plugin` directory into your project or `~/.claude/plugins/` to activate RAD commands in Claude Code.

```
~/.claude/plugins/rad-plugin/
├── .claude-plugin/
└── commands/
    ├── suggest.md
    ├── audit.md
    ├── new.md
    └── explain.md
```

### Step 2: Configure Jackie UX as a Claude Project

1. Open [claude.ai](https://claude.ai) and create a new Project named "Jackie UX — RAD"
2. Paste the contents of `prompts/system-prompt.md` into the Project Instructions
3. Upload `knowledge/rad-design-system.md` as a Project knowledge file

This gives the agent direct access to the full RAD component catalog and design rules during every conversation.

### Step 3 (API): Inject RAD Knowledge into the System Prompt

For API usage, concatenate the RAD knowledge document into the system prompt:

```python
import anthropic

with open("prompts/system-prompt.md", "r") as f:
    system_prompt = f.read()

with open("knowledge/rad-design-system.md", "r") as f:
    rad_knowledge = f.read()

combined_system = f"{system_prompt}\n\n---\n\n## RAD Design System Reference\n\n{rad_knowledge}"

client = anthropic.Anthropic(api_key="your-api-key")

response = client.messages.create(
    model="claude-opus-4-6",
    max_tokens=2048,
    system=combined_system,
    messages=[
        {
            "role": "user",
            "content": "Use Strategic Mode. I'm designing an agent that sends emails on the user's behalf. Which RAD components are non-negotiable, and what are the trade-offs in how I implement HC01?"
        }
    ]
)

print(response.content[0].text)
```

---

## Workflow Patterns

### Pattern 1: Component Selection → Reasoning Evaluation

Use RAD to identify what components apply, then use Jackie UX to evaluate whether the implementation direction is sound.

```
Step 1 (Claude Code): /rad:suggest
→ "I'm building an AI that reads and categorizes a user's email inbox"

Step 2 (Jackie UX, Strategic Mode):
→ "RAD suggests HC04 (Consent & Scope Gates) and CM01 (Context Sources) for
   an inbox agent. I'm considering surfacing consent once at onboarding rather
   than at each new access request. What are the trade-offs?"
```

### Pattern 2: Audit → Targeted Interrogation

Use RAD to surface compliance gaps, then use Jackie UX to decide which gaps are worth addressing first given your constraints.

```
Step 1 (Claude Code): /rad:audit
→ Identifies: missing TD06 (Algorithmic Nudge Disclosure) and AA01 (Audit Trail)

Step 2 (Jackie UX, Direct Mode):
→ "We have engineering capacity for one of these: TD06 or AA01.
   We're a B2C consumer app, not enterprise. Which do I prioritize?"
```

### Pattern 3: Assumption Challenge Before Ship

Run Provocative Mode against any design you feel confident about before finalizing.

```
Jackie UX, Provocative Mode:
→ "We've implemented HC01 as a single confirmation modal before the agent
   runs a 12-step task that takes 4 minutes. Challenge this."
```

### Pattern 4: Trade-Off Analysis Between RAD-Compliant Approaches

Multiple implementations can be RAD-compliant. Jackie UX evaluates which is better for your specific context.

```
Jackie UX, Strategic Mode:
→ "For surfacing AI confidence (TD04), I'm choosing between:
   (A) a percentage confidence score next to each output, or
   (B) a three-tier label (High / Medium / Low confidence).
   My users are non-technical procurement managers. Which is stronger?"
```

---

## Starter Prompts for RAD + Jackie UX

These prompts are structured for users who have RAD knowledge loaded into the agent:

**Component selection reasoning:**
"I'm building [describe agentic feature]. RAD suggests [component IDs]. Walk me through the trade-offs in how I implement [specific component] given [constraint]."

**Compliance gap prioritization:**
"A RAD audit flagged [list of missing components] in our [product type]. We have limited engineering capacity. What's the correct prioritization and why?"

**Dark pattern detection:**
"Describe the interface: [describe current implementation]. Does this violate any RAD principles? Identify specific components we are omitting or misimplementing."

**User trust evaluation:**
"Our agent [describe what it does]. A user who has never used it before encounters [describe the current experience]. Where does trust break down, and which RAD components address those break points?"

**Pre-ship stress test:**
"We're shipping [describe feature] next week. Use Provocative Mode to find the RAD compliance failure we haven't seen yet."

---

## What Jackie UX Will Not Do That RAD Does

- Generate component scaffolding or markup (`/rad:new` does this)
- Produce a structured audit list of specific compliance gaps (`/rad:audit` does this)
- Provide a component catalog with precise implementation specs (`/rad:explain` does this)

Jackie UX reasons about design decisions. RAD generates design artifacts. The boundary is clear: use the right tool for the right layer.
