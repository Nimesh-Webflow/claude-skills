# Webflow Push

Instructions for pushing design system tokens and classes to Webflow via MCP.
This file is read when executing Step 10 (Starter) or Step 4 (Developer) — after
the user has confirmed the preview summary.

---

## Pre-Push Checklist

Before calling any Webflow MCP tool:

1. Confirm Site ID is stored from the entry point
2. Confirm the user has reviewed and approved the preview summary
3. Check if existing variables or styles were flagged — if yes, warn before overwriting
4. Push in the correct order — variables must exist before classes that reference them

---

## Push Order

```
1. Color variables
2. Typography variables (font families, sizes, weights, line heights)
3. Spacing variables
4. Effect variables (border radius, transitions — if configured)
5. Global resets (custom code injection)
6. Typography classes
7. Layout classes (container, section-padding)
8. Button classes
9. Custom variables (if any)
10. Custom classes (if any)
```

Never push classes before their referenced variables exist.

---

## Webflow MCP Tool Usage

Use the Webflow MCP tools available in the session. Common operations:

**To list available sites:**
Use the Webflow MCP list sites tool to confirm the Site ID is valid.

**To create a variable:**
Use the Webflow MCP variable tool with:
- Variable name (kebab-case, from token schema)
- Variable type (color, size, number, font-family)
- Variable value
- Variable group (Colors / Typography / Spacing / Effects)

**To create a class:**
Use the Webflow MCP style tool with:
- Class name (kebab-case)
- CSS properties as key-value pairs
- Reference variable names where applicable (not raw values)

**To inject global resets:**
Use the Webflow MCP custom code tool to add reset CSS to the site's head custom code.

---

## Variable Type Mapping

| Token Category | Webflow Variable Type |
|---|---|
| color-* | Color |
| font-size-* | Size |
| font-weight-* | Number |
| line-height-* | Number |
| font-primary, font-display, font-mono | Font Family |
| spacing-* | Size |
| radius-* | Size |
| transition-* | String (not a native Webflow variable type — use as custom property) |

---

## Error Handling

If a push fails for any variable or class:

1. Note the failure — do not stop the entire push
2. Continue with remaining items
3. At the end, report failures separately with suggested fixes

Common failures:
- **Duplicate name** — variable or class already exists with that name
  → Inform user, ask whether to skip or overwrite
- **Invalid value format** — Webflow rejected the value
  → Check format and retry with corrected value
- **MCP auth error** — Webflow session expired
  → Ask user to reconnect Webflow MCP and retry

---

## Global Resets — Custom Code Block

Inject this into Site Settings → Custom Code → Head Code:

```css
<style>
/* Design System — Global Resets */
*, *::before, *::after { box-sizing: border-box; }
body { margin: 0; }
img, video { max-width: 100%; display: block; }
a { text-decoration: none; color: inherit; }
button { cursor: pointer; border: none; background: none; }
ul, ol { list-style: none; margin: 0; padding: 0; }
h1, h2, h3, h4, h5, h6 { margin: 0; }
p { margin: 0; }
</style>
```

Note: If the user already has custom code in the head, append rather than replace.
Flag this to the user before injecting.

---

## Post-Push Verification

After all pushes complete, prompt the user to verify:

> **Verify in Webflow Designer:**
>
> 1. Open Variables panel — you should see groups: Colors, Typography, Spacing
> 2. Open Style panel — search for `heading-1`, `btn-primary`, `container` to confirm classes exist
> 3. Apply `heading-1` to a text element and check it renders correctly
> 4. Apply `section-padding-md` to a section and confirm vertical spacing
>
> If anything looks off, share a screenshot and I'll diagnose.
