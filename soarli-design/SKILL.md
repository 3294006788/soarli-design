---
name: soarli-design
description: Apply a neutral gray-white, clean, restrained design system to web projects. Use when the user asks to build tool-style web pages, dashboards, documentation sites, blogs, or any functional web UI where they want a "soarli" aesthetic — neutral grays, pure white cards, no color bias, with LXGW WenKai Screen as the primary font. Triggers on requests for UI implementation, frontend styling, component building, or converting mockups to code when this specific minimal, zen-like aesthetic is desired.
---

Apply a neutral gray-white, clean, restrained design system to any frontend project. This system emphasizes minimalism, readability, and a calm reading experience through fully neutral grays, pure white cards, and the characterful LXGW WenKai Screen font. Dual light/dark mode is built in from the start.

## When to Use This System

Use whenever building functional web interfaces — tool pages, dashboards, documentation, blogs, editors — where content clarity and a calm, zen-like atmosphere matter. The system is intentionally restrained: no color bias, no shadows, no animations that draw attention. Pure information design.

## Core Principles

1. **All neutral, no color bias**: Every gray is truly neutral — no warm or cool undertones. Visual interest comes from typography and spacing, not hue.
2. **White card layering**: Page is light gray (`#F5F5F5`), cards are pure white (`#FFFFFF`). Depth is communicated through value contrast alone.
3. **Low contrast, gentle**: Body text is `#525252` (medium gray), never pure black. Headings at `#262626` (near-black) create clear hierarchy without harshness.
4. **Dark mode as first-class citizen**: Dark mode has its own independent color palette — not inverted light mode values. Dark backgrounds use warm-tinged deep grays.
5. **LXGW WenKai font**: The defining typographic choice. A handwritten-style Chinese font that brings warmth and character to an otherwise neutral system.
6. **No emoji**: Never use emoji characters or decorative Unicode symbols anywhere in generated pages. Use SVG icons or plain text instead.

## Design Tokens

Read `references/design-tokens.css` for the complete CSS variable set. The key tokens:

| Token | Light | Dark | Role |
|-------|-------|------|------|
| `--bg-page` | `#F5F5F5` | `#151617` | Page background |
| `--bg-card` | `#FFFFFF` | `#1D1F20` | Card / sidebar surface |
| `--text-heading` | `#262626` | `#D0D0D0` | Headings and titles |
| `--text-body` | `#525252` | `#A0A0A0` | Body text |
| `--text-muted` | `#A3A3A3` | `#696969` | Secondary info, dates, metadata |
| `--text-link` | `#525252` | `#4682B4` | Link color |
| `--border` | `#E5E5E5` | `#333333` | Dividers and card borders |
| `--selection-bg` | `#A3A3A3` | `#3B936F` | Text selection background |
| `--input-bg` | `#F5F5F5` | `#555555` | Input field background |
| `--input-focus` | `#FFFFFF` | `#FFFFFF` | Input focus state |
| `--btn-success-bg` | — | `#257538` | Success button (dark mode) |
| `--strong-color` | — | `rgb(84, 141, 212)` | Bold/strong text (dark mode) |
| `--table-stripe` | — | `rgba(51, 51, 51, 0.5)` | Table alternating rows (dark mode) |
| `--image-brightness` | — | `70%` | Default image brightness (dark mode) |
| `--image-brightness-hover` | — | `80%` | Image hover brightness (dark mode) |

Link hover in light mode: `#262626` (shifts from `#525252`). Input focus border deepens in light mode. Search button in dark mode uses `#AEAEAE`.

## Typography

### Font Stack

| Role | Font |
|------|------|
| Primary | **LXGW WenKai Screen** (霞鹜文楷) |
| Fallback | `-apple-system`, `system-ui`, `sans-serif` |
| Code | `Consolas`, `Monaco`, `"Courier New"`, `monospace` |

Load LXGW WenKai via `@font-face`:

