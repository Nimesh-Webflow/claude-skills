# Developer Flow

Fast-track experience for developers who already know their values and want
to fill a structured file and push everything to Webflow in one shot.

Read `token-schema.md` for naming conventions before generating or validating the Excel file.

---

## Flow Overview

```
1. Generate Excel template → send to developer
2. Developer fills values → re-uploads
3. Validate uploaded file
4. Preview summary → confirm
5. Push to Webflow
6. Final report
```

---

## Step 1 — Generate Excel Template

When the user selects Developer mode, say:

> **Developer mode — let's move fast.**
>
> I'll generate a pre-structured Excel file with all the class names and token names
> already filled in. Your job:
>
> 1. Download the file
> 2. Fill in your values (only the Value column — everything else is pre-filled)
> 3. Add any extra classes you need in the Custom sheet
> 4. Mark anything you don't want with **SKIP** in the Skip column
> 5. Re-upload here and I'll push everything to Webflow
>
> Generating your template now...

Then generate the Excel file using the spec below.

---

## Excel File Spec

File name: `webflow-design-system.xlsx`

### Sheet structure:

The file has 6 sheets:

1. **README** — instructions tab (read-only looking, gray background)
2. **Colors** — color tokens
3. **Typography** — type tokens and classes
4. **Spacing** — spacing scale
5. **Buttons** — button class definitions
6. **Custom** — developer's own additions

---

### Sheet 1: README

Content (plain text, no table):

```
WEBFLOW DESIGN SYSTEM — SETUP FILE
────────────────────────────────────────────────────────

HOW TO USE THIS FILE:
1. Fill in the VALUE column on each sheet with your design values
2. Leave Class Name and Property columns as-is — they are pre-configured
3. In the SKIP column, type "SKIP" for any row you don't want created
4. Use the Custom sheet to add your own classes and variables
5. Save and re-upload to Claude when done

NAMING RULES:
- All names use kebab-case (e.g. color-primary, heading-1)
- Name by role, not by value (e.g. color-primary not color-blue)
- Variable names reference Webflow Variables panel
- Class names reference Webflow Style panel

QUESTIONS? Type /help in the chat at any time.
```

---

### Sheet 2: Colors

Columns: `Token Name` | `Value` | `Example` | `Skip` | `Notes`

Pre-filled rows:

| Token Name | Value | Example | Skip | Notes |
|---|---|---|---|---|
| color-primary | | #3B5BDB | | Main brand color |
| color-primary-hover | | #364FC7 | | Auto-generated if left blank |
| color-secondary | | #7950F2 | | Supporting brand color |
| color-accent | | #F03E3E | | CTA / highlight color |
| color-neutral-100 | | #F8F9FA | | Lightest gray |
| color-neutral-300 | | #DEE2E6 | | Light gray |
| color-neutral-500 | | #ADB5BD | | Mid gray |
| color-neutral-700 | | #495057 | | Dark gray |
| color-neutral-900 | | #212529 | | Darkest gray |
| color-text-default | | #212529 | | Default body text |
| color-text-muted | | #868E96 | | Secondary text |
| color-text-inverse | | #FFFFFF | | Text on dark bg |
| color-bg-default | | #FFFFFF | | Page background |
| color-bg-subtle | | #F8F9FA | | Subtle section bg |
| color-bg-dark | | #212529 | | Dark section bg |
| color-success | | #2F9E44 | | Success state |
| color-warning | | #F08C00 | | Warning state |
| color-error | | #E03131 | | Error state |

---

### Sheet 3: Typography

**Section A — Font Families**

Columns: `Token Name` | `Value` | `Example` | `Skip` | `Notes`

| Token Name | Value | Example | Skip | Notes |
|---|---|---|---|---|
| font-primary | | Inter | | Body and UI font |
| font-display | | Cal Sans | | Headings (leave blank if same as primary) |
| font-mono | | JetBrains Mono | | Code font (leave blank if not used) |

