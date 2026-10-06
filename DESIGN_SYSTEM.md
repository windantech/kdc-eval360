# KDC Impact360 — Design System

Carried over from the FPC demonstration and Eval360. The *system* transfers; the *identity* is
provisional until KDC's brand is known.

## One line

**One shell, tokens for everything, three typefaces by role.** A screen supplies content and nothing
else — no `<head>`, no fonts, no colour literals.

## Colour — tokens, never literals

Declared once in `:root` at the top of `kdc_eval360_demo.html`.

| Token | Value | Role |
|---|---|---|
| `--bg` / `--card` / `--muted` | `#f3f5f7` / `#fff` / `#e8ecf0` | Ground, raised surface, recessed fill |
| `--ink` / `--ink-soft` / `--ink-mute` | `#0f1c2a` / `#384858` / `#677686` | Text, secondary, labels |
| `--line` / `--line-soft` | `#d3dae2` / `#e4e9ee` | Borders, internal dividers |
| `--brand` / `--brand-deep` / `--brand-soft` | `#0e5a4a` / `#08362d` / `#e1efeb` | **Primary** (provisional deep green) — buttons, links, sidebar |
| `--accent` / `--accent-soft` | `#2f5fb3` / `#e3ebf8` | Emphasis, one thing at a time. Not a status. |
| `--ok` `--warn` `--bad` `--info` (+ `-soft`) | green / amber / red / indigo | **Status only** |

Charts read the same tokens through `chartTheme()`, so recolouring the brand recolours the charts and
the exported reports. Settings → Branding changes them live.

**Semantic colour is reserved.** Red, amber and green mean off track / needs attention / on track,
overdue / due soon / done. Using them decoratively destroys the signal. State is always also carried
by a label or icon, never colour alone.

## Typography

```
Fraunces        headings, page titles, figures that matter
Inter           UI, body, labels, buttons
JetBrains Mono  codes and IDs — IND-COMP-003, CA-001
```

Uppercase labels at 9.5–10.5px, 700 weight, letter-spaced. Columns of numbers use tabular figures.

## Components

`card()` · `pageHead()` · `kpi()` (a button when it drills down) · `table()` (sortable, paged, CSV) ·
`fSelect` / `fSearch` / `fPills` filter bars · `tabs()` · `chip()` / `statusChip()` · `banner()` ·
`progressBar()` / `dualBar()` · `.split-bar` · `.heat` · `.board` · `.chain` (results chain) ·
`.stepper` (workflow) · `.tl` (history) · `evidenceList()` · `demoTag()`.

## Rules

- **Every dashboard number drills down** where there is a list behind it (brief §60).
- **Illustrative figures are labelled** with `demoTag()` where the brief asks.
- **Not everything is a card.** Lift the one thing that needs lifting.
- **Wide content scrolls in its own container** (`.tbl-scroll`); the page never scrolls sideways.
- Must work on a 1366px laptop and collapse cleanly on a phone.
- Dates `5 Oct 2026` in the UI, ISO in exports and file names.

## Provenance (KDC-specific)

- `pubBadge(key)` — green **Public KDC Data**; opens the source. Every value from `PUBLIC` carries one.
- `demoBadge()` — dashed **Illustrative Demo Data**, tooltip: "This record was generated solely to
  demonstrate Eval360 functionality and does not represent actual KDC operational data."
- `.zone.pub` / `.zone.demo` — public and synthetic figures never share a zone.
- The badge is a `span role="button"`, not a button: it sits inside clickable KPI tiles, and nested
  buttons break layout.