```css
@font-face {
  font-family: 'soarliWORD';
  font-display: swap;
  src: url('your-font-url.woff2') format('truetype');
}
```

The font family name must be `'soarliWORD'` to match the design system. Use `font-display: swap` for performance.

### Type Scale

| Level | Size | Weight | Use |
|-------|------|--------|-----|
| H1 | 24px–30px | 700 | Page title |
| H2 | 18px–22px | 700 | Article / section headings |
| H3 | 16px–18px | 700 | Sidebar / card titles |
| Body | 14px | 400 | Articles, lists, buttons |
| Small | 12px | 400 | Dates, categories, metadata |

### Typesetting

- Body line-height: `1.6` – `1.8`
- Paragraph spacing: `1em` – `1.5em`
- Word breaking: `word-break: normal; word-wrap: break-word;`
- Never use italic for Chinese text — use bold or color for emphasis instead
- Keep font weights restrained: 400 for body, 700 for headings
- Use a single font family across the entire site — no mixing

## Spacing

8px baseline grid:

| Token | Value | Use |
|-------|-------|-----|
| xs | 8px | Compact element spacing |
| sm | 16px | Element spacing, padding |
| md | 24px | Section spacing, card gaps |
| lg | 32px | Main container padding |
| xl | 48px | Large section separation |

Page container: `max-width: 1280px`, horizontally centered.

## Borders & Depth

- **Border radius**: `0.5rem` (8px) for cards, buttons, inputs — consistent across all elements
- **Card borders**: `1px solid var(--border)` — subtle, barely-there definition
- **No box-shadow**: Depth is communicated through background value contrast (gray page → white card), not shadows
- **Dark mode borders**: `#333333` — deep gray, visible but not prominent

## Component Patterns

### Cards

```css
.card {
  background: var(--bg-card);
  color: var(--text-body);
  border: 1px solid var(--border);
  border-radius: 0.5rem;
  /* no box-shadow */
}
```

Cards float on the gray page background through pure white fill. Content cards are auto-height. Editor/preview cards should have a fixed min-height (400–600px).

### Buttons

**Primary:**
```css
.btn-primary {
  background: var(--text-heading);
  color: var(--bg-card);
  border: none;
  border-radius: 0.5rem;
  padding: 0.5rem 1rem;
  font-size: 0.875rem;
  font-weight: 500;
  cursor: pointer;
  transition: opacity 150ms ease;
}
.btn-primary:hover { opacity: 0.85; }
```

**Secondary / Ghost:**
```css
.btn-ghost {
  background: transparent;
  color: var(--text-body);
  border: 1px solid var(--border);
  border-radius: 0.5rem;
  padding: 0.5rem 1rem;
  font-size: 0.875rem;
  cursor: pointer;
  transition: color 150ms ease, border-color 150ms ease;
}
.btn-ghost:hover {
  color: var(--text-heading);
  border-color: var(--text-muted);
}
```

**Dark mode success button:**
```css
.dark .btn-success {
  background: var(--btn-success-bg);  /* #257538 */
  color: #FFFFFF;
}
```

Disabled buttons: `opacity: 0.5; cursor: not-allowed; pointer-events: none;`

### Inputs & Forms

```css
input, textarea, select {
  background: var(--input-bg);       /* #F5F5F5 light / #555555 dark */
  color: var(--text-body);
  border: 1px solid var(--border);
  border-radius: 0.5rem;
  padding: 0.5rem 0.75rem;
  font-size: 0.875rem;
  outline: none;
  transition: background 150ms ease, border-color 150ms ease;
}
input:focus, textarea:focus, select:focus {
  background: var(--input-focus);    /* #FFFFFF in both modes */
  border-color: var(--text-muted);
}
::placeholder { color: var(--text-muted); }
```

In light mode, focused inputs switch from gray to white background with a deeper border. In dark mode, text color shifts from `#C1C6C9` to `#FFFFFF` on focus.

### Navigation

