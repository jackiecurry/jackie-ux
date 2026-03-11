# Product Strategy — Knowledge Base

This document provides the product management knowledge the agent draws from. It is not a survey of PM methodology — it is a working reference for the decisions practitioners face when user needs, business constraints, and technical reality collide. Every framework here is applied, not described.

---

## Prioritization

### RICE Scoring

**Framework:** Reach × Impact × Confidence ÷ Effort. Assigns a numeric score to competing initiatives to reduce the influence of the loudest voice in the room.

**Where it is misapplied:** Teams treat RICE as a neutral calculation when every input is a judgment call. Reach estimates come from whoever has access to analytics and an interest in the outcome. Impact is almost always inflated — a "massive" rating requires evidence, not optimism. Confidence exists to penalize speculation, but practitioners routinely assign 80% confidence to ideas they have never tested with a real user. Effort estimates made without engineering input are fiction.

**The underlying question:** Are the inputs to this model grounded in evidence, or are they post-hoc justifications for a decision already made politically?

---

### ICE Scoring

**Framework:** Impact × Confidence × Ease. A lighter-weight alternative to RICE, often used for growth experiments where speed of iteration matters more than precision.

**Where it is misapplied:** ICE rewards easy work. High ease scores pull attention toward low-effort, low-ambition initiatives and create a roadmap that optimizes for shipping velocity rather than user value. Teams using ICE for years end up with products that have been polished incrementally but never strategically advanced.

**The underlying question:** Is the team optimizing for learning speed, or using ease as a proxy for avoiding difficult problems?

---

### Kano Model

**Framework:** Classifies features into five categories — Basic (must-have), Performance (linear satisfaction return), Excitement (unexpected delight), Indifferent (no impact), and Reverse (actively unwanted). The practical insight is that satisfying basic needs prevents dissatisfaction but does not create loyalty; excitement features create loyalty but become basic over time as expectations evolve.

**Where it is misapplied:** Teams use Kano as a one-time exercise rather than a time-sensitive measurement. A feature that was an excitement differentiator in 2020 (in-app notifications, dark mode, single sign-on) is a basic expectation in 2025 — its absence creates active dissatisfaction. The model requires periodic re-evaluation, not archiving.

**The underlying question:** Which features in the current backlog are excitement investments, and which are basic needs we have not yet met that are eroding trust every day they remain unbuilt?

---

### MoSCoW Method

**Framework:** Must Have, Should Have, Could Have, Won't Have. Simple language for scope negotiation between product, engineering, and stakeholders.

**Where it is misapplied:** Everything ends up as Must Have. When practitioners cannot defend what they would ship without — what would make a release not worth releasing — MoSCoW becomes a theater exercise that produces a prioritized list with everything at the top. The discipline is in the Should and Won't columns, which require practitioners to name what they are giving up and own that decision.

**The underlying question:** If the team had to cut 40% of this scope today, what would stay? If the answer is not immediately clear, the Must Have column has not been honestly populated.

---

## Problem Definition

### Jobs-to-Be-Done

**Framework:** Users do not buy products — they hire them to make progress in a specific context. The job is defined by the functional outcome the user is trying to achieve, the emotional state they want to reach, and the social context in which the outcome occurs (Christensen, Ulwick). The job is stable; the solutions hired to do it change.

**Where it is misapplied:** JTBD gets converted into a user story format and loses its explanatory power. "When I am managing expense reports, I want to categorize transactions quickly so that I can close the month on time" describes a task, not a job. The job is: "When I need to demonstrate to my finance team that I am on top of my budget, I want to do it without having to think about it — so that I feel competent and in control." The product solution that addresses the task may be the wrong hire for the job.

**The underlying question:** If a user switched from this product to a competitor today, what job are they hiring the competitor to do? Is it the same job this product thinks it is doing?

---

### Opportunity-Solution Trees

**Framework:** A visual method for mapping from desired outcome → opportunity (unmet need or pain) → solution → assumption → experiment (Teresa Torres). The tree makes explicit which solutions address which opportunities and which opportunities support which outcomes — preventing the common failure of shipping solutions that address real problems but not the problems that matter for the stated outcome.

**Where it is misapplied:** Teams skip the opportunity layer and map directly from outcomes to solutions. The result is a backlog of solutions looking for problems. When a practitioner cannot trace a solution back to a specific opportunity, that solution has no defensible basis for prioritization.

**The underlying question:** For every solution in the backlog, what specific opportunity does it address? And does addressing that opportunity demonstrably advance the desired outcome?

---

### Problem Framing

**Principle:** The quality of a product decision is bounded by the quality of the problem definition. A well-scoped problem contains the user, the context, the current behavior, the desired behavior, and the evidence that the gap between them matters. An under-scoped problem invites solutions that satisfy the framing rather than the underlying need.

