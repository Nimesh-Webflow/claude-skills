# Starter Flow

Step-by-step guided experience for developers who are new to design systems
or want structured help setting up their Webflow project from scratch.

Read `token-schema.md` for naming rules and valid token structures before pushing anything.

---

## Flow Overview

```
1. Welcome & project context
2. Colors
3. Typography
4. Spacing scale
5. (Optional) Border radius
6. (Optional) Transitions
7. Button styles
8. Global resets
9. Preview summary → confirm → push to Webflow
10. Final report
```

Sections marked optional can be skipped with `/skip`.
Sections marked required cannot be skipped.

---

## Step 1 — Welcome & Project Context (required)

By this point the following are already confirmed from the entry point:
- Webflow MCP connected and Site ID stored
- Conflict detection completed and resolution strategy stored
- Template flavor selected (Modern Minimal / Bold Editorial / none)

Say:

> Let's build your design system step by step.
> One quick question before we start:
>
> What is this project? (e.g. SaaS product, portfolio, agency site, e-commerce)

Store the answer. Use project type as context when giving examples throughout the flow.

Remind the user of their template:
> I'll pre-load **[flavor name]** defaults for each section.
> Just confirm the value or type your own to override it.
> Type `/skip` on optional sections, `/help` anytime you need context.

---

## Step 2 — Colors (required)

Load the selected flavor's color values from `defaults.md`.
Display them as pre-filled suggestions so the user only needs to override.

Say:

> **Step 1 of 6 — Colors**
>
> Here are your color tokens pre-loaded from the **[flavor]** template.
> Confirm each value or type a replacement. Leave blank to keep the default.
>
> ```
> Primary:           [default value]
> Primary Hover:     [default value]  ← auto-generated if left blank
> Secondary:         [default value]
> Accent:            [default value]
> Neutral Light:     [default value]
> Neutral Mid:       [default value]
> Neutral Dark:      [default value]
> Text Default:      [default value]
> Text Muted:        [default value]
> Background:        [default value]
> Background Subtle: [default value]
> Background Dark:   [default value]
> Success:           [default value]
> Warning:           [default value]
> Error:             [default value]
> ```
>
> Reply with **"all good"** to accept all defaults, paste your overrides,
> or type `/help` if you need guidance.

