---
name: axiom-brand-ui
description: Axiom's visual system (colors, type, shape, logo, UI copy rules) for any Axiom-branded interface, including the Axiom CRM fork of Atomic CRM. Load before theming, building or reviewing any Axiom UI screen, component, email template or page. Not for client-branded assets — clients carry their own brand.
---

# Axiom brand UI

Source of truth: the live site **https://deployaxiom.com** (`/assets/site.css`, `/assets/favicon.svg`), captured 2026-09-27. If the site and this file disagree, the site wins; update this file.

Scope guard: this is the **Axiom lane only**. Never apply it to a client deploy. Client deploys get their own theme file, never these tokens.

## Files
- `theme.css` holds the shadcn/Tailwind v4 tokens. Drop it into the app's global CSS in place of the default shadcn `:root` / `.dark` blocks.
- `assets/axiom-mark.svg` is the "A" mark: lime on an ink square. Use it for the favicon, app icon and collapsed-sidebar logo.

## Palette
| Token | Hex | Use |
|---|---|---|
| paper | `#ebe7dc` | App background |
| ink | `#101310` | Text, strong borders, input borders |
| muted | `#526056` | Secondary text (5.4:1 on paper) |
| field | `#151915` | Sidebar, dark bands, dark mode base |
| sage | `#dfe5d7` | Soft panels, hover, secondary buttons |
| line | `#a8aea3` | Dividers only |
| signal | `#bdff43` | Primary fill, active state, the one thing to click |
| focus | `#4d8000` | Focus ring |

Hard rules, based on the contrast checks:
1. **Signal is a fill, never text on paper** (1.03:1). Text on signal is always ink.
2. **Line is never an input or control border** (1.8:1). Inputs use an ink border, as the site does.
3. Use one signal element per view region. It marks the next action, so don't use it as decoration.
4. Destructive red `#b3261e` is derived and not on the site. Keep it for delete and error only.

## Shape and type
- **Radius 0.** Square everywhere: buttons, cards, inputs, badges, avatars included.
- Borders are 1px solid. Build grids with 1px gaps over a `line` background (the site's `.contract` / `.lanes` pattern).
- The font is the system sans stack. No webfont, which keeps it fast.
- Wordmark: `DEPLOY AXIOM`, weight 850, tracking `.14em`, uppercase (`.axiom-wordmark`).
- Headings: heavy weight, tracking `-.04em`, line-height about .95 (`.axiom-heading`).
- Eyebrow labels: `.72rem`, weight 800, tracking `.12em`, uppercase, muted (`.axiom-eyebrow`).
- Buttons: min-height 46px, weight 800, 1px ink border. Primary is a signal fill; quiet is transparent.
- Focus ring: 3px solid ring, 3px offset. Honor `prefers-reduced-motion`.

## Layout
- Max content width 1180px, side padding `clamp(1.2rem, 4vw, 3.5rem)`.
- Sidebar uses the dark field band: paper text, signal fill for the active item.
- Layouts must collapse to a single column under 720px, and nav collapses under 390px.

## Product language in the UI
The site defines Axiom's operating model. Reuse its words in CRM labels so the product and the pitch match:
- Pipeline and job stages: **Catch → Gather → Prepare → You decide → Log**.
- Outcomes: **Good fit · Not a fit · Waiting on you · Handed off**.
- Permission ladder: **Read · Sort · Draft · Line up · Act\* · Stop**. \*Acting needs the owner's yes. A draft never counts as approval.
- Copy is plain, short and second person ("You decide", "Waiting on you"). For longer copy, load `pkfit-writer-brief` for Axiom voice.

## Replace upstream branding
When theming Atomic CRM, remove every "Atomic CRM" and Marmelab mark from the UI, `index.html` title and meta, manifest, favicon, email templates and the login screen. Keep the MIT `LICENSE` and copyright notice in the repo; that's required and never shown in the UI.

## Review checklist (score every Axiom UI PR)
- [ ] No upstream name or logo is visible anywhere (`grep -ri "atomic" src/` has no UI hits).
- [ ] Every surface uses tokens only, with no raw hex in components.
- [ ] Radius is 0 everywhere.
- [ ] No signal text on paper, and no line-colored control borders.
- [ ] Focus ring is visible on every interactive element.
- [ ] Layout works at 390px, 720px and 1180px+.
- [ ] Dark mode is checked.
- [ ] Stage and outcome labels match the product language above.
