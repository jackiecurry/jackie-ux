Changelog

⸻

v2.0.0 — Unified UX + UI Skill

Release date: 2026

What’s new
	•	Build Mode
Introduces a fourth operational mode for execution tasks such as component design, CSS, flow specifications, and wireframe annotations. Build Mode is automatically detected from request language alongside the existing Strategic, Direct, and Provocative modes.
	•	Visual design and UI craft capabilities
Adds system-driven visual design fundamentals including:
	•	8pt grid alignment
	•	Mathematical type scales
	•	60-30-10 color balance
	•	Component height scales
	•	Shadow hierarchy
	•	Dark mode palettes
	•	GPU-accelerated animation and easing functions
All values are derived from a coherent design system.
	•	Cross-industry pattern recognition
Expands pattern knowledge to include onboarding archetypes, authentication flows, e-commerce patterns, dashboard structures, and settings architecture, along with a cross-industry inspiration mapping table.
	•	Five companion knowledge files
	•	knowledge/psychology-deep-dive.md
Cognitive science references, decision architecture, and animation timing tables with CSS easing values.
	•	knowledge/patterns-and-flows.md
Cross-industry patterns for onboarding, authentication, commerce flows, dashboards, and navigation.
	•	knowledge/design-tokens.md
Complete CSS token scales covering spacing, typography, color, shadows, radii, and breakpoints.
	•	knowledge/component-library.md
Detailed specifications for buttons, inputs, cards, tables, modals, navigation elements, tooltips, and toasts.
	•	knowledge/polish-and-craft.md
Advanced visual techniques, including copy-paste CSS, responsive layout rules, and touch-target guidelines.
	•	Interface text step
Content design is now a defined stage in the operational process. Button labels, error messages, empty states, and confirmation dialogs follow explicit rules rather than being deferred.
	•	Knowledge file upload guidance
The Claude integration guide now includes instructions for uploading companion knowledge files as project knowledge, enabling precise retrieval of tokens and specifications.
	•	Updated token guidance
Recommended max_tokens increased to 4,000 minimum to accommodate Build Mode output, as component specifications and full flows frequently exceed 2,500 tokens.

Design decisions

The original skill was intentionally positioned as a strategic reasoning system, not a generator of design artifacts. Version 2.0 introduces execution capabilities, but only within the same UX-first framework.

Build Mode still requires the agent to:
	1.	Understand the human context
	2.	State the design strategy
	3.	Produce the artifact

This sequencing prevents the system from degrading into a pure code generator that jumps directly to implementation.

Mode auto-detection removes the need for prompt engineering. The skill reads the request, selects the appropriate mode, and explicitly signals the mode in its response. Practitioners can still override this behavior when needed.

The knowledge architecture intentionally separates principles from specifications:
	•	The system prompt governs reasoning and behavior
	•	The knowledge files provide precise values, tables, and CSS implementations


⸻

v1.0.0 — Initial Release

Release date: 2025

What this version established
	•	Three operational modes: Strategic, Direct, and Provocative
	•	Ten core capability areas with application-level knowledge documentation
	•	Knowledge base covering:
	•	Nielsen’s heuristics with applied commentary
	•	Behavioral psychology laws
	•	AI/UX considerations
	•	Three worked examples demonstrating each operational mode in realistic UX scenarios
	•	Contribution guidelines for extending and refining the skill
	•	Vocabulary constraint policy with a prohibited word list and rationale
	•	Formatting rules governing structure, tone, and presentation
	•	Full system prompt compatible with Claude and other LLM platforms
	•	Integration guides for Claude (Projects and API) and OpenAI Custom GPTs

Design decisions

The skill is intentionally positioned above entry-level and intermediate UX practice.

It does not:
	•	define foundational UX terminology
	•	provide tutorial-style explanations of established concepts
	•	soften positions to avoid disagreement

This is deliberate. The intended practitioner is senior, and the value of the system diminishes if it dilutes its reasoning to accommodate a broader audience.

The three-mode structure reflects distinct decision contexts:
	•	Strategic Mode — the default. Most UX decisions have downstream consequences that benefit from deliberate reasoning.
	•	Direct Mode — used when speed matters more than deliberation.
	•	Provocative Mode — designed to challenge assumptions and surface risks that feel deceptively certain.

The vocabulary constraint policy reflects a broader theory of quality: the language an agent uses signals the quality of the thinking behind it. Restricting inflated language is not a stylistic preference; it is an epistemic standard.

⸻
