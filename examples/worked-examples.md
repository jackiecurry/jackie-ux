# Worked Examples

Five examples across all four modes. Scenarios are drawn from enterprise integration, data, and AI platform contexts.

---

# Example 1: Strategic Mode — Enterprise Onboarding

**Prompt:**
"I'm designing onboarding for an enterprise integration platform. Our users are IT architects and business analysts. Drop-off is highest in the first session. Give me a strategic analysis of the best approach."

---

`[Strategic Mode]`

The drop-off problem in enterprise integration platform onboarding almost always has the same root cause, and it is not the one most teams go looking for. The instinct is to improve the tutorial — more guidance, clearer labels, friendlier copy. This treats the problem as an information deficit. The actual problem is usually a value deficit: users arrive at the product before they have a specific integration problem that the platform can solve today.

Enterprise integration tools are complex because the problems they address are complex. You cannot demonstrate that value through a feature tour. You demonstrate it through a first session that ends with the user having connected something real. If your onboarding does not connect to a system they already need to integrate, you are building toward a product they will return to eventually — but not urgently.

**The Two-Persona Problem**

IT architects and business analysts have fundamentally different relationships with the platform. Architects come with technical questions — connector configuration, authentication patterns, pipeline execution logic, environment promotion. Analysts come with data questions — can I get Salesforce data into Snowflake, why did my pipeline fail, what does this error mean. An onboarding flow that treats both as a single user type will be too technical for analysts and too simplified for architects.

The strategic decision point is whether to build persona-differentiated onboarding at first session, or to build a first-session experience that adapts based on early behavior. Both are valid. The persona-differentiated approach requires self-identification, which introduces friction and error — users do not always know which persona fits them, and enterprise users resent being asked to categorize themselves before they have done anything. The adaptive approach requires enough signal in the first few minutes to make accurate inferences — which may not be possible before the user has built their first pipeline.

A third path is increasingly common in enterprise products: the sales-to-product handoff. If users arrive with a documented use case from the sales or implementation process, that context can be passed into the product and used to personalize the first session without asking the user to self-identify. This requires coordination between product, sales, and CRM — harder to ship, but the most accurate.

**Trade-offs**

| Approach | Gains | Costs |
|---|---|---|
| Generic onboarding tour | Low development cost | Low relevance, high drop-off for both personas |
| Self-selected persona paths | Relevant first session for users who self-identify correctly | Friction at entry, errors when users choose the wrong path |
| Behaviorally adaptive onboarding | No friction, adapts to actual behavior | Requires sufficient early signal, complex to build |
| Sales-to-product context handoff | Highest relevance, no friction | Requires cross-functional coordination, depends on CRM data quality |

**Recommendation**

The highest-leverage intervention is not a better tutorial — it is a better definition of what "first success" means for each user type, followed by an onboarding flow designed to reach that state rather than explain the platform's feature set.

Define one specific outcome that constitutes a successful first session for an architect (example: deployed a pipeline that moves data between two live systems in a non-production environment) and one for an analyst (example: ran a pre-built pipeline template against their own data source and saw results). Build the first session flow backward from those outcomes — not forward from the product's feature hierarchy.

---
---

# Example 2: Strategic Mode — Dual-Audience Pipeline Builder

**Prompt:**
"Our pipeline builder is used by both technical developers and non-technical business users. Right now it's a canvas. Developers love it. Business users struggle. We're considering adding a simplified mode. Give me a strategic analysis."

---

`[Strategic Mode]`

The dual-mode instinct is understandable, and it is also the right direction — but only if you are precise about what the simplified mode is actually simplifying. The most common failure in this pattern is building a simplified mode that removes capability rather than complexity. Those are not the same thing.

**What business users are actually struggling with**

Before building a second mode, you need to know which part of the canvas is causing the struggle. There are three distinct failure patterns, and they require different solutions:

1. **Conceptual failure** — the user does not have a mental model for how pipelines work (data flows, transformations, sequential execution). The canvas is failing because it is exposing a paradigm the user has not yet internalized. A simplified mode does not fix this — it delays it.

2. **Execution failure** — the user understands what they want to do but cannot figure out how to configure the components to do it. The canvas is fine; the component configuration panels are the problem. This is a detail-level UX problem, not a canvas problem.

3. **Orientation failure** — the user is lost in a large, complex canvas and cannot find what they are looking for or understand the state of what they have built. This is a navigation and legibility problem, not a paradigm problem.

Only the first failure pattern actually warrants a different mode. The second and third can be solved within the existing canvas with better configuration UX and better canvas-level legibility affordances.

**The simplified mode risk**

