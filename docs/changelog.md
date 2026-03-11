# Changelog

---

## v2.0.0 — Unified UX + UI Skill

**Release date:** 2026

**What this version adds:**

- **Build Mode:** A fourth operational mode for execution tasks (component design, CSS, flow specs, wireframe annotations). Auto-detected from request language alongside the existing Strategic/Direct/Provocative modes.
- **Visual Design and UI Craft capability:** 8pt grid, mathematical type scales, 60-30-10 color, component height scales, shadow hierarchy, dark mode palettes, GPU-accelerated animation, and easing functions. Every value comes from a system.
- **Cross-Industry Pattern Recognition capability:** Onboarding archetypes, authentication patterns, e-commerce flows, dashboard types, settings architecture, and the cross-industry inspiration mapping table.
- **Five companion knowledge files:**
  - `knowledge/psychology-deep-dive.md` — Cognitive science detail, decision architecture, animation timing tables with CSS easing values
  - `knowledge/patterns-and-flows.md` — Cross-industry patterns for onboarding, auth, e-commerce, dashboards, and navigation
  - `knowledge/design-tokens.md` — Complete CSS custom property scales: spacing, color, typography, shadows, radii, breakpoints
  - `knowledge/component-library.md` — Full specifications for buttons, inputs, cards, tables, modals, nav, tooltips, toasts
  - `knowledge/polish-and-craft.md` — Advanced visual techniques with copy-paste CSS, responsive patterns, touch target rules
- **Interface text step:** Content design is now an explicit step in the operational process, handled directly rather than deferred. Button labels, error messages, empty states, and confirmation dialogs have specific rules.
- **Knowledge file upload instructions:** The Claude integration guide now includes the step to upload companion knowledge files as project knowledge, enabling the agent to retrieve exact token values and specs on demand.
- **Updated token guidance:** `max_tokens` recommendation raised to 4,000 minimum to accommodate Build Mode output (component specs and full flows regularly exceed 2,500 tokens).

**Design decisions in this version:**

The original skill was intentionally positioned as a strategic reasoner that did not produce design deliverables. This version adds the ability to execute — but execution is gated behind the same UX-first posture. Build Mode still requires understanding the human and stating the strategy before producing any artifact. The operational process exists precisely to prevent the skill from becoming a code generator that skips to implementation.

The mode auto-detection logic was added because practitioners should not have to manage prompt engineering to get appropriate behavior. The skill reads the request type and signals which mode it has selected, which also makes it easy to override.

The knowledge files are companion documents, not embedded content. The system prompt embeds the principles; the knowledge files provide the specific values, tables, and CSS. This distinction matters: the prompt governs behavior, the files enable precision.

---

## v1.0.0 — Initial Release

**Release date:** 2025

**What this version establishes:**

- Three operational modes: Strategic, Direct, Provocative
- Ten core capability areas with application-level knowledge documentation
- Vocabulary constraint policy with prohibited word list and reasoning
- Formatting rules covering structure, tone, and presentation
- Full system prompt for Claude and compatible LLM platforms
- Integration guides for Claude (Projects and API) and OpenAI Custom GPTs
- Knowledge base covering Nielsen's heuristics with applied commentary, behavioral psychology laws, and AI/UX considerations
- Three worked examples demonstrating each mode in a realistic UX scenario
- Contribution guide for extending or refining the skill

**Design decisions in this version:**

The skill is intentionally positioned above entry-level and intermediate UX practice. It does not define basic terms, does not provide tutorial-style explanations for established concepts, and does not soften positions to avoid disagreement. This is a deliberate choice — the target practitioner is senior, and the value of the skill diminishes if it hedges to accommodate a broader audience.

The three-mode structure is not arbitrary. Strategic Mode is the default because most UX decisions have downstream consequences that benefit from deliberation. Direct Mode exists because there are situations where deliberation is a liability — the practitioner needs to move. Provocative Mode exists because the most expensive design mistakes are the ones that felt certain.

The vocabulary constraint policy reflects a specific theory of quality: that the words an agent uses signal the quality of the thinking behind them. Prohibiting inflated language is not a style preference — it is an epistemic standard.

---

## Planned for v1.1

- Heuristics knowledge file with extended application commentary
- Research methodology knowledge file (usability testing, survey design, tree testing)
- Additional worked examples covering accessibility-specific scenarios
- LangChain integration guide for open-source model deployment
- Reflex and error pattern library for common UX anti-patterns
