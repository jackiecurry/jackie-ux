# RAD Design System — Knowledge Reference

RAD is a design system created by Jackie Curry for building responsible agentic AI interfaces. The system addresses the specific trust failures that emerge when AI acts on a user's behalf — taking actions, making decisions, and accessing resources without constant explicit instruction.

**Core thesis:** Most AI interface failures are not technical failures. They are disclosure failures, oversight failures, and attribution failures. RAD provides the component language to address all three.

---

## Foundational Principles

**Responsible** — Every AI action is attributable. The user can always trace what the system did and why.

**Accountable** — Human oversight is preserved. Consequential decisions require explicit human approval before execution. Auto-cancellation is acceptable; auto-approval of irreversible actions is not.

**Disclosed** — AI involvement is never hidden. Data sources, confidence levels, model involvement, and environmental costs are surfaced — not buried in settings or omitted.

These principles address a pattern failure in agentic product design: teams build capable AI systems that users cannot trust because the system gives them no basis for trust. RAD components are the mechanisms that provide that basis.

---

## Design Rules

These rules are non-negotiable in RAD-compliant interfaces:

1. **Never auto-approve consequential actions.** Auto-cancellation is the only safe default for irreversible operations. Approval must be explicit.
2. **Pre-action warnings are mandatory** for all irreversible agent actions — before execution, not after.
3. **Prompt enhancement is opt-in only.** Never silently modify a user's prompt. Enhancement is a service, not a correction.
4. **Result is primary; process is available.** When an agent produces reasoning and a deliverable, default to the deliverable. Keep the reasoning accessible but not dominant.
5. **Suggested prompts must match system capability.** Do not surface suggestions the system cannot fulfill. False capability promises destroy trust faster than missing features.

---

## Component Catalog

### Transparency & Disclosure (TD / AI)

These components address the question: *Does the user understand what the AI is doing, on what basis, and with what confidence?*

| ID | Component | When to Use |
|---|---|---|
| TD01 | Disclosure Alerts | AI is acting or has acted on the user's behalf |
| TD02 | Transparency Popovers | User needs to understand why AI made a specific decision |
| TD03 | Bias Check Prompts | Output carries statistical risk or a documented data limitation |
| TD04 | Uncertainty Indicators | Communicating model confidence at point of output |
| TD05 | Confidence Threshold Warning | Output falls below an operator-defined confidence level |
| TD06 | Algorithmic Nudge Disclosure | AI is ranking, pre-selecting, or framing choices |
| AI01 | Streaming Text Display | Token-by-token output is rendering |
| AI02 | AI Loading States | Model is reasoning, retrieving, or generating |
| AI04 | AI Error States | Timeout, refusal, hallucination, or rate limit condition |
| AI05 | Session Management | Managing context window, memory state, or session history |

**Application standard:** Transparency components are not warnings — they are explanations. The design question is not "did we disclose it?" but "did the user actually understand it?" A tooltip that surfaces after three interactions has failed the first two users who made decisions without it.

TD06 deserves specific attention: any interface that ranks, orders, or pre-selects options using an AI model is making choices that appear neutral but are not. Failure to disclose this conflates AI curation with objective presentation — a dark pattern by omission.

---

### Human Control & Oversight (HC / AI)

These components address the question: *Can the user stop, redirect, or override the agent at any meaningful point in a task?*

| ID | Component | When to Use |
|---|---|---|
| HC01 | Human-in-the-Loop Controls | Agent action requires explicit human approval |
| HC02 | Impact Assessment Toggles | Surfacing the footprint of agent runs before or during execution |
| HC03 | Agent State Indicators | Agent is actively running a multi-step task |
| HC04 | Consent & Scope Gates | Agent requests access to a new system or data source |
| HC05 | Agent Attention Triggers | Monitoring detects anomaly or scope breach |
| HC06 | Recovery & Override Controls | Agent has errored, paused, or needs intervention |
| AI06 | Feedback & Correction | User needs to signal quality or correct output |

**Application standard:** HC01 is the most commonly under-implemented component in agentic interfaces. Teams default to a "confirm or cancel" modal that appears once at task start — then the agent runs autonomously for minutes. True human-in-the-loop design means approval gates at consequential steps, not just at task initiation.

HC04 is frequently absent in agent products because permission requests feel like friction. They are friction — intentional friction that makes the cost of access legible to users. Removing it does not improve UX; it removes the user's ability to give informed consent.

---

### Accountability & Audit (AA)

These components address the question: *When something goes wrong, can the user (or operator) reconstruct what happened?*

| ID | Component | When to Use |
|---|---|---|
| AA01 | Audit Trail Widgets | Logging agent actions for accountability and review |
| AA02 | Environmental Impact Indicators | Surfacing energy, water, and carbon cost of AI inference |

**Application standard:** AA01 is a legal and operational requirement in enterprise contexts and a trust signal in consumer contexts. The design failure mode is audit trails that log everything but surface nothing — technically compliant, functionally useless. Effective audit trails distinguish between actions the system took and decisions the user made.

