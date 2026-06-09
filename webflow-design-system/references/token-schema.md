# Token Schema & Naming Rules

Shared across both Starter and Developer flows. This is the source of truth for how
all design tokens are structured before being pushed to Webflow.

---

## Color Tokens

### Required categories:
| Token Name | Purpose | Example Value |
|---|---|---|
| `color-primary` | Main brand color | #3B5BDB |
| `color-primary-hover` | Hover state of primary | #364FC7 |
| `color-secondary` | Supporting brand color | #7950F2 |
| `color-accent` | Highlight / CTA color | #F03E3E |
| `color-neutral-100` | Lightest neutral (near white) | #F8F9FA |
| `color-neutral-300` | Light neutral | #DEE2E6 |
| `color-neutral-500` | Mid neutral | #ADB5BD |
| `color-neutral-700` | Dark neutral | #495057 |
| `color-neutral-900` | Darkest neutral (near black) | #212529 |
| `color-text-default` | Default body text | #212529 |
| `color-text-muted` | Secondary / subdued text | #868E96 |
| `color-text-inverse` | Text on dark backgrounds | #FFFFFF |
| `color-bg-default` | Default page background | #FFFFFF |
| `color-bg-subtle` | Subtle section background | #F8F9FA |
| `color-bg-dark` | Dark section background | #212529 |
| `color-success` | Success state | #2F9E44 |
| `color-warning` | Warning state | #F08C00 |
| `color-error` | Error state | #E03131 |

### Optional (only if used in the design):
- `color-info` — informational state
- `color-border-default` — default border color
- `color-border-subtle` — light divider color

---

## Typography Tokens

### Font family variables:
| Token Name | Purpose |
|---|---|
| `font-primary` | Main body and UI font |
| `font-display` | Heading / display font (if different) |
| `font-mono` | Code / monospace (only if used) |

### Type scale (font size variables):
| Token Name | Typical Value |
|---|---|
| `font-size-xs` | 12px |
| `font-size-sm` | 14px |
| `font-size-base` | 16px |
| `font-size-md` | 18px |
| `font-size-lg` | 20px |
| `font-size-xl` | 24px |
| `font-size-2xl` | 32px |
| `font-size-3xl` | 40px |
| `font-size-4xl` | 48px |
| `font-size-5xl` | 64px |

Only create sizes that are actually used. Do not create the full scale by default.

### Font weight variables:
| Token Name | Value |
|---|---|
| `font-weight-regular` | 400 |
| `font-weight-medium` | 500 |
| `font-weight-semibold` | 600 |
| `font-weight-bold` | 700 |

Only include weights that are used in the project.

### Line height variables:
| Token Name | Value |
|---|---|
| `line-height-tight` | 1.2 |
| `line-height-snug` | 1.35 |
| `line-height-normal` | 1.5 |
| `line-height-relaxed` | 1.65 |

---

## Spacing Tokens

Use an 8px base scale. Only include steps that are actually used in the design.
Never create every possible spacing value.

| Token Name | Value |
|---|---|
| `spacing-1` | 4px |
| `spacing-2` | 8px |
| `spacing-3` | 12px |
| `spacing-4` | 16px |
| `spacing-5` | 24px |
| `spacing-6` | 32px |
| `spacing-7` | 48px |
| `spacing-8` | 64px |
| `spacing-9` | 80px |
| `spacing-10` | 96px |
| `spacing-section-sm` | 64px — small section padding |
| `spacing-section-md` | 96px — default section padding |
| `spacing-section-lg` | 128px — large section padding |
| `spacing-container` | Max-width of content container |

---

## Border Radius Tokens (optional)

| Token Name | Value |
|---|---|
| `radius-sm` | 4px |
| `radius-md` | 8px |
| `radius-lg` | 12px |
| `radius-full` | 9999px (pill shape) |

---

## Transition Tokens (optional)

| Token Name | Value |
|---|---|
| `transition-fast` | 150ms ease |
| `transition-default` | 250ms ease |
| `transition-slow` | 400ms ease |

---

## Webflow Variable Groups

When pushing to Webflow, organize variables into these groups:

1. **Colors** — all color tokens
2. **Typography** — font families, sizes, weights, line heights
3. **Spacing** — spacing scale + section padding
4. **Effects** — border radius, transitions (if configured)

---

## Class Naming Reference

All classes follow this pattern: `[category]-[modifier]`

Examples:
- `heading-1`, `heading-2`, `heading-3`, `heading-4`
- `text-large`, `text-base`, `text-small`, `text-muted`, `text-inverse`
- `btn-primary`, `btn-secondary`, `btn-sm`, `btn-lg`
- `bg-primary`, `bg-subtle`, `bg-dark`
- `section-padding-sm`, `section-padding-md`, `section-padding-lg`
- `container`

Never name classes by their visual value (e.g. `text-blue`, `padding-48`).
Always name by role or intent.