**Validation rules:**
- Accept hex (#RRGGBB, #RGB), rgba(), or hsl() values
- If a value looks malformed, flag it immediately with a correction suggestion
- If Primary Hover is not provided, auto-generate a 10% darkened version and mention it
- Minimum required: Primary, Text Default, Background

**On /help for this step:**
> **Colors** are the foundation of your design system. Instead of typing a hex code
> every time you style something in Webflow, you create a variable once and reference
> it everywhere. If your brand color changes, you update one variable and everything updates.
>
> **Primary** = your main brand color (buttons, links, highlights)
> **Neutral scale** = grays used for text, borders, backgrounds
> **Semantic colors** = success/warning/error states in forms, alerts, badges

---

## Step 3 — Typography (required)

Say:

> **Step 2 of 6 — Typography**
>
> Now let's define your type system. We'll set up font families, the sizes you
> actually use, weights, and line heights.
>
> **Font families:**
> What fonts does this project use?
>
> ```
> Primary font (body/UI):   e.g. Inter
> Display font (headings):  e.g. Cal Sans  ← leave blank if same as primary
> Mono font (code):         e.g. JetBrains Mono  ← leave blank if not used
> ```

After font families are collected, continue:

> **Heading sizes:**
> Share the font sizes for your headings (H1–H4 minimum):
>
> ```
> H1:  e.g. 64px
> H2:  e.g. 48px
> H3:  e.g. 32px
> H4:  e.g. 24px
> H5:  e.g. 20px  ← optional
> H6:  e.g. 18px  ← optional
> ```
>
> **Body text sizes:**
> ```
> Large:   e.g. 18px
> Default: e.g. 16px
> Small:   e.g. 14px
> XSmall:  e.g. 12px  ← optional
> ```
>
> **Font weights used** (only list what your design actually uses):
> ```
> e.g. Regular (400), Medium (500), Bold (700)
> ```
>
> **Line heights:**
> ```
> Tight (headings):   e.g. 1.2
> Normal (body):      e.g. 1.5
> Relaxed (long text): e.g. 1.65  ← optional
> ```
>
> Type `/help` if you need guidance on any of these.

**Validation rules:**
- Accept px, rem, or unitless values for line height
- If rem values are given for font sizes, convert to px equivalent and confirm with user
- Minimum required: H1, H2, H3, Body Default, font-weight-regular, line-height-normal

**On /help for this step:**
> **Typography variables** mean you define your type scale once and reuse it across
> all heading and text classes. Change `font-size-3xl` from 40px to 44px and every
> H2 on the site updates instantly.
>
> **Line height** controls the space between lines of text. Tighter (1.2) works
> for large headings. Looser (1.5–1.65) works for body text readability.
>
> Only share sizes you actually use — we're not creating the full scale, just what's in your design.

---

## Step 4 — Spacing Scale (optional — /skip allowed)

Say:

> **Step 3 of 6 — Spacing Scale**
>
> Spacing tokens eliminate the guesswork of padding and margin values across the project.
> We'll set up a minimal scale — just the steps you actually use.
>
> Most projects work well with an 8px base scale. Here's a suggested starting point:
>
> ```
> spacing-1:  4px
> spacing-2:  8px
> spacing-3:  12px
> spacing-4:  16px
> spacing-5:  24px
> spacing-6:  32px
> spacing-7:  48px
> spacing-8:  64px
> spacing-9:  96px
> ```
>
> And for section padding (the most repetitive manual work):
> ```
> Section Small:   e.g. 64px
> Section Medium:  e.g. 96px  ← most common default
> Section Large:   e.g. 128px
> Container width: e.g. 1280px
> ```
>
> Reply with:
> - **"Use suggested"** to accept the defaults above
> - **Your own values** if your design uses a different scale
> - `/skip` to skip spacing tokens entirely

**On /help for this step:**
> **Spacing tokens** are especially useful for section padding — the top and bottom
> space on every section of your site. Instead of typing 96px manually on every section,
> you apply one class (`section-padding-md`) and it references the variable.
>
> The numbered scale (spacing-1 through spacing-9) is used for gaps, margins,
> and padding inside components. You don't need all of them — just the values
> you actually reach for.

---

## Step 5 — Border Radius (optional — /skip allowed)

Say:

> **Step 4 of 6 — Border Radius** *(optional)*
>
> Do you use consistent border radius values across your design?
> (cards, buttons, inputs, badges, etc.)
>
> ```
> Small:  e.g. 4px   ← inputs, tags
> Medium: e.g. 8px   ← cards, modals
> Large:  e.g. 12px  ← featured sections
> Pill:   e.g. 9999px ← pill buttons, badges
> ```
>
> Reply with your values, **"Use suggested"**, or `/skip`.

---

## Step 6 — Transitions (optional — /skip allowed)

Say:

> **Step 5 of 6 — Transitions** *(optional)*
>
> Do you want consistent transition speeds for hover states and animations?
>
> ```
> Fast:    e.g. 150ms ease   ← micro-interactions
> Default: e.g. 250ms ease   ← buttons, links
> Slow:    e.g. 400ms ease   ← modals, panels
> ```
>
> Reply with your values, **"Use suggested"**, or `/skip`.

---

## Step 7 — Button Styles (required)

Say:

> **Step 6 of 6 — Button Styles**
>
> Let's define your button variants. We'll create `btn-primary` and `btn-secondary`
> as the baseline, plus size variants if needed.
>
> For each button, share:
>
> **Primary button** (filled, main CTA):
> ```
> Background:      e.g. color-primary (or hex)
> Text color:      e.g. #FFFFFF
> Border:          e.g. none
> Border radius:   e.g. radius-md (or 8px)
> Padding:         e.g. 14px 28px
> Font size:       e.g. font-size-base
> Font weight:     e.g. font-weight-semibold
> Hover bg:        e.g. color-primary-hover
> ```
>
> **Secondary button** (outlined or ghost):
> ```
> Background:      e.g. transparent
> Text color:      e.g. color-primary
> Border:          e.g. 2px solid color-primary
> Hover bg:        e.g. color-primary (with white text)
> ```
>
> **Size variants** (optional):
> ```
> Small:  padding e.g. 10px 20px, font-size e.g. font-size-sm
> Large:  padding e.g. 18px 36px, font-size e.g. font-size-lg
> ```
>
> You can reference variable names (like `color-primary`) or give raw hex values.
> Type `/help` for guidance.

**On /help for this step:**
> Button classes save time because every CTA on the site shares the same base styles.
> When your client wants to change the button color, you update one variable.
>
> **Primary** = the main action button (buy, sign up, get started)
> **Secondary** = a softer option (learn more, view demo)
> Referencing variables (like `color-primary`) instead of raw hex means
> buttons update automatically when your color tokens change.

---

## Step 8 — Global Resets (required, auto-applied)

No user input needed for this step. Inform the user:

> **Global Resets**
>
> I'll include these standard resets automatically — they eliminate the most
> common browser inconsistencies and are safe for every Webflow project:
>
> ```css
> *, *::before, *::after { box-sizing: border-box; }
> body { margin: 0; }
> img, video { max-width: 100%; display: block; }
> a { text-decoration: none; color: inherit; }
> button { cursor: pointer; border: none; background: none; }
> ul, ol { list-style: none; margin: 0; padding: 0; }
> h1, h2, h3, h4, h5, h6 { margin: 0; }
> p { margin: 0; }
> ```
>
> These go into your Webflow global styles / custom code head.
> Reply **"looks good"** or let me know if you want to remove any of these.

---

## Step 9 — Preview Summary & Confirmation

Before pushing anything to Webflow, generate a full preview:

Say:

> **Review before we push**
>
> Here's everything that will be created in your Webflow project:
>
> [Generate a structured summary in this format:]

```
VARIABLES (Webflow Variables panel)
─────────────────────────────────
Colors (N variables)
  • color-primary: #value
  • color-secondary: #value
  ... all color tokens

Typography (N variables)
  • font-primary: value
  • font-size-h1: value
  ... all type tokens

Spacing (N variables)
  • spacing-4: 16px
  ... all spacing tokens

[Border Radius if configured]
[Transitions if configured]

CLASSES (Webflow Style panel)
─────────────────────────────
Headings
  • heading-1 → font: font-primary, size: font-size-h1, weight: bold, line-height: tight
  ... h2 through h4

Text styles
  • text-large, text-base, text-small, text-muted, text-inverse

Buttons
  • btn-primary → [all properties]
  • btn-secondary → [all properties]
  [size variants if configured]

Layout
  • container → max-width: Npx, margin: 0 auto
  • section-padding-sm/md/lg

Global resets
  • Applied to body and * selector

SKIPPED SECTIONS
  • [list any sections the user skipped]
```

> **Ready to push to Webflow?**
> Reply **"yes, push it"** to create everything above, or tell me what to change first.

---

## Step 10 — Push to Webflow

Once confirmed, follow `webflow-push.md` to execute the push via Webflow MCP.

Push in this order:
1. Variables (colors first, then typography, then spacing, then effects)
2. Global resets (custom code)
3. Typography classes
4. Layout classes (container, section padding)
5. Button classes

After each group, confirm success before moving to the next.

---

## Step 11 — Final Report

After all pushes are complete, output:

> **Done! Here's what was created:**
>
> ✅ N color variables
> ✅ N typography variables
> ✅ N spacing variables
> [✅ border radius / transitions if configured]
> ✅ N classes created
> ✅ Global resets applied
> ⏭ Skipped: [sections skipped]
>
> **Next steps:**
> - Open your Webflow Designer → Variables panel to verify tokens
> - Apply `heading-1` through `heading-4` to your text elements
> - Use `btn-primary` and `btn-secondary` on all CTA elements
> - Apply `section-padding-md` to your sections for consistent vertical rhythm
> - Apply `container` to your wrapper divs for max-width control
>
> Your design system baseline is live. Want to continue with component-level styles
> or is this a good stopping point?
