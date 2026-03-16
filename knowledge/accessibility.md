# Accessibility Rules

Comprehensive reference for building and auditing accessible interfaces.
Read when implementing components, reviewing designs, or conducting audits.

---

## Foundational Principle

Accessibility is not a compliance activity. It is a quality dimension that affects
every user — under varying devices, environments, lighting conditions, cognitive
loads, and physical states. The goal is not to pass a checklist; it is to ensure
the interface works for the full range of human experience.

Standard applied: WCAG 2.1 and 2.2 at Level AA minimum. AAA where noted.

---

## Perceivable

### 1.1 Text Alternatives

Every non-text element that carries meaning needs a text equivalent.

| Element | Rule |
|---|---|
| `<img>` with meaning | `alt="[descriptive text]"` |
| `<img>` decorative | `alt=""` (empty, not absent) |
| Icon-only button | `aria-label="[action name]"` + `aria-hidden="true"` on the icon |
| Icon with visible label | `aria-hidden="true"` on the icon — the label is sufficient |
| SVG (inline, meaningful) | `<title>` inside SVG or `aria-label` on container |
| Image of text | Avoid; use real text instead |
| Charts and graphs | Text summary or data table as alternative |

**Rule:** Never leave a meaningful image without `alt`. Never put the filename or
"image of" in `alt` — describe what the image communicates.

### 1.2 Time-Based Media

| Content type | AA requirement |
|---|---|
| Pre-recorded audio | Transcript |
| Pre-recorded video (silent) | Audio description or text alternative |
| Pre-recorded video with audio | Captions (synchronized) |
| Live audio/video | Captions for live content |

### 1.3 Adaptable

Structure must be preserved when CSS is removed or content is linearized.

- Use semantic HTML. `<button>` for actions, `<a>` for navigation, `<h1>`–`<h6>` for hierarchy.
- Heading levels must be sequential — do not skip from `<h1>` to `<h3>`.
- Reading order in DOM must match visual order. Do not reorder only with CSS.
- Form fields must have programmatically associated labels — use `<label for>` or `aria-labelledby`, not `placeholder` as a substitute.
- Landmark regions: `<header>`, `<nav>`, `<main>`, `<footer>`, `<aside>`. One `<main>` per page.
- Tables used for data require `<th>` with `scope` attributes, not `<td>` for all cells.

### 1.4 Distinguishable

**Color contrast — minimum ratios (WCAG AA):**

| Text type | Minimum ratio |
|---|---|
| Normal text (under 18px regular / under 14px bold) | 4.5:1 |
| Large text (18px+ regular or 14px+ bold) | 3:1 |
| UI components (inputs, buttons, focus rings, icons) | 3:1 |
| Disabled elements | No requirement — but mark clearly disabled |
| Decorative elements | No requirement |

**Color contrast — AAA targets (aspirational):**

| Text type | AAA ratio |
|---|---|
| Normal text | 7:1 |
| Large text | 4.5:1 |

**Rules:**
- Never use color alone to communicate meaning. Always pair with text, icon, pattern, or position.
- Error states that rely only on red fail WCAG 1.4.1. Add an error icon or message.
- Status indicators (online/offline, severity levels) need non-color differentiation.

**Text sizing and reflow:**
- Text must remain readable when scaled to 200% without loss of content or functionality.
- At 400% zoom (WCAG 1.4.10 Reflow), content must not require horizontal scrolling at 320px viewport width. Exception: content that requires 2D layout (maps, data tables, complex diagrams).

**Spacing:**
- Line height at least 1.5× the font size.
- Letter spacing at least 0.12em.
- Word spacing at least 0.16em.
- Do not override user-defined spacing. Use relative units (`em`, `rem`) not `px` for text sizing.

**Audio:**
- Background audio in auto-playing content must be stoppable or be below -20 dBFS relative to foreground.

---

## Operable

### 2.1 Keyboard Accessible

Every interaction achievable with a mouse must be achievable with a keyboard. No exceptions.

**Standard key bindings:**

| Key | Action |
|---|---|
| `Tab` | Move focus forward through interactive elements |
| `Shift+Tab` | Move focus backward |
| `Enter` | Activate links, submit forms, activate buttons |
| `Space` | Activate buttons, toggle checkboxes |
| `Arrow keys` | Navigate within composite widgets (menus, tabs, sliders, radio groups) |
| `Escape` | Close overlays, cancel operations, collapse expanded elements |
| `Home` / `End` | Jump to first / last item in a list or composite widget |