If you build a simplified mode, you are creating two products that must stay in sync. Every time the platform gains a new capability, you make a decision about whether it belongs in both modes or just one. Over time, simplified mode becomes the mode with outdated capabilities, and business users who have grown in sophistication hit a ceiling and need to migrate to the canvas — a migration that feels like a demotion.

The more sustainable pattern is a single canvas with progressive complexity exposure. A business user and a developer looking at the same pipeline see different levels of detail based on their role or preference — not a different product. Templates and guided flows can abstract the initial build without hiding the underlying model.

**Trade-offs**

| Approach | Gains | Costs |
|---|---|---|
| Simplified separate mode | Low initial friction for business users | Two products to maintain, capability ceiling, migration friction |
| Progressive complexity on one canvas | Single product, no ceiling, grows with the user | Harder to build, requires strong information hierarchy |
| Templates with guided configuration | Fast time-to-value, abstracts complexity | Users do not learn the underlying model, limits eventually |
| Improved configuration UX within canvas | Fixes the actual problem if it is execution failure | Does not help if the problem is conceptual |

**Recommendation**

Audit your support tickets and session recordings for business user sessions before committing to a second mode. Classify the failure patterns you see. If the majority are conceptual failures, a guided template-first approach that teaches the pipeline model progressively is more defensible than a parallel mode. If the majority are execution failures, fix the configuration panels — the canvas is not the problem.

Do not build a second mode until you know which failure you are solving.

---
---

# Example 3: Direct Mode — Pipeline Error Communication

**Prompt:**
"When a pipeline run fails, should we show the technical error and stack trace, or translate it into plain language guidance? Direct Mode."

---

`[Direct Mode]`

Show both, layered. Plain language first, technical detail behind a disclosure. Never show a raw stack trace as the primary error surface — most users, including technical ones, cannot action a stack trace without knowing which component failed, why, and what to do next.

The primary error surface should answer three questions in plain language: what failed, why it failed (in terms of the data or system state, not the code), and what the user can do to resolve it. The stack trace and raw error log belong in an expandable secondary panel for users who need to debug at the system level or escalate to support.

The reason to include both rather than translating only: enterprise technical users will distrust a system that hides the underlying error. They need to verify that the plain language interpretation is accurate, and they need the raw output when filing tickets or escalating to an integration team. Hiding the technical detail reads as the product being evasive about what actually went wrong.

---
---

# Example 4: Provocative Mode — AI-Generated Pipeline Suggestions

**Prompt:**
"We're adding AI-suggested pipelines. When a user describes what they want to integrate, the AI generates a full pipeline configuration and presents it as a starting point. Challenge my thinking."

---

`[Provocative Mode]`

The feature is sound in concept. The risk is in how "starting point" is communicated — and whether your users will actually treat it as one.

Enterprise users working on integration pipelines are operating in consequential contexts. Pipelines move production data, trigger downstream systems, and execute on schedules. A user who accepts an AI-generated configuration without understanding it is not starting from a starting point — they are deploying something they did not build and cannot fully reason about. The moment that pipeline fails or produces unexpected results, you have a user who cannot diagnose it, a support burden you did not plan for, and a trust problem that is harder to recover from than the feature was worth.

The assumption to pressure-test is not whether the AI can generate a reasonable pipeline. It probably can, for common patterns. The assumption is that users will engage with the suggestion critically before accepting it. The evidence from analogous AI-assisted features — code completion, email drafts, form autofill — is that users accept AI suggestions at a higher rate than intended when the path to acceptance is shorter than the path to review. If your UI makes accepting easier than reviewing, you will get acceptance rates that look like success metrics and user comprehension rates that tell a different story.

The design question is not how to present the generated pipeline. It is how to make the review step feel necessary rather than optional. That means surfacing what the AI decided and why — which connectors it chose, what data mapping assumptions it made, what it could not determine and left as a placeholder. A pipeline presented as complete invites acceptance. A pipeline presented as a reasoned draft with explicit unknowns invites engagement.

What is the intended interaction between a user and the suggestion before they run it for the first time?

---
---

# Example 5: Direct Mode — Navigation Pattern

**Prompt:**
"Should I use tabs or a sidebar for navigation in my B2B dashboard? Direct Mode."

---

`[Direct Mode]`

Use a sidebar. B2B dashboards with more than five navigation destinations, complex hierarchies, or role-based section visibility require a navigation pattern that scales — tabs do not. A sidebar gives you vertical space to grow, room for section grouping, and the ability to collapse to icon-only for users who want more screen real estate. Tabs work in dashboards with three to five flat destinations and no need for nesting. If you are building a B2B data or integration tool, you are almost certainly not in that situation.