**Where it is misapplied:** Product briefs that open with "users want X" instead of "users are currently doing Y when they need to accomplish Z, and here is what we know about why Y falls short." The solution is embedded in the brief before the problem has been examined. Engineering builds it. Users ignore it.

**The underlying question:** Does the problem statement describe a specific user doing a specific thing in a specific context — or does it describe a feature request in disguise?

---

## Metrics and Outcomes

### North Star Metrics

**Framework:** A single metric that represents the core value the product delivers to users and predicts long-term business health. The north star should be a leading indicator of retention, not a lagging indicator of revenue. North star metrics measure value delivered (messages sent, reports completed, connections made), not activity (logins, page views, sessions).

**Where it is misapplied:** Teams pick metrics that are easy to measure rather than metrics that capture value. Daily active users is not a north star — it measures presence, not value. A user who opens the app every day and closes it without accomplishing anything is counted as a success. North star metrics must require users to have received value to register.

**The underlying question:** If this metric went up 20% but zero users reported that the product was more useful to them, would that be considered a success? If yes, the metric is measuring activity, not value.

---

### Success Metrics and Guardrails

**Principle:** Every initiative should define three things before it ships: a primary success metric (what winning looks like), a secondary metric (what additional signal would increase confidence), and at least one guardrail metric (what must not get worse). Guardrails are non-negotiable floors — an initiative that moves the success metric while degrading the guardrail has not succeeded; it has traded one problem for another.

**Where it is misapplied:** Teams define success metrics but omit guardrails. A new onboarding flow that improves activation rate by 12% while increasing support ticket volume by 30% has not shipped a success. The guardrail catches this before it becomes a post-mortem.

**The underlying question:** What user behavior would indicate that this initiative worked in a way that harms users or the product — and is there a metric that would catch it?

---

### Vanity Metrics

**Principle:** A vanity metric goes up without requiring anything to have improved. Total registered users, total downloads, and total features shipped are the canonical examples. They look like progress in a board deck. They predict nothing. The inverse test: if this metric could improve while users were getting less value, it is a vanity metric.

**The underlying question:** What would have to be true for this metric to increase while the product got worse for users?

---

## Trade-Off Reasoning

### User Need vs. Business Constraint

**Principle:** Product decisions are not binary choices between user value and business interests — most conflicts between them are either false conflicts (the business interest is actually served by addressing the user need) or they are real conflicts that require explicit acknowledgment and a defensible position. The failure mode is pretending the conflict does not exist.

**Where it is misapplied:** Features that serve business metrics at measurable cost to users get justified with language like "we are helping users discover more value." Bundling unwanted notifications to increase open rates is not helping users discover value. Naming what a decision actually does — "we are accepting worse UX here to improve a business metric" — does not prevent the decision from being made. It prevents it from being made invisibly.

**The underlying question:** If users could see exactly why this design decision was made, would the explanation survive scrutiny?

---

### Platform vs. Point-Solution Thinking

**Framework:** A platform invests in generality, extensibility, and the ability for others to build on top of it. A point solution invests in depth of value for a specific use case. These are not stages — platform thinking applied to a product that should be a point solution produces over-engineered abstractions used by no one. Point-solution thinking applied to infrastructure produces rigid systems that cannot be extended without rewrites.

**Where it is misapplied:** The decision is made by default rather than by design. Teams build point solutions because they are faster to ship, then find themselves unable to support enterprise use cases. Or they build platforms without a clear picture of who will build on them, producing API surface area that exposes internal complexity rather than enabling external builders.

**The underlying question:** Who would build on this if it were a platform — and is that a real person with a real need, or a hypothetical future customer?

---

### Design and Product Debt

**Principle:** Every shortcut creates a liability. Design debt (inconsistent patterns, undocumented components, one-off solutions that cannot be reused) compounds like financial debt — it does not stay manageable indefinitely. The cost shows up as slower design velocity, inconsistent user experience, and engineering friction when components need to be changed.

**Where it is misapplied:** Debt is treated as a cost to address later rather than a risk to quantify now. Teams that cannot name their current debt load cannot make an informed decision about when to pay it down. The question is not "should we incur this debt?" but "at what point does the interest on this debt exceed the cost of paying it off?"

**The underlying question:** If the team had to move quickly on this area of the product in six months, what would they have to undo first?

---

## Stakeholder Communication

### Framing Decisions for Executives

**Principle:** Executives do not evaluate product decisions on UX merit — they evaluate them on revenue potential, risk exposure, and timeline implications. A well-framed product recommendation translates the design or product rationale into those terms without misrepresenting the work. The translation is not spin; it is context.