**No keyboard trap:** Focus must never be locked inside a component unless it is an intentional modal overlay. When a modal is open, trap focus within it. When it closes, return focus to the trigger.

**Custom widgets:** If you are building a menu, tabs, combobox, date picker, or tree, implement the full ARIA Authoring Practices Guide (APG) keyboard pattern. Using Radix UI satisfies this automatically.

### 2.2 Enough Time

- If a session timeout exists, warn the user at least 20 seconds before expiry with an option to extend.
- Auto-updating content must be pausable. Moving, scrolling, and blinking content that lasts more than 5 seconds must have a user control to pause, stop, or hide it.

### 2.3 Seizures and Physical Reactions

- Nothing on the page flashes more than 3 times per second (WCAG 2.3.1).
- Avoid rapidly flashing animations. If animation is required, respect `prefers-reduced-motion`.

### 2.4 Navigable

**Skip links:** Provide a visible (or visually hidden, appearing on focus) "Skip to main content" link as the first focusable element on every page.

```html
<a href="#main-content" class="sr-only focus:not-sr-only focus:fixed focus:top-4 focus:left-4 focus:z-50 focus:px-4 focus:py-2 focus:bg-background focus:text-foreground focus:rounded">
  Skip to main content
</a>
```

**Page titles:** Every page must have a descriptive `<title>` that identifies both the page and the site.

**Focus order:** Focus must follow a logical sequence that matches the reading order. Tab order should not jump unpredictably. Do not set `tabindex` values greater than 0.

**Focus visible:** Every focused element must have a visible focus indicator. Never apply `outline: none` without a replacement. Minimum (WCAG 2.2 AA): focus indicator must have 3:1 contrast ratio against adjacent colors, and change by at least 2px CSS perimeter area.

```css
/* Compliant Tailwind pattern */
focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2
```

**Link purpose:** Link text must be descriptive on its own. Avoid "click here", "read more", "learn more" without additional context via `aria-label` or visually hidden text.

**Headings and labels:** Use headings to organize content. Every section of content should be reachable via the heading structure.

**Multiple ways:** Provide more than one way to reach a page: site search, navigation, sitemap, or breadcrumb.

### 2.5 Input Modalities

**Touch targets (WCAG 2.5.5 / 2.5.8):**

| Standard | Minimum size | Spacing |
|---|---|---|
| WCAG 2.5.5 (AAA) | 44×44px | — |
| WCAG 2.5.8 (AA, WCAG 2.2) | 24×24px | At least 24px from edge of adjacent target |
| Apple HIG | 44×44px | — |
| Material Design | 48×48dp | 8dp between targets |

**Apply 44×44px as the working standard.** The 24px AA floor is a floor, not a target.

**Pointer cancellation (2.5.2):** For single-pointer actions, at least one of: the down-event is not used to complete the action; abort/undo is available; up-event reverses the down-event action. In practice: trigger actions on `mouseup` / `click`, not `mousedown`.

**Motion actuation (2.5.4):** If an action can be triggered by device motion (shake, tilt), a UI alternative must exist, and motion actuation must be disableable.

---

## Understandable

### 3.1 Readable

- Set `lang` attribute on `<html>`. Use the correct BCP 47 language code (`lang="en"`).
- Mark language changes within content with `lang` on the element.

### 3.2 Predictable

- **On focus:** No context change occurs when an element receives focus. Do not trigger navigation, form submission, or dialog opening on focus alone.
- **On input:** No context change occurs on input unless the user has been advised in advance. Do not auto-submit forms or auto-navigate on `<select>` change.
- **Consistent navigation:** Navigation elements that repeat across pages appear in the same order.
- **Consistent identification:** Components with the same function have the same label across the interface.

### 3.3 Input Assistance

**Error identification (3.3.1):** If a form has an error, identify the field and describe the error in text. Do not rely on color alone or placeholder disappearance.

```tsx
// Correct
<input aria-invalid={hasError} aria-describedby={hasError ? 'email-error' : undefined} />
{hasError && <p id="email-error" role="alert">{errorMessage}</p>}
```

**Labels or instructions (3.3.2):** Every input has a visible label. If an input requires a specific format (date, phone), provide that instruction before the field.

**Error suggestion (3.3.3):** If an error can be corrected with a specific suggestion, provide it. "Enter a valid email address" is better than "Invalid input".

**Error prevention (3.3.4):** For consequential actions (financial transactions, legal submissions, account deletion): provide review step before submission, allow correction, or allow reversal after.

**Redundant entry (3.3.7, WCAG 2.2):** Do not require users to re-enter information already provided in the same session unless re-entry is essential (password confirmation).