**Section B — Font Sizes**

| Token Name | Value | Example | Skip | Notes |
|---|---|---|---|---|
| font-size-xs | | 12px | | Extra small text |
| font-size-sm | | 14px | | Small text, captions |
| font-size-base | | 16px | | Default body size |
| font-size-md | | 18px | | Large body / lead text |
| font-size-lg | | 20px | | Small headings |
| font-size-xl | | 24px | | H4 range |
| font-size-2xl | | 32px | | H3 range |
| font-size-3xl | | 40px | | H2 range |
| font-size-4xl | | 48px | | H1 range |
| font-size-5xl | | 64px | | Display heading |

**Section C — Font Weights**

| Token Name | Value | Example | Skip | Notes |
|---|---|---|---|---|
| font-weight-regular | | 400 | | Default body weight |
| font-weight-medium | | 500 | | Medium emphasis |
| font-weight-semibold | | 600 | | Subheadings, labels |
| font-weight-bold | | 700 | | Headings, strong CTAs |

**Section D — Line Heights**

| Token Name | Value | Example | Skip | Notes |
|---|---|---|---|---|
| line-height-tight | | 1.2 | | Large headings |
| line-height-snug | | 1.35 | | Subheadings |
| line-height-normal | | 1.5 | | Body text |
| line-height-relaxed | | 1.65 | | Long-form content |

**Section E — Typography Classes**

Columns: `Class Name` | `Font Size Token` | `Font Weight Token` | `Line Height Token` | `Font Family Token` | `Skip` | `Notes`

| Class Name | Font Size Token | Font Weight Token | Line Height Token | Font Family Token | Skip | Notes |
|---|---|---|---|---|---|---|
| heading-1 | font-size-5xl | font-weight-bold | line-height-tight | font-display | | |
| heading-2 | font-size-4xl | font-weight-bold | line-height-tight | font-display | | |
| heading-3 | font-size-3xl | font-weight-semibold | line-height-snug | font-display | | |
| heading-4 | font-size-2xl | font-weight-semibold | line-height-snug | font-primary | | |
| heading-5 | font-size-xl | font-weight-medium | line-height-normal | font-primary | | |
| heading-6 | font-size-lg | font-weight-medium | line-height-normal | font-primary | | |
| text-large | font-size-md | font-weight-regular | line-height-normal | font-primary | | |
| text-base | font-size-base | font-weight-regular | line-height-normal | font-primary | | |
| text-small | font-size-sm | font-weight-regular | line-height-normal | font-primary | | |
| text-muted | font-size-base | font-weight-regular | line-height-normal | font-primary | | Applies color-text-muted |
| text-inverse | font-size-base | font-weight-regular | line-height-normal | font-primary | | Applies color-text-inverse |

---

### Sheet 4: Spacing

**Section A — Spacing Scale Variables**

Columns: `Token Name` | `Value` | `Default` | `Skip` | `Notes`

| Token Name | Value | Default | Skip | Notes |
|---|---|---|---|---|
| spacing-1 | | 4px | | Micro spacing |
| spacing-2 | | 8px | | Base unit |
| spacing-3 | | 12px | | |
| spacing-4 | | 16px | | Common gap |
| spacing-5 | | 24px | | |
| spacing-6 | | 32px | | |
| spacing-7 | | 48px | | |
| spacing-8 | | 64px | | |
| spacing-9 | | 96px | | |
| spacing-section-sm | | 64px | | Section padding small |
| spacing-section-md | | 96px | | Section padding default |
| spacing-section-lg | | 128px | | Section padding large |
| spacing-container | | 1280px | | Max content width |

**Section B — Spacing Classes**

Columns: `Class Name` | `Property` | `Token Reference` | `Skip` | `Notes`