AA02 addresses a growing expectation gap: users are increasingly aware that AI inference carries environmental cost, and products that hide this are not neutral — they are obscuring information users might use to make different choices.

---

### Foundation (AI)

These components address the baseline interaction primitives that every agentic interface requires.

| ID | Component | When to Use |
|---|---|---|
| AI03 | Prompt Input | Primary text input for AI interaction |
| AI07 | Empty & First-Run States | Zero state or first-time user onboarding |
| AI08 | AI Artifacts | Displaying AI-generated documents, code, charts, or other structured output |

**Application standard:** AI08 requires specific attention in interfaces that blend AI-generated and human-generated content. The artifact component must make AI provenance legible without treating every AI output as suspect. The design challenge is signal clarity: users need to know what the AI produced without every artifact carrying an anxiety-inducing disclaimer.

---

### Capability Discovery (CD)

These components address the question: *Does the user understand what this system can do, and how to ask for it effectively?*

| ID | Component | When to Use |
|---|---|---|
| CD01 | Suggested Prompts | User arrives with no context — empty prompt box |
| CD02 | Suggested Next Actions | Post-response follow-on actions are available and relevant |
| CD03 | Prompt Enhancement | User's prompt is vague and a more specific version exists |
| CD04 | Task Builder | Task is complex enough to warrant structured form controls instead of free text |

**Application standard:** CD03 is the component most frequently implemented unethically. Silent prompt enhancement — rewriting the user's input without disclosure — violates user autonomy and produces outputs users cannot attribute to their own intent. Enhancement must be visible, reversible, and opt-in.

CD01 is not a substitute for onboarding. Suggested prompts reduce activation friction; they do not teach the user what the system's actual capability boundaries are. Teams that rely on CD01 alone produce users who are surprised when the system cannot do what the suggestions implied.

---

### Agent Activity (AG)

These components address the question: *What is the agent doing right now, and what has it done?*

| ID | Component | When to Use |
|---|---|---|
| AG01 | Agent Activity Timeline | Showing chronological agent steps with status |
| AG02 | Tool Execution Log | Logging tool calls made by an agent in real time |
| AG03 | Collapsible Agent Steps | Long reasoning chains need condensing without hiding |
| AG04 | Process vs Result Layout | Agent produces both a reasoning trace and a final deliverable |

**Application standard:** AG04 encodes the most important layout decision in agentic UI: the result is the primary surface, the process is secondary. Teams that default to showing reasoning chains first produce interfaces that feel like watching someone else think — technically transparent, but practically exhausting. The reasoning must be accessible; it should not be default.

AG03 addresses the cognitive load problem of long agent runs. Collapsing steps is not hiding them — but the design must make it clear that steps exist and are reviewable. The anti-pattern is collapsing into a single success message that gives the user no evidence of what was actually done.

---

### Context Management (CM)

These components address the question: *Does the user know what information the AI is working with, and can they control it?*

| ID | Component | When to Use |
|---|---|---|
| CM01 | Context Sources | Showing what data sources the AI is drawing from |
| CM02 | Context Pills | Compact indicators of active context in the prompt area |
| CM03 | Active Memory Panel | Surfacing and managing AI memory across sessions |
| CM04 | Context Scope Selector | Letting users define the scope of an AI query |

**Application standard:** CM03 is absent from most consumer AI products, and its absence is a design failure. If a system stores memory across sessions, users have a right to know what is stored, how it affects responses, and how to remove it. Memory without visibility is a dark pattern — the system is making decisions based on information the user cannot see or contest.

CM01 pairs directly with TD02 (Transparency Popovers): the source of a claim and the reasoning behind a claim are different things, and users need both.

---

## How to Apply RAD in UX Reviews

When analyzing an agentic interface against RAD principles, the relevant questions are:

**Disclosure audit:**
- Does the user know when AI is involved in a decision, action, or recommendation?
- Are confidence levels and data limitations surfaced at the point of output, not buried elsewhere?
- Is algorithmic ranking disclosed anywhere choices are pre-ordered or pre-selected?

**Control audit:**
- At what points can the user stop, redirect, or override the agent?
- Are irreversible actions preceded by a warning and explicit approval?
- Is the agent's current state visible while it is running?

**Attribution audit:**
- Can the user trace any AI-generated output back to its source and reasoning?
- Is there a recoverable audit trail if something goes wrong?
- Is memory surfaced and controllable, or is it invisible and permanent?

**Capability honesty audit:**
- Do suggested prompts represent actual system capability?
- Is prompt enhancement visible and reversible?
- Does the first-run state teach capability boundaries, or just reduce friction?

---

## Source

RAD Design System — jackiecurry
Plugin repository: [github.com/jackiecurry/rad-plugin](https://github.com/jackiecurry/rad-plugin)
Published design system: [jackiecurry.github.io/rad](https://jackiecurry.github.io/rad)