**Accessible authentication (3.3.8, WCAG 2.2):** Do not require cognitive function tests (solving puzzles, transcribing characters) for authentication. Support copy/paste in all password fields. Support password managers and autofill.

---

## Robust

### 4.1 Compatible

**Name, role, value (4.1.2):** Every interactive component has:
- An accessible name (from `<label>`, `aria-label`, `aria-labelledby`, or element content)
- A role (from semantic HTML or explicit `role` attribute)
- States and properties communicated via ARIA when they change

```tsx
// Accordion trigger
<button
  aria-expanded={isOpen}
  aria-controls="panel-id"
>
  Section title
</button>

// Disclosure with icon
<button aria-expanded={isOpen}>
  <ChevronIcon aria-hidden="true" className={isOpen ? 'rotate-180' : ''} />
  Section title
</button>

// Toggle
<button role="switch" aria-checked={isEnabled} aria-label="Enable notifications">
```

**Status messages (4.1.3):** Messages that appear without focus moving to them must use `role="status"` (polite, non-urgent) or `role="alert"` (assertive, urgent).

```tsx
// Non-urgent confirmation
<div role="status" aria-live="polite">File saved successfully</div>

// Urgent error
<div role="alert" aria-live="assertive">Session expired. Please log in again.</div>
```

Use `role="alert"` sparingly. It interrupts the screen reader immediately. Most confirmations should use `role="status"`.

---

## ARIA Reference

### When to use ARIA

Use native HTML semantics first. ARIA is for gaps that HTML cannot fill.

| Use ARIA when... | Do not use ARIA when... |
|---|---|
| HTML has no equivalent role | A native element can do the job |
| Updating dynamic content | A page reload would be simpler |
| Building a custom composite widget | Radix or a similar library handles it |

**The five ARIA rules:**
1. If you can use native HTML, use native HTML.
2. Do not change native semantics unless necessary (`<h2 role="tab">` is wrong).
3. All interactive ARIA controls must be keyboard operable.
4. Do not use `role="presentation"` or `aria-hidden="true"` on visible focusable elements.
5. All interactive elements must have an accessible name.

### Common ARIA patterns

```tsx
// Modal dialog
<div role="dialog" aria-modal="true" aria-labelledby="dialog-title" aria-describedby="dialog-desc">
  <h2 id="dialog-title">Confirm deletion</h2>
  <p id="dialog-desc">This action cannot be undone.</p>
</div>

// Combobox
<input
  role="combobox"
  aria-expanded={isOpen}
  aria-autocomplete="list"
  aria-controls="listbox-id"
  aria-activedescendant={activeOption?.id}
/>
<ul role="listbox" id="listbox-id">
  <li role="option" aria-selected={isSelected} id="option-1">Option 1</li>
</ul>

// Tab panel
<div role="tablist" aria-label="Settings sections">
  <button role="tab" aria-selected={active === 0} aria-controls="panel-0" id="tab-0">General</button>
  <button role="tab" aria-selected={active === 1} aria-controls="panel-1" id="tab-1">Notifications</button>
</div>
<div role="tabpanel" id="panel-0" aria-labelledby="tab-0" tabindex="0">...</div>

// Breadcrumb
<nav aria-label="Breadcrumb">
  <ol>
    <li><a href="/">Home</a></li>
    <li><a href="/products">Products</a></li>
    <li><span aria-current="page">Widget Pro</span></li>
  </ol>
</nav>

// Progress
<div role="progressbar" aria-valuenow={65} aria-valuemin={0} aria-valuemax={100} aria-label="Upload progress">
  65%
</div>
```

---

## Motion and Animation