| Class Name | Property | Token Reference | Skip | Notes |
|---|---|---|---|---|
| section-padding-sm | padding-top + padding-bottom | spacing-section-sm | | |
| section-padding-md | padding-top + padding-bottom | spacing-section-md | | Most common |
| section-padding-lg | padding-top + padding-bottom | spacing-section-lg | | |
| container | max-width + margin-left + margin-right | spacing-container + auto | | |

---

### Sheet 5: Buttons

Columns: `Property` | `btn-primary` | `btn-secondary` | `btn-sm` | `btn-lg` | `Skip` | `Notes`

| Property | btn-primary | btn-secondary | btn-sm | btn-lg | Skip | Notes |
|---|---|---|---|---|---|---|
| background | | | | | | Use token name or hex |
| text-color | | | | | | |
| border | | | | | | e.g. none or 2px solid color-primary |
| border-radius | | | | | | Token name or px value |
| padding | | | | | | e.g. 14px 28px |
| font-size | | | | | | Token name or px value |
| font-weight | | | | | | Token name or numeric |
| hover-background | | | | | | |
| hover-text-color | | | | | | Leave blank if unchanged |
| transition | | | | | | Token name or value |

Pre-fill btn-sm and btn-lg columns with SKIP by default — developer removes SKIP if they want size variants.

---

### Sheet 6: Custom

For developer-added classes and variables not covered in the standard sheets.

Columns: `Type` | `Name` | `Property` | `Value` | `Notes`

| Type | Name | Property | Value | Notes |
|---|---|---|---|---|
| variable | | | | e.g. color, spacing, font |
| class | | | | CSS property: value pairs |

First 3 rows pre-filled as examples with light gray background:

| variable | color-brand-alt | | #FF6B6B | Example — delete this row |
| class | badge-primary | background + color + border-radius + padding | color-primary + white + radius-full + 4px 12px | Example — delete this row |
| class | text-gradient | background + -webkit-background-clip + color | gradient value + text + transparent | Example — delete this row |

---

## Step 2 — Handling the Upload

When the developer re-uploads the file:

1. Parse all 6 sheets
2. Skip any row where Skip column contains "SKIP" (case-insensitive)
3. Skip any row where Value column is empty (treat as not configured)
4. For `color-primary-hover` — if empty, auto-generate 10% darkened version of `color-primary`
5. Validate all values against token-schema.md naming and format rules
6. Flag any issues before proceeding — do not silently skip malformed values

**Validation checks:**
- Color values: valid hex, rgba, or hsl format
- Font size values: px or rem only
- Font weight: numeric (100–900) or keyword (regular, medium, bold)
- Line height: unitless decimal (1.0–2.0) or px
- Spacing: px values only
- Padding shorthand: valid CSS shorthand (e.g. 14px 28px or 14px 28px 14px 28px)
- Token references in classes: must match a token defined in the same file

If validation errors found, say:

> I found a few issues in your file before pushing:
>
> [list each issue with sheet name, row/token name, and what's wrong]
>
> Fix these and re-upload, or tell me to skip the affected rows.

---

## Step 3 — Preview Summary & Confirmation

Same format as starter-flow.md Step 9. Generate a full structured summary of everything
that will be created, grouped by Variables and Classes.

Then ask:

> Everything look right? Reply **"yes, push it"** to create all of the above in Webflow,
> or tell me what to adjust first.

---

## Step 4 — Push to Webflow

Follow `webflow-push.md` for the push sequence.

Same push order as starter flow:
1. Variables (colors → typography → spacing → effects)
2. Global resets
3. Typography classes
4. Layout classes
5. Button classes
6. Custom variables and classes

---

## Step 5 — Final Report

Same format as starter-flow.md Step 11.

Additionally, for Developer mode, output a **token manifest** — a clean summary the developer
can save as project documentation:

> **Token Manifest — [Project Name]**
> Generated: [date]
>
> [List every variable name and its value in a copyable format]
> [List every class name and its key properties]
