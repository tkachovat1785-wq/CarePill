# CarePill — Design System Specification

Mobile artboard: **428 × 926** px (iPhone-style). Font: **Inter** (400/500/600/700/800).
All values below are exact and authoritative.

---

## 1. Color

### Brand / primary
| Token | Hex | Usage |
|---|---|---|
| `navy` (primary) | `#04277D` | Primary buttons, headings, key icons, skateboard deck, nav accent |
| `navy-soft` | `#5C6BB0` | Deck highlight, muted affordance text ("Tap to change") |
| `navy-ink` | `#2C3E73` | Illustration trousers / deep navy shading |
| `teal` (secondary / success) | `#0D5C4D` | Success check fill, woman's sweater, secondary brand |
| `teal-deep` | `#0A4A3E` / `#0A3A30` | Illustration shading |

### Surfaces & backgrounds
| Token | Hex | Usage |
|---|---|---|
| `bg-app` | `#FAF9F7` | App background (most screens) |
| `surface` | `#FFFFFF` | Cards, inputs, time-picker sheet |
| `mint` | `#E3F2EE` | Splash bg, **bottom-sheet popups** (reminder, snooze, snoozed, call-confirm, action-complete), icon accents |
| `mint-2` | `#E6F0EC` | Icon chips / medication icon container |
| `mint-3` | `#F1F5F3` | Timeline icon tiles |
| `lavender` | `#E0E7FF` | "Anna" assistant surfaces, accent blobs, collar trim, selected schedule chip |
| `lavender-2` | `#E0E8FF` | Contact avatar background |
| `lavender-border` | `#C7D0F5` | Border on lavender surfaces |

### Text
| Token | Hex | Usage |
|---|---|---|
| `text-primary` | `#1E2E29` | Body / primary content text |
| `text-heading` | `#04277D` | Headings, labels on brand |
| `text-secondary` | `#4A5955` | Secondary text & captions (default) |
| `text-secondary-hc` | `#2C3531` | Secondary text in **high-contrast** mode |
| `text-popup-body` | `#3A6359` | Body copy inside mint bottom-sheet popups |
| `text-muted-indigo` | `#5C6BB0` | "Tap to change", "Skip for now" |

### AM/PM (secondary time-format control) — deliberately softer than primary chips
| State | bg | text | border |
|---|---|---|---|
| selected | `#EAEEF7` | `#3E4A66` | `2px #AEB9D6` |
| unselected | `#F5F7FB` | `#707B95` | `1.5px #DCE4E2` |
| check icon | — | `#5C6BB0` | — |

### Destructive
| Token | Hex | Usage |
|---|---|---|
| `danger` | `#BA1A1A` | Delete buttons/labels, error text, missed-dose marker |
| `danger-surface` | `#FBE9E9` | Confirm-dialog destructive icon circle |
| `call-end` | `#E5453A` | End-call button |

### Emergency
| Token | Hex | Usage |
|---|---|---|
| `emergency` | `#E07B4F` (prop `emergencyColor`) | Call buttons / emergency accent |

### Borders & dividers
| Token | Hex | Usage |
|---|---|---|
| `border` | `#DCE4E2` | Default input/card outline |
| `border-2` | `#E8ECEA` | Card outline (softer) |
| `border-3` | `#E2E7E5` | Tiles / day chips |
| `divider` | `#EEF1EF` | Hairline dividers, segmented bg |

### Status / chips
| Token | Hex | Usage |
|---|---|---|
| taken chip | bg `#E6F4EF`, text `#0D5C4D` | "Taken" status |
| missed marker | `#BA1A1A` | missed dose |
| grey neutral | `#9AA8C8` / `#9AA8A3` | skateboard hardware, chevrons |
| hair silver | `#C9D2E0` | illustration hair |
| skin | `#D6A07C` (shade `#C2895F`) | illustration skin |

> **Rule:** navy + teal are the only dominant colors. Mint & lavender are accents. Do not introduce new
> dominant hues. Cheek blush (`#E8A78F`, ~50% opacity) is decorative-only.

---

## 2. Typography

Family: **Inter**, `-apple-system, sans-serif` fallback.

