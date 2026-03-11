# UX Writing — Knowledge Base

Interface copy is a design decision, not a communication task. The words you choose determine what users believe the system can do, whether they trust it when it fails, and whether they recover when they are lost. Every label, error, placeholder, and confirmation dialog is a choice about cognitive load, emotional tone, and trust calibration.

This file covers the patterns, rules, and failure modes the agent draws on when writing, reviewing, or auditing interface text.

---

## Voice and Tone

Voice is constant. Tone adapts.

**Voice** is the personality of the product expressed through language — defined once, applied everywhere. Attributes like "direct, honest, specific" describe voice. Voice does not change based on context.

**Tone** is the emotional register adjusted to match the user's current state. Errors call for calm and accountability. Success moments call for brevity. Onboarding calls for confidence without presumption.

The most common failure: products that use a single tone everywhere. Cheerful copy on an error screen reads as tone-deaf. Formal copy in an empty state reads as cold. The mismatch erodes trust faster than the error itself.

### Tone Map by Context

| User state | Tone target | Avoid |
|---|---|---|
| Error / failure | Calm, accountable, specific | Apologetic filler, blame-shifting, exclamation points |
| Success / completion | Brief, affirmative, forward-pointing | Excessive celebration, drawn-out confirmation |
| Empty state | Orienting, explanatory, non-presumptuous | Cheerful emptiness ("Nothing here yet!") |
| Onboarding | Confident, low-pressure | Overselling, manufactured urgency |
| Destructive action | Precise, neutral, consequence-naming | Vague labels, scary language |
| Permissions / consent | Specific, honest, non-coercive | Buried opt-outs, dark pattern framing |

---

## Patterns by Screen Type

### Button Labels

Name the outcome, not the action. The user already knows they are clicking a button — the label should complete the sentence "When I click this, I will..."

**Pattern:** [Verb] + [Object] (optionally + [context])

| Anti-pattern | Corrected |
|---|---|
| Submit | Save changes |
| OK | Confirm deletion |
| Yes | Archive this project |
| Send | Send to design team |
| Continue | Continue to payment |
| Next | Next: Add team members |

Rules:
- One primary action per form section. Not two.
- Destructive actions name what is being destroyed: "Delete project" not "Delete"
- Both buttons in a pair must be understandable without reading anything else on screen: "Cancel" / "Delete project" works. "No" / "Yes" does not.
- Loading state label mirrors the active verb: "Saving…" not "Loading…"

---

### Error Messages

Every error must answer three questions in plain language:

1. What happened?
2. Whose fault is it — the user's or the system's?
3. What should the user do next?

Missing any one produces an incomplete error. "Something went wrong" fails all three. "Invalid input" fails two.

**Structure:** What happened → why (if it adds recovery value) → what to do next.

| Anti-pattern | Corrected |
|---|---|
| Something went wrong. | We couldn't save your changes — the connection was interrupted. Try saving again, or copy your work first. |
| Invalid email address. | The email address isn't in a recognized format. Check for a missing "@" or a typo. |
| Error 403 | You don't have permission to view this page. Contact your workspace admin to request access. |
| Your session has expired. | You've been signed out after 30 minutes of inactivity. Sign in again to continue — your work has been saved. |

Additional rules:
- Preserve the user's work wherever possible, and say so explicitly when you do
- Never blame the user for system failures
- If the error is the user's fault, be specific about what went wrong — not accusatory, but precise
- Recovery CTA should be the exact next step, not a vague suggestion

---

### Empty States

Every empty state exists for a reason. The reason determines the copy.

**Four types:**

**1. First-time empty** — the user has never added anything yet.
Goal: orient, explain what goes here, give a clear first action.
Example: "You haven't created any pipelines yet. A pipeline connects your data sources and transforms data between them. [Create your first pipeline]"

**2. Search / filter empty** — the user's query returned nothing.
Goal: acknowledge the query, suggest a path forward.
Example: "No results for "Salesforce connector." Check your spelling or try a broader search term."

**3. Cleared empty** — the user just deleted or dismissed the last item.
Goal: confirm the action completed, offer what's next.
Example: "All notifications cleared. New notifications will appear here when your pipelines run."

**4. Permission empty** — the user doesn't have access to the content.
Goal: explain the access barrier and who can resolve it.
Example: "This report isn't shared with you. Ask the report owner to share it, or contact your workspace admin."

Anti-patterns:
- "Nothing here yet!" — cheerful, explains nothing, gives no action
- Blank screens with no explanation
- Error iconography for states that aren't errors

---

### Confirmation Dialogs

Both button labels must be understandable without reading the surrounding text. Test by covering the dialog body and reading only the buttons.

**Structure:**
- Headline: name the action specifically ("Delete "Q4 Sales Pipeline"?")
- Body: name the consequence and whether it is reversible
- Buttons: specific action label + specific cancel label

| Component | Anti-pattern | Corrected |
|---|---|---|
| Headline | Are you sure? | Delete "Q4 Sales Pipeline"? |
| Body | This cannot be undone. | This will permanently delete the pipeline and its run history. Connected integrations will not be affected. |
| Confirm button | Delete | Delete pipeline |
| Cancel button | Cancel | Keep pipeline |