- **Layout**: flex, space-between, align center
- **Background**: `var(--bg-card)` — matches sidebar/card background
- **Height**: 56–64px
- **Links**: `var(--text-body)` color, 14px, hover transitions to `var(--text-heading)`
- **Mobile**: compress spacing, consider hamburger menu

### Sidebar

- **Background**: `var(--bg-card)` — white in light mode, `#1D1F20` in dark
- **Width**: 240–280px
- **Separator**: `1px solid var(--border)`
- **Active item**: `var(--text-heading)` color, bolder weight

### Footer

- **Layout**: flex, space-between, align center
- **Background**: transparent, blending into page
- **Text**: `var(--text-muted)`, 12px
- **Mobile**: flex-col, centered

### Table

Striped rows in dark mode:
```css
.dark table tr:nth-child(even) {
  background: var(--table-stripe);  /* rgba(51, 51, 51, 0.5) */
}
```

### Toggle Switch

Dark mode active state: `#19A9D5` (bright blue).

### Images in Dark Mode

```css
.dark img {
  filter: brightness(var(--image-brightness));  /* 70% */
  transition: filter 150ms ease;
}
.dark img:hover {
  filter: brightness(var(--image-brightness-hover));  /* 80% */
}
```

## Dark Mode

Apply via a `.DarkMode` class on the root element. Key changes from light mode:

- **Background layers swap**: Light gray → warm deep black (`#151617`), white cards → deep gray (`#1D1F20`)
- **Text inverts gently**: Body becomes `#A0A0A0`, headings become `#D0D0D0` — lower contrast than light mode
- **Links switch to steel blue** (`#4682B4`) instead of gray — color is the affordance in an otherwise monochrome environment
- **Selection becomes teal-green** (`#3B936F`) instead of gray — a subtle but distinctive touch
- **Images are dimmed** to 70% brightness to reduce eye strain
- **Bold text uses WeChat-style blue** (`rgb(84, 141, 212)`) — a deliberate warm accent

### Theme Toggle Icon

| Mode | Icon Color | Notes |
|------|-----------|-------|
| Light mode toggle | `#777777` | Gray sun/moon icon |
| Dark mode toggle | `#FFC107` | Amber gold — a warm anchor in dark space |

Use inline SVG icons for the toggle. The amber gold on dark mode is the system's only deliberate color accent — it should feel like a small warm light in the dark.

## Animation Rules

- Duration: always **150ms**
- Properties: `color`, `opacity`, `background`, `border-color`, `filter` — never transform or positional changes
- No entrance animations, no page load effects
- The page is static; interaction feedback is subtle and instant

## Responsive Behavior

| Breakpoint | Layout |
|------------|--------|
| Mobile (< 1024px) | Single column, stack vertically |
| Desktop (≥ 1024px) | Multi-column grid or side-by-side panels |

- Main container stays centered at all breakpoints
- Mobile: reduce font sizes by 1–2px, collapse sidebar, stack cards
- Touch targets: minimum 44px on mobile

## Icons

Use simple line-style SVG icons (Lucide or custom). Size 16–20px. Color matches surrounding text via `currentColor`. Keep icons minimal — the font is the star of this system.

## Implementation Order

When applying this system to a project:

1. Copy the CSS variable block from `references/design-tokens.css` into the project
2. Load LXGW WenKai Screen via `@font-face` with `font-family: 'soarliWORD'`
3. Set the font stack: `'soarliWORD', -apple-system, system-ui, sans-serif` on `body`
4. Apply `--bg-page` to the page, `--bg-card` to cards, sidebars, and nav
5. Use `border` for element separation — never `box-shadow`
6. Set body text to 14px, line-height 1.6–1.8
7. Configure dark mode by toggling `.DarkMode` class — all variables swap automatically
8. Add the amber-gold theme toggle icon for dark mode

## Design Keywords

> **Gray-white base · Pure white cards · Neutral text · Minimal layering · Independent dark palette · LXGW WenKai font**