| Role | Size | Weight | Letter-spacing | Color | Notes |
|---|---|---|---|---|---|
| Display heading | 32px | 700 | -0.5px | `#04277D` | Welcome title |
| Screen title (h1) | 28–30px | 700 | -0.4px | `#04277D` | Step screens |
| Popup title (h2) | 25px | 700/800 | -0.3px | `#04277D` | Bottom-sheet & dialog titles |
| Detail name | 30px | 800 | -0.4px | `#04277D` | Med/contact detail header |
| Big time value | 54–64px | 700/800 | -1 to -2px | `#04277D` | Time cards & picker; `font-variant-numeric: tabular-nums` |
| Body | 18–20px | 500/600 | — | `#1E2E29` / `#4A5955` | `text-wrap: pretty` for paragraphs |
| Popup body | 19px | 600 | — | `#3A6359` | line-height 1.5 |
| Button label | 19–22px | 700 | — | varies | |
| Field label | 16–17px | 600 | — | `#04277D` | |
| Caption / overline | 13–15px | 600/700 | 0.4–0.6px, `UPPERCASE` | `#4A5955` / `#04277D` | section + status labels |
| Min size | **14px** | — | — | — | never smaller (older-adult legibility) |

### Text-size accessibility scale
Multipliers `[1, 1.13, 1.27, 1.4]` (4 steps), applied to whole screens/overlays. Prototype uses CSS
`zoom`; in a real app use a font-scale context / Dynamic Type and ensure layouts reflow without clipping.

---

## 3. Spacing & layout

- **Horizontal screen padding:** `28px` (forms/content), `24px` (history sheet).
- **Top padding:** `62px` for screens with a back-button row; `80px` for success screens (back button
  removed — keep balanced top breathing room).
- **Footer (CTA) padding:** `14px 28px 30px`; stacked CTAs use `gap: 8–12px`.
- **Common gaps:** 6 / 8 / 10 / 12 / 14 / 18 / 20 / 22 px (flex/grid `gap` — not margins).
- **Bottom-sheet padding:** `30px 28px 36px`.
- **Dialog (centered) padding:** `30px 26px 24px`, `max-width: 360px`.
- **Card padding:** `16–20px`.
- Layout uses **flex/grid with `gap`** throughout. Day pickers use `grid-template-columns: repeat(3,1fr)`.

---

## 4. Border radius
| Element | Radius |
|---|---|
| Primary / large buttons | 18px |
| Secondary buttons, inputs | 16px |
| Cards | 18–22px |
| Icon chips | 14px |
| Bottom sheets (top corners) | 34px |
| Centered dialog | 26px |
| Pills / chips / avatars | 999px / 50% |
| Time-picker stepper buttons | 18px |
| AM/PM buttons | 14px |

---

## 5. Shadows
| Use | Value |
|---|---|
| Primary button | `0 12px 26px rgba(4,39,125,.22)` |
| Destructive button | `0 10px 24px rgba(186,26,26,.25)` |
| Card (soft) | `0 2px 8px rgba(13,92,77,.04)` |
| Card (default) | `0 4px 14px rgba(13,92,77,.05)` |
| Card (raised) | `0 6px 18px rgba(13,92,77,.06)` |
| Input | `0 1px 2px rgba(0,0,0,.04)` |
| Bottom sheet | `0 -10px 40px rgba(8,30,24,.x)` |
| Centered dialog | `0 24px 60px rgba(8,30,24,.3)` |
| Overlay scrim | `rgba(8,30,24,.5)` (sheets) / `.55` (dialogs) |

---

## 6. Motion
Keyframes (durations & easings are exact):

| Name | Definition | Use |
|---|---|---|
| `cpFade` | opacity 0→1, `.2–.25s ease` | overlay scrims |
| `cpUp` | translateY(100%)→0, `.35s cubic-bezier(.2,.8,.2,1)` | bottom sheets |
| `cpPop` | scale .7→1.06→1, `.3–.45s ease` | dialogs, success checks |
| `cpPulse` | scale 1→1.9 + fade, `2.2–2.8s` infinite | Anna mic halo, splash |
| `cpRing` | scale .9→1.6 + fade, `1.8s` infinite | call ripple |
| `cpGlide` | translateY 0→-6→0, `3.8s ease-in-out` infinite | Welcome riders bob |
| `cpRoll` | rotate 0→360°, `3.2s linear` infinite | Welcome skateboard wheels |
| `cpSway` | rotate 0→7°→0, `~3.4s ease-in-out` infinite | Welcome hair sway |
| `cpDrift` | translateX + fade, `2.7s ease-in-out` infinite (staggered) | Welcome speed lines |
| Screen track | `transform .42s cubic-bezier(.4,0,.2,1)` | onboarding horizontal slide |

**Reduced motion:** `@media (prefers-reduced-motion: reduce) { .cp-ride, .cp-wheel { animation: none !important } }`.
Wheels/hair use `transform-box: fill-box; transform-origin: center` (SVG).

---

## 7. Component recipes