The "Keep [thing]" pattern for cancel buttons is underused. "Keep pipeline" / "Delete pipeline" as a pair is more useful than "Cancel" / "Delete pipeline" because both labels describe an outcome, not just one of them.

---

### Form Labels and Placeholder Text

Labels belong above the field, always. Not inside it.

Placeholder text is not a label. Placeholder text disappears when the user starts typing, which means they lose context mid-task. If the label is in the placeholder, the user cannot check what the field was asking for after they have entered something.

**The one valid use for placeholder text:** format examples that are genuinely supplementary. "e.g., 2024-01-15" helps. Instructions do not belong here. Labels do not belong here.

Helper text (below the field, persistent) is for constraints and format requirements: "Must be at least 12 characters" or "Use the format YYYY-MM-DD." Write it before the user encounters the error — not only in the error state.

Label rules:
- Top-aligned, always
- Sentence case: "Email address" not "Email Address"
- No trailing colons
- Mark optional fields, not required ones — if most fields are required, mark the exceptions with "(optional)"
- No abbreviations: "Phone number" not "Phone #"

---

### Navigation Labels

Navigation labels are the map. They must match what the user finds when they arrive, not what the internal team calls the destination.

- Use the user's vocabulary, not the product's internal architecture vocabulary
- Verb-noun for action destinations: "Create pipeline" not "Pipeline Creation"
- Noun for reference destinations: "Settings", "Reports", "Team"
- Avoid clever names that require context: "The Hub" tells a new user nothing
- Test with tree testing before shipping — navigation labels are the highest-leverage copy in the product because they mediate access to everything else

---

### Tooltips

Tooltips are for information that is genuinely supplementary — not required to complete the task, but useful to some users in some contexts.

Rules:
- If the user needs the information to complete the task, it belongs in the UI, not a tooltip
- One sentence: what this does or why it matters
- Never start with "This button..." — start with what the action does: "Triggers a manual sync of all connected data sources"
- Never put information critical to a decision only in a tooltip

---

### Onboarding and Progressive Disclosure

Onboarding copy sets the user's mental model of the product. The words used in the first session become the vocabulary the user carries into every subsequent session and every conversation with their colleagues.

- Use the product's actual terminology consistently from the first screen — if it's called a "pipeline," call it a pipeline, not a "connection" or a "flow"
- State what the product does in the user's terms: "Connect your data sources and define how they move and transform" not "Configure your integration topology"
- Label sample and demo data explicitly — users should always know whether they are looking at real data or examples
- Progress indicators for multi-step flows should name the step, not just number it: "Step 2 of 4: Connect your source" not "Step 2 of 4"

---

## The User Vocabulary Problem

The single most common UX writing failure in enterprise software is using internal or technical vocabulary that the user does not share.

When search logs show null results, the most common cause is not that users searched for something that doesn't exist — it is that they searched using different words than the content uses. This is the documented gap between user vocabulary and system vocabulary.

Fix it at two levels:

1. **Search and navigation:** Add synonyms, aliases, and user-facing labels alongside technical terms
2. **Interface copy:** Use the words users actually say during contextual inquiry and usability sessions — not the words the engineering team uses in the data model

The test: can a user who has never seen the product before read a label or button and know what it refers to? If they need prior product exposure to understand the label, the label is written for insiders.

---

## Reading Level and Cognitive Load

Enterprise software users are not reading your interface. They are scanning it. Under task load, users process interface text at a significantly reduced rate compared to reading for comprehension.

Practical rules:
- Front-load the important information: the first five words carry most of the weight
- One idea per sentence
- Maximum two sentences for any body copy in a task flow
- Avoid embedded clauses: "Click Save, which will apply your changes and return you to the dashboard" → "Click Save to apply your changes. You'll return to the dashboard."
- Sentence case always — all caps and title case both increase reading time
- Specifics over generics: "Saved 3 minutes ago" beats "Saved recently"

---

## Trust Copy

Permissions requests, consent dialogs, and legal-adjacent UI are the places where users are most likely to either disengage entirely or click through without reading. Both outcomes are failures.

Rules:
- Name what you are asking for and why in one sentence: "This integration needs access to your Google Drive to import spreadsheets." Not "This app requires certain permissions to function."
- State the consequence of granting or not granting: "Without calendar access, this integration can't schedule meetings on your behalf."
- Consent must be as easy to decline as to grant — if the decline path requires more steps, the consent is coerced
- Keep legal-mode writing out of the primary consent surface — if the legal team requires specific language, put it behind a disclosure link
- Do not disguise data collection as a feature benefit

---

## Diagnostic Questions

When reviewing any interface copy, apply these in sequence:

**Button labels:** Cover the surrounding context. Read only the button. Does it tell you what will happen?

**Error messages:** Does this error answer (1) what happened, (2) whose fault it is, and (3) what to do next? If not, which question is missing?

**Empty states:** Which of the four types is this? Does the copy address the reason this state exists, not just the fact that it is empty?

**Confirmation dialogs:** Cover the body text. Read only the two button labels. Are both outcomes clear?

**Navigation labels:** Ask a user who has never seen the product: "Where would you go to find [task]?" If they don't point to the right label, the label is wrong — not the user.

**Placeholder text:** Remove the placeholder. Does the form still work? If the answer is no, the placeholder was doing the label's job.
