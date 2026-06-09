---
name: webflow-design-system
description: >
  Use this skill when a Webflow developer wants to set up a design system, style variables,
  typography classes, color tokens, spacing utilities, button styles, or global resets in Webflow.
  Trigger when the user mentions setting up Webflow styles from scratch, creating a design system
  baseline, importing design tokens into Webflow, or reducing manual styling setup. Also trigger
  for phrases like "Webflow starter styles", "set up Webflow variables", "Webflow typography classes",
  "design system for Webflow", or "Client First inspired setup". Always use this skill before
  the user starts manually creating variables or classes in Webflow.
---

# Webflow Design System Skill

A guided workflow to help Webflow developers set up a clean, production-ready design system
baseline — covering variables, typography, spacing, colors, buttons, and global resets.
Inspired by Finsweet Client First principles but scoped to what actually matters.

---

## Entry Point

When this skill is triggered, run this entry point flow exactly as described below.

---

### Step 1 — Webflow MCP Check

Before anything else, verify the user has Webflow connected via MCP.

Say exactly this:

> Before we start, I need to confirm your Webflow project is connected.
>
> **Check:** Is the Webflow MCP connected in your Claude settings?
> - If **yes** — share your Webflow Site ID and we'll get started.
> - If **no** — go to Claude Settings → Integrations → Connect Webflow, then come back.
>
> Once connected, I'll be pushing your design system variables and classes directly
> into Webflow — no copy-pasting needed.

Wait for the user to confirm connection and provide their Site ID before proceeding.

If the user is unsure how to find their Site ID, explain:
> Your Site ID is in your Webflow project URL:
> `https://webflow.com/design/SITE-ID-HERE`
> Or go to Project Settings → General → Site ID.

---

### Step 2 — Conflict Detection

Before mode selection, run conflict detection.
Follow `references/conflict-detection.md` exactly.

- Fetch existing variables and classes from the Webflow project via MCP
- Determine which scenario applies (fresh / partial / full)
- Resolve the conflict strategy with the user before proceeding
- Store the resolution for use at push time

Do not skip this step even if the user says the project is new — always verify via MCP.

---

### Step 3 — Template Flavor Selection

Once conflict resolution is confirmed, ask the user to pick a template flavor.
This applies to both modes — the flavor sets default values for any token not provided.

Say:

> Before we dive in, pick a starting point for your design system.
> You can override any value — this just sets smart defaults so nothing is left blank.
>
> 🔵 **Modern Minimal**
> Clean, professional, SaaS-ready. Inter font, strong blue primary, tight spacing.
> Best for: SaaS products, dashboards, portfolios, startups.
>
> 🖤 **Bold Editorial**
> Strong typographic contrast, generous spacing, expressive personality.
> Best for: Creative agencies, design studios, luxury brands, editorial sites.
>
> Reply with **Minimal** or **Editorial** to continue.
> Or type **none** if you want to provide all values yourself with no defaults.

Store the selected flavor. Reference `references/defaults.md` for all token values.

---

### Step 4 — Mode Selection

Once flavor is confirmed, present the two modes:

> Great. Now let's choose how you want to work:
>
> 🟢 **Starter** — Best if you're new to design systems or want step-by-step guidance.
> I'll walk you through colors, typography, spacing, and buttons one section at a time.
> Your template defaults are pre-loaded — just confirm or override each value.
> Type `/help` at any point for an explanation of what I'm asking.
>
> ⚡ **Developer** — Best if you already know your values.
> I'll generate a pre-filled Excel file based on your chosen template.
> Override what you need, upload it back, and I'll push everything to Webflow.
>
> Reply with **Starter** or **Developer** to continue.

---

### Step 5 — Route to Mode

Based on the user's reply:

- If **Starter** → follow `references/starter-flow.md`
- If **Developer** → follow `references/developer-flow.md`

Pass through: selected flavor, conflict resolution strategy, Site ID.

---

## Global Rules (apply to both modes)

These rules apply throughout the entire skill regardless of mode:

**Naming conventions:**
- All class names: kebab-case only (e.g. `heading-1`, `text-muted`, `btn-primary`)
- All variable names: kebab-case, semantic not value-based (e.g. `color-primary` not `color-blue-500`)
- No abbreviations unless universally understood (e.g. `btn` is fine, `typ` is not)

**Scope discipline:**
- Only create what is scoped to this skill: colors, typography, spacing scale, buttons, global resets
- Do not create every possible utility class — only the ones that eliminate the most repetitive manual work
- If the user requests something outside scope, note it and offer to handle it after the core setup

**Before pushing to Webflow:**
- Always show a preview summary of everything that will be created
- Wait for explicit confirmation before making any changes
- After pushing, output a final report of what was created

**Conflict awareness:**
- Always fetch existing Webflow styles via MCP before collecting any values
- Never assume a project is fresh — verify it
- Follow conflict-detection.md for the full decision flow
- Store conflict resolution strategy and apply it at push time

---

## /help Command

If the user types `/help` at any point, refer to the current step they are on and explain:
- What is being asked
- Why it matters for the design system
- What a good example looks like

The `/help` response should be concise — 3 to 5 lines max. Not a lecture.

---

## /skip Command

If the user types `/skip` at any point during the Starter flow, skip the current optional
section and move to the next one. Mark skipped sections in the final summary as "not configured".

Sections that can be skipped: spacing scale, border radius, transitions.
Sections that cannot be skipped: colors, typography, global resets.

---

## Reference Files

- `references/starter-flow.md` — Step by step guided flow for beginners
- `references/developer-flow.md` — Excel spec, upload handling, and push logic
- `references/token-schema.md` — Shared naming rules and variable structure
- `references/webflow-push.md` — How to create variables and classes via Webflow MCP
- `references/defaults.md` — Modern Minimal and Bold Editorial template values
- `references/conflict-detection.md` — Conflict detection and resolution logic