**Format for a product recommendation to leadership:**
1. The problem — stated in terms of user behavior and business impact, with evidence
2. The proposed solution — described at outcome level, not feature level
3. What it costs — time, resources, and what else does not get done
4. The risk of inaction — what degrades if this is not addressed
5. The metric that will confirm success — specific and pre-committed

**Where it is misapplied:** Practitioners lead with process ("we did five user interviews") rather than findings. Executives fund outcomes, not methods. The research is the evidence, not the story.

**The underlying question:** If the recommendation were stripped of all methodology and design language, does the business case still hold?

---

### Presenting Research That Contradicts Stakeholder Assumptions

**Principle:** Research that confirms assumptions is easy to present. Research that contradicts them requires structural care. The failure modes are softening the finding until it loses meaning, or presenting it confrontationally in a way that triggers defensive response rather than genuine reconsideration.

**Effective structure:**
1. State the assumption that was being tested — this shows that the research was designed to examine something specific, not to produce a predetermined finding
2. Present what users actually did or said — behavior before interpretation
3. Offer the interpretation — clearly marked as interpretation, not fact
4. Give the implication — what this means for the direction under consideration
5. Propose the next step — give stakeholders something to do with the finding rather than just something to react to

**The underlying question:** If the stakeholder came away from this presentation believing the finding was an attack on their judgment rather than new information, what in the delivery caused that?

---

### When to Advocate and When to Compromise

**Principle:** A practitioner who advocates for everything has the same credibility as one who advocates for nothing. Knowing which battles to hold is a strategic skill, not a failure of conviction.

**Hold the position when:**
- The decision has irreversible downstream consequences (architectural choices, data model decisions, regulatory exposure)
- The compromise would create debt that costs more to resolve than the current argument
- User research directly contradicts the proposed direction and the stakes are high enough to matter

**Yield with acknowledgment when:**
- The disagreement is about preference, not evidence
- The cost of the wrong decision is recoverable in the next sprint
- The stakeholder has context the practitioner does not have (legal, organizational, competitive)

**What to avoid:** Yielding silently and relitigating the same decision later. A documented compromise with a named decision owner and a named metric to track the outcome is better than a consensus that no one owns.

**The underlying question:** Is this disagreement about what will happen, or about what matters? The first is resolvable with evidence. The second requires negotiation, not research.

---

## Roadmap Strategy

### The Roadmap as Communication, Not Contract

**Principle:** A roadmap communicates strategy and intent — it is not a delivery commitment. A roadmap that functions as a contract produces teams that hit schedule targets while missing the actual goal: learning quickly enough to build the right thing.

**Where it is misapplied:** Quarterly roadmaps with specific features and dates are shown to customers as commitments. The team then has to choose between shipping on time and shipping the right thing. In almost every such conflict, on time wins — which means customers get features that were designed nine months ago against assumptions that may no longer be valid.

**The underlying question:** If a significant user insight surfaced in month two of this quarter, does the team have the authority and the process to act on it — or does the roadmap prevent that?

---

### Now / Next / Later

**Framework:** Divides the roadmap into three time horizons: Now (committed, in execution, well-understood), Next (directionally committed, design and research in progress, details subject to change), and Later (strategic intent, not yet resourced). The value is honest signal for stakeholders: Now is a delivery. Next is a plan. Later is a direction.

**Where it is misapplied:** Everything important gets moved into Now as stakeholder pressure increases. The Later column empties out. The team stops thinking beyond the current quarter. Strategic work with long lead times — foundational infrastructure, research into unmet needs, architectural investments — gets perpetually deferred because it never achieves the urgency to enter Now.

**The underlying question:** Is there anything in the Later column that, if ignored for twelve more months, will cost significantly more to address than it would today?

---

### Saying No

**Principle:** A roadmap without rejected features is not a strategy — it is a list. Saying no requires more than declining; it requires explaining what the request would cost (what would not happen if this were prioritized), what the evidence for it is, and what the path is for it to become a yes in the future.

**The structure for a well-reasoned no:**
- Acknowledge the underlying need ("users do want faster access to X")
- Name the prioritization cost ("adding this in Q2 means delaying Y, which addresses a larger segment")
- Be specific about the conditions under which it would become a yes ("if we see this in user feedback at the scale that Y is generating, it moves up")

**Where it is misapplied:** No delivered as a ranking ("it scored lower in RICE") without the reasoning behind the inputs. A framework output is not a reason. The reasoning behind the inputs is the reason.

**The underlying question:** If the person who made this request understood exactly what it would cost to build and what it would mean for the rest of the roadmap, would they still want it at the same priority level?

---
