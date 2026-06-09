# Conflict Detection

Handles existing Webflow styles and variables before any push.
Run this check immediately after mode selection, before collecting any values.

---

## When to Run

Always — for both Starter and Developer flows, as soon as the Site ID is confirmed.
Do not wait until push time. Catch conflicts early so the user can decide upfront.

---

## Step 1 — Fetch Existing Styles

Use the Webflow MCP to read the current project state:

1. Fetch all existing variables (colors, typography, spacing)
2. Fetch all existing classes / styles

Store results as `existing_variables` and `existing_classes`.

If the fetch returns empty — project is fresh. Say:

> Fresh project — no existing styles or variables found. We're good to go.

Then continue to template flavor selection.

---

## Step 2 — Identify Conflicts

Compare `existing_variables` and `existing_classes` against the full token list
from `token-schema.md` (or the Developer Excel if already uploaded).

A conflict is any item where the name matches something we would create.

Build two lists:

**Variable conflicts** — existing variables that share a name with tokens we'd create
**Class conflicts** — existing classes that share a name with classes we'd create

---

## Step 3 — Determine Scenario

### Scenario 1 — Fresh Project

No conflicts found.

Say:
> No existing styles found. Starting fresh — let's go.

Proceed to template flavor selection.

---

### Scenario 2 — Partial Setup (most common)

Some conflicts found but not all. Developer has started manually.

Say:

> I found **N existing items** in your Webflow project that overlap with what
> we're about to create.
>
> **Variable conflicts (N):**
> ```
> • color-primary — exists: #000000  →  we'd set: [new value or template]
> • font-size-base — exists: 15px    →  we'd set: 16px
> ```
>
> **Class conflicts (N):**
> ```
> • heading-1  — exists (has styles)  →  we'd overwrite
> • btn-primary — exists (has styles) →  we'd overwrite
> • container  — exists (has styles)  →  we'd overwrite
> ```
>
> **What would you like to do?**
>
> **A — Overwrite all conflicts** — replace existing with new design system values
> **B — Keep all existing** — skip anything that already exists, only create new items
> **C — Decide one by one** — I'll ask you about each conflict individually
> **D — Safe merge (recommended)** — prefix new items that conflict (e.g. `ds-heading-1`)
> so they sit alongside your existing styles. You can migrate gradually.
>
> Reply with A, B, C, or D.

---

### Scenario 3 — Full Setup Exists

More than 80% of tokens already exist. Developer likely has a complete system.

Say:

> Your Webflow project already has a substantial design system set up.
> I found **N existing variables** and **N existing classes** that overlap
> with what we'd create.
>
> Before proceeding, I want to make sure this is intentional.
>
> **What's your goal here?**
>
> **1 — Rebuild from scratch** — clear existing design system and replace with a new one
> *(Warning: this will affect any pages already using these styles)*
>
> **2 — Review what's there** — show me a summary of existing styles so I can
> decide what to keep, update, or replace
>
> **3 — Add only what's missing** — keep everything existing, only create tokens
> and classes that don't already exist
>
> **4 — Safe merge** — prefix all new items (e.g. `ds-`) so nothing existing is touched
>
> Reply with 1, 2, 3, or 4.

If they choose **2 — Review**, output a clean summary of existing styles:

```
EXISTING VARIABLES
──────────────────
Colors (N)
  • color-primary: #value
  • color-secondary: #value
  ...

Typography (N)
  • font-size-base: value
  ...

Spacing (N)
  • spacing-4: value
  ...

EXISTING CLASSES (N)
──────────────────
  • heading-1, heading-2, heading-3
  • btn-primary, btn-secondary
  • container
  ...
```

Then ask:
> Based on what's there, how would you like to proceed?
> (Options 1, 3, or 4 from above)

---

## Step 4 — Handle User Decision

### If Overwrite All (A or 1):

Store `conflict_resolution = overwrite`.
Note in the push step to overwrite existing values.

Warn once before pushing:
> Just to confirm — **N existing styles will be overwritten**.
> Pages using these styles will update immediately after publish.
> Proceeding in 3... or type **stop** to cancel.

---

### If Keep All Existing (B or 3):

Store `conflict_resolution = skip_conflicts`.
Remove all conflicting items from the push list.
Note skipped items in the final report.

---

### If Decide One by One (C):

For each conflict, ask:

> **[token/class name]**
> Current value: [existing value]
> New value: [proposed value]
>
> [K] Keep existing   [O] Overwrite   [S] Skip entirely

Wait for response before moving to next conflict.
After all decisions, summarize choices and confirm before pushing.

---

### If Safe Merge (D or 4):

Ask:
> What prefix would you like to use for new items?
> Default is `ds-` (e.g. `ds-heading-1`, `ds-color-primary`)
> Or type your own prefix.

Store `conflict_resolution = prefix` and `conflict_prefix = [chosen prefix]`.
Apply prefix to all conflicting names only — non-conflicting items keep original names.

Note in the final report:
```
Prefixed items (to avoid conflicts):
  • ds-heading-1  (original name heading-1 already existed)
  • ds-color-primary  (original name color-primary already existed)

Non-conflicting items created with original names:
  • text-muted
  • section-padding-md
  ...
```

---

## Step 5 — Continue to Template Flavor Selection

After conflict resolution is decided (not yet executed — execution happens at push time),
continue the normal flow:

- Starter → template flavor selection → Step 1 of starter-flow.md
- Developer → template flavor selection → generate Excel with conflict resolution noted

---

## Conflict Resolution at Push Time

When `webflow-push.md` executes, check `conflict_resolution` before each item:

- `overwrite` → push regardless, overwrite if exists
- `skip_conflicts` → skip if name exists, create if new
- `one_by_one` → use stored per-item decisions
- `prefix` → apply prefix to conflicting names before pushing