### Primary button
`height: 90px` (CTA) or `80px` (in-overlay); `bg #04277D`; text `#fff` 21–22px/700; radius 18px;
`box-shadow: 0 12px 26px rgba(4,39,125,.22)`; centered flex, `gap:12px` with optional trailing chevron.

### Secondary (outline) button
`height: 66–80px`; `bg #fff`; `2px solid #04277D`; text `#04277D` 18–20px/700; radius 16px.

### Tertiary / ghost button
Transparent bg, no border; text `#5C6BB0` 700 (e.g. "Skip for now") or `#BA1A1A` 700 (Delete actions);
`height: 60–66px`.

### Destructive button (in confirm dialog)
`bg #BA1A1A`; text `#fff`; `height: 78px`; radius 18px; `box-shadow 0 10px 24px rgba(186,26,26,.25)`;
trash icon leading.

### Input field
`height: 72–74px`; `bg #fff`; `1.5px solid #DCE4E2` (error → `#BA1A1A`); radius 16px;
padding `16–22px`; text 19px/500 `#1E2E29`; `box-shadow 0 1px 2px rgba(0,0,0,.04)`; outline none.
Error row: 18px circle-alert icon + `#BA1A1A` 16px/600 message, `cpFade` in.

### Card (list item)
`bg #fff`; `1.5px solid #E8ECEA`; radius 18–22px; padding 16–20px; raised shadow; left icon chip
(48–56px, `bg #E6F0EC`/`#E0E8FF`, radius 14px or 50%) + text column + trailing chevron `#9AA8A3`.

### Medication icon (centered capsule) — **critical**
24×24 viewBox. Pill must be perfectly centered & rotated about the **viewBox center**:
```svg
<rect x="5.5" y="9" width="13" height="6" rx="3" transform="rotate(-45 12 12)" fill="#04277D"/>
```
Never pivot rotation about a corner. The container is flex `align-items:center; justify-content:center`.

### Bottom-sheet popup (the canonical confirmation popup)
Scrim `rgba(8,30,24,.5)` + `cpFade`; sheet anchored bottom: `bg #E3F2EE`; `border-radius 34px 34px 0 0`;
**padding `30px 28px 36px`**; `cpUp` enter; column, centered, `gap:12px`. Contents: 84px circle
(`rgba(4,39,125,.10)`) wrapping 60px `#04277D` circle + white icon → h2 title 25px/700 `#04277D` →
body 19px/600 `#3A6359` → 80px primary "Close"/action button.
**All "completed-action" confirmations (Medication Deleted, Contact Deleted, Medication Saved, Contact
Saved, Reminder Snoozed) share these exact dimensions.**

### Centered confirm dialog (destructive)
Scrim `rgba(8,30,24,.55)`; centered card `max-width 360px`; `bg #fff`; radius 26px; padding
`30px 26px 24px`; `cpPop`. 72px `#FBE9E9` circle + `#BA1A1A` trash icon → h2 25px → body 18px `#4A5955`
→ stacked `#BA1A1A` Delete (78px) + outline Cancel (70px).

### Time picker (single shared control)
White bottom sheet (radius 34px top, padding `26px 28px 32px`). Grab-handle. Header: title +
12h/24h toggle pill (`bg #E0E7FF`, `1.5px #C7D0F5`, clock icon). Two stepper columns (hour, minute) —
each `88×64px` up/down buttons (`bg #FAF9F7`, `1.5px #DCE4E2`, chevron) around a `64px/800` value with
`tabular-nums`; ":" separator. AM/PM segmented control (see §1, hidden in 24h mode, check when selected,
`aria-pressed`). 80px primary "Save Time" + 64px outline "Cancel". Minute step = 5.

### Schedule / day chips (primary selection — keep prominent)
Selected: `bg #E0E7FF`, text `#04277D`, `2px #04277D` border, leading check. Unselected: `bg #fff`,
`1.5px #DCE4E2`. Min height 62px.

### Bottom nav (app phase)
Tab buttons, equal flex; active tab pill `bg` accent; pill / phone / profile icons; label below.

---

## 8. Accessibility checklist
- Hit targets ≥ 44px; primary CTAs 80–90px.
- Body ≥ 18px, never below 14px; supports the 4-step font scale to 1.4×.
- High-contrast mode darkens secondary text to `#2C3531`.
- Selection states never rely on color alone — also use **border weight changes + check icons +
  `aria-pressed`** (see AM/PM and chips).
- Interactive non-button elements (tappable time cards) use `role="button"`, `tabindex="0"`, `aria-label`.
- Decorative motion disabled under `prefers-reduced-motion`.
- Illustration has `role="img"` + descriptive `aria-label`.
