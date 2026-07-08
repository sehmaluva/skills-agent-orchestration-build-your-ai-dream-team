# Project Pulse Implementation Plan

## Summary
Build a static, polished **Project Pulse** dashboard that renders project cards from `app/project-data.json`, styles them in `app/styles.css`, and runs via a VS Code launch profile in `.vscode/launch.json` that opens `app/index.html` (not a directory listing).

## Roles and Responsibilities

### Designer
- Define dashboard information hierarchy (title, project cards, status/activity/priority visibility).
- Specify accessible, polished visual system (spacing, contrast, badges, responsive card layout).
- Provide deterministic CSS hook guidance (`.dashboard`, `.project-card`) and UI states (loading/error/empty).
- Review final UI for readability, accessibility, and visual consistency.

### Coder
- Implement HTML structure and data rendering in `app/index.html`.
- Implement final styling in `app/styles.css` based on Designer guidance.
- Author valid data schema/content in `app/project-data.json` (`projects` array with required fields).
- Create strict JSON `.vscode/launch.json` for **Run Project Pulse Dashboard** using `python3 -m http.server 5500`, serving from `app/`, opening `http://localhost:%s/index.html`.
- Execute validation checks and report completion evidence.

---

## Ordered Implementation Steps (Phases)

## Phase 1 — Scope + UX/Data contract
1. Confirm required fields and UI outputs from brief/workflow checks.
2. Define project card content contract and status/priority display rules.
3. Decide fallback behavior for empty/invalid/unreachable data.

**File assignments**
- Planning only (no file edits required yet).

## Phase 2 — Content/data foundation
4. Create `app/project-data.json` with top-level `projects` key.
5. Add multiple project objects with `name`, `owner`, `status`, `recentActivity`, `priority`.

**File assignments**
- **Coder**: `app/project-data.json`
- **Designer (review)**: data readability/label semantics guidance

## Phase 3 — Dashboard structure + rendering
6. Build `app/index.html` with:
   - Exact title text: `Project Pulse`
   - Reference to `styles.css`
   - Reference/loading path for `project-data.json`
   - Rendered project cards using `project-card` class
   - Visible `status`, `recentActivity`, and `priority` fields
7. Add semantic landmarks and accessible labels/headings.

**File assignments**
- **Coder**: `app/index.html`
- **Designer (review)**: hierarchy/accessibility

## Phase 4 — Visual polish
8. Implement `app/styles.css` with:
   - `.dashboard` and `.project-card` selectors
   - `border-radius` and `box-shadow`
   - Responsive layout behavior and readable spacing
   - Clear visual distinction for status/priority indicators

**File assignments**
- **Designer (lead)** + **Coder (implementation)**: `app/styles.css`

## Phase 5 — Local run/debug configuration
9. Create `.vscode/launch.json` (strict JSON, no comments) with launch configuration:
   - Name: `Run Project Pulse Dashboard`
   - Command: `python3 -m http.server 5500`
   - Working directory: `${workspaceFolder}/app`
   - `serverReadyAction` opening `http://localhost:%s/index.html`

**File assignments**
- **Coder**: `.vscode/launch.json`

## Phase 6 — validation + readiness
10. Validate file existence/content requirements and JSON parsing.
11. Run launch profile and confirm dashboard opens `index.html` with rendered cards.
12. Capture unresolved risks/limitations.

**File assignments**
- Verification across: `app/index.html`, `app/styles.css`, `app/project-data.json`, `.vscode/launch.json`

---

## File Ownership / Assignment Table

| File | Primary Owner | Supporting Role | Notes |
|---|---|---|---|
| `app/index.html` | Coder | Designer (UX/a11y review) | Structure, rendering, field visibility |
| `app/styles.css` | Designer (design direction) | Coder (implementation) | Must include `.dashboard`, `.project-card`, `border-radius`, `box-shadow` |
| `app/project-data.json` | Coder | Designer (content clarity review) | Top-level `projects`, required fields per item |
| `.vscode/launch.json` | Coder | — | Strict JSON, deterministic launch behavior |

---

## Dependencies Between Steps
- Phase 1 -> Phases 2, 3, 4, 5 (contract first).
- Phase 2 -> Phase 3 (UI rendering depends on data shape).
- Phase 3 -> Phase 4 (styling depends on stable markup/classes).
- Phases 2/3/4 -> Phase 6 (validation after implementation).
- Phase 5 -> Phase 6 (run/debug validation requires launch config).

---

## Parallel vs Sequential Work

### Can run in parallel
- Phase 2 (`app/project-data.json`) and initial Phase 5 (`.vscode/launch.json`)  
  **Reason:** independent file scopes; no direct content coupling.
- Designer’s visual direction for Phase 4 can begin while Coder builds Phase 3 structure  
  **Reason:** style system and layout intent can be drafted before final markup lock.

### Must be sequential
- Phase 1 before all build work  
  **Reason:** prevents rework from unclear requirements.
- Final `app/styles.css` polish after `app/index.html` class/structure stabilize  
  **Reason:** avoids selector churn and merge conflicts.
- Final validation after all four files exist  
  **Reason:** completion criteria spans all deliverables.

---

## Edge Cases to Handle
- `project-data.json` missing/unreadable -> show clear in-page error state.
- `projects` exists but empty -> show “no active projects” empty state.
- Project object missing required fields -> render safe fallback text (not broken card).
- Long values (owner/activity) -> prevent layout overflow/wrapping issues.
- Unknown `status`/`priority` values -> apply default badge styling.
- Launch opens directory root instead of page -> enforce URL target `index.html`.

---

## validation Expectations (Acceptance Checklist)
- [ ] `app/index.html` exists and includes `Project Pulse`.
- [ ] `app/index.html` references `styles.css`.
- [ ] `app/index.html` references/loads `project-data.json`.
- [ ] `app/index.html` renders cards with `project-card` and shows `status`, `recentActivity`, `priority`.
- [ ] `app/styles.css` includes `.dashboard`, `.project-card`, `border-radius`, `box-shadow`.
- [ ] `app/project-data.json` parses as JSON and includes top-level `projects`.
- [ ] Each project includes `name`, `owner`, `status`, `recentActivity`, `priority`.
- [ ] `.vscode/launch.json` parses as JSON and includes `Run Project Pulse Dashboard`.
- [ ] Launch uses `python3 -m http.server 5500`, serves from `app/`, opens `http://localhost:%s/index.html`.
- [ ] Manual run confirms browser opens dashboard UI (not directory listing).

---

## Open Questions
1. How many seed projects should be included initially (minimum viable count)?
2. Should `priority` vocabulary be fixed (`Low/Medium/High`) or free-form?
3. Should status-to-color mapping be strictly defined now or left flexible?
4. If data load fails, should UI retry automatically or only show an error state?