```css
/* Respect user motion preference — always */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

**Rules:**
- Animate `transform` and `opacity` only for GPU-accelerated performance. Never animate `width`, `height`, `top`, `left`, or `margin` in loops.
- Entrance animations: ease-out. Exit animations: ease-in. Repositioning: ease-in-out.
- Nothing flashes more than 3 times per second.
- Parallax effects that cover large areas of the viewport must be disableable under `prefers-reduced-motion`.
- Auto-playing carousels and marquees must have pause controls.

---

## Cognitive Accessibility

Cognitive accessibility extends WCAG into readability, memory load, and decision complexity.

**Language and readability:**
- Write at the appropriate reading level for the audience. Avoid jargon in consumer products.
- Use plain language for error messages, instructions, and labels.
- Break long forms into logical sections or steps with clear progress indication.

**Memory and attention:**
- Do not require users to remember information from a previous step to complete the current one.
- Show context inline. Do not hide critical information in tooltips or hover states.
- Provide confirmation dialogs for destructive or irreversible actions.
- Progress indicators for multi-step processes: always show where the user is and how many steps remain.

**Consistency:**
- Same action = same label throughout the interface.
- Same icon = same meaning throughout the interface.
- Consistent placement of primary actions (right side of modals and forms, per platform convention).

**Distraction:**
- No auto-playing audio or video that the user did not initiate.
- Notifications do not interrupt mid-task without urgent cause.
- Animation is purposeful, not decorative.

---

## Focus Management

Focus must always be intentional. When content changes, focus must land somewhere logical.

| Trigger | Focus destination |
|---|---|
| Modal opens | First focusable element inside modal, or the modal heading |
| Modal closes | The element that opened the modal |
| Page navigation (SPA) | Page heading (`<h1>`) or top of new content |
| Inline alert/error appears | Alert element (use `role="alert"`) or move focus to it |
| Action completes and element disappears | Logical next element, or previous element in DOM order |
| Accordion expands | Expanded content is next in Tab order — do not move focus automatically |
| Toast / snackbar appears | Do not move focus — use `aria-live` |

```tsx
// Focus trap for modals
import { FocusTrap } from '@radix-ui/react-focus-trap'  // Radix handles this

// Manual focus return after close
const triggerRef = React.useRef<HTMLButtonElement>(null)
const handleClose = () => {
  setIsOpen(false)
  triggerRef.current?.focus()
}
```

---

## Testing

No accessibility rule is verified without testing. Automated tools catch ~30–40% of issues.
Manual testing catches the rest.

### Automated tooling

| Tool | What it catches |
|---|---|
| axe DevTools (browser extension) | ~50% of WCAG violations, zero false positives |
| Lighthouse (Chrome DevTools) | High-level score, contrast, labels |
| Storybook a11y addon | Component-level axe checks in isolation |
| ESLint jsx-a11y | Missing `alt`, role misuse, interactive element issues at build time |
| Playwright + axe-core | Automated regression tests in CI |

### Manual testing protocol

1. **Keyboard only.** Unplug the mouse. Navigate through every interaction in the page. Confirm:
   - Every interactive element is reachable.
   - Focus is always visible.
   - No keyboard trap (unless in a modal).
   - Tab order is logical.
   - All actions are completable.

2. **Screen reader.** Test with at least one screen reader:
   - macOS/iOS: VoiceOver (`Cmd+F5` to enable)
   - Windows: NVDA (free) or JAWS
   - Android: TalkBack
   Navigate by headings, by landmarks, and by interactive elements. Verify all content is announced correctly.

3. **Zoom to 200%.** Increase browser zoom. Confirm nothing overlaps, truncates, or disappears.

4. **Zoom to 400% / 320px width.** Verify content reflows without horizontal scroll (Reflow, WCAG 1.4.10).

5. **Color contrast.** Use Chrome DevTools color picker or WebAIM Contrast Checker. Check every text/background combination and every UI component against the required ratios.

6. **Reduced motion.** In OS settings, enable "Reduce motion". Verify animations stop.

7. **High contrast mode.** On Windows, enable High Contrast mode. Verify the interface is usable.

8. **Disable CSS.** Verify the reading order and content hierarchy still make sense.

### Audit checklist

**Perceivable:**
- [ ] All images have `alt` text (meaningful images descriptive, decorative images `alt=""`)
- [ ] Color is not the sole conveyor of meaning
- [ ] Text contrast ≥ 4.5:1 (normal), ≥ 3:1 (large text)
- [ ] UI component contrast ≥ 3:1
- [ ] Content reflows at 320px width
- [ ] Text resize to 200% without loss of content

**Operable:**
- [ ] All interactions keyboard accessible
- [ ] No keyboard trap (except intentional modal focus trap)
- [ ] Focus is always visible
- [ ] Skip link present and functional
- [ ] Touch targets ≥ 44×44px
- [ ] No content flashes more than 3× per second
- [ ] Page title is descriptive

**Understandable:**
- [ ] `lang` attribute set on `<html>`
- [ ] Form errors identified in text, associated with field
- [ ] Form fields have visible labels (not placeholder-only)
- [ ] No context changes on focus or input without warning
- [ ] Consistent navigation and labeling across pages

**Robust:**
- [ ] Every interactive element has accessible name, role, state
- [ ] Dynamic content updates announced via `aria-live` or `role="alert"/"status"`
- [ ] Custom widgets follow APG keyboard patterns
- [ ] No ARIA misuse (role on wrong element, incorrect nesting)
