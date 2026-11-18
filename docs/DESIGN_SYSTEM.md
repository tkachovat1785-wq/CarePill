# CarePill — Design System Specification

**Version:** 2026-11-18, rev. 2. Rebuilt from the app in this repository (`index.html` at commit `55aede1`), then updated for the UI fixes in §10a (typography, Medication Details buttons, interaction states). This replaces the earlier handoff spec.

**Single source of truth:** where this document and `index.html` disagree, `index.html` wins.

## How the values were obtained

Every value has a source marker:

| Marker | Meaning |
|---|---|
| **R** | **Rendered.** Measured with `getComputedStyle` / `getBoundingClientRect` in Chromium at 428×926, default props, across 41 screen states (onboarding, Pillbox, overlays, Profile, EN/DE/RU). |
| **S** | **Source.** Read directly from the inline CSS / logic in `index.html`. Used where rendering cannot show the exact value (for example 1.5px borders, which Chromium reports as `1px`) or for states that were not rendered. |
| **A** | **Assumption.** Not verified. Stated as guidance only. |

"Default props" means the values the app ships with:

- `highContrast: true`
- `showAnna: true`
- `navAccent: #04277D`
- `emergencyColor: #AF5F3E`

Note that the JavaScript fallbacks differ: `highContrast ?? false` and `emergencyColor ?? '#E07B4F'`. These apply only if the runtime passes no props. **S**

Known inconsistencies in the app itself are listed in [§10](#10-known-inconsistencies-in-the-app-not-fixed). They are documented here, not fixed.

---

## 1. Artboard and layout

| Item | Value | Src |
|---|---|---|
| Artboard | 428 × 926 px phone frame, radius 46px, `overflow:hidden` | R |
| Page around the frame | Frame centred; page height 1034px (54px above and below) | R |
| Responsive behaviour | **None.** The frame is always 428px wide. Below ~442px viewport width it is clipped left and right: at 390px, 19px per side; at 375px, 26px; at 320px, 54px. No scaling, no breakpoints, no `@media` width queries. | R |
| Status bar | Static "9:41", notch 122×32 radius 18 | R |
| Screen side padding | 28px (onboarding screens, Pillbox, Profile, overlays) | R/S |
| Top padding (screens with back button) | 62px; detail screens 70px | S |
| Onboarding track | Horizontal flex row. `translateX(-obStep × 428px)`, `transition: transform .42s cubic-bezier(.4,0,.2,1)`. 16 screens; the container is declared 6420px wide (15 × 428). | R/S |
| Scroll areas | `.cp-scroll` hides scrollbars | S |

---

## 2. Color

### 2.1 Brand

| Token | Hex | Use | Src |
|---|---|---|---|
| `navy` | `#04277D` | Primary buttons, headings, labels, icons, selected borders. Most used colour (417 occurrences). | R |
| `teal` | `#0D5C4D` | Success circles, "Taken" chip text, "Emergency contact" status text | R |
| `navy-soft` | `#5C6BB0` | "Skip for now", "Tap to change", "Tap to hear it again" | R |
| `emergency` | `#AF5F3E` (default prop) | Call buttons, "Resolve with Anna" outline, missed labels. Options: `#AF5F3E`, `#BA1A1A`, `#E07B4F`. | R/S |
| `call-end` | `#E5453A` | End-call button, shadow `0 12px 30px rgba(229,69,58,.4)` | R |
| `danger` | `#BA1A1A` | Destructive buttons and labels, input error border and text | R |
| `danger-surface` | `#FBE9E9` | Delete-dialog icon circle | R |

### 2.2 Surfaces

| Token | Hex | Use | Src |
|---|---|---|---|
| `bg-app` | `#FAF9F7` | Screens, Medication Details, contact picker sheet, stepper buttons | R |
| `surface` | `#FFFFFF` | Cards, inputs, chips, dialogs, time-picker sheet, history sheet | R |
| `mint` | `#E3F2EE` | Splash, Sign Up / Log In screen, **full-screen** reminder / missed / taken / snooze modals, call-confirm and action-complete bottom sheets, toasts | R |
| `mint-chip` | `#E6F0EC` | Icon chips (name screen 72×72 r20, med-added 52×52 r14, detail 78×78 r22) | R |
| `mint-tile` | `#F1F5F3` | Schedule time tile 54×54 r15 | R |
| `lavender` | `#E0E7FF` | Anna sheet, selected time-of-day chip, selected intake tile, 12-hour toggle | R |
| `lavender-voice` | `#E7ECFF` | "Voice reminder playing" button in reminder modal | R |
| `lavender-avatar` | `#E0E8FF` | Contact / profile avatars | R |
| `lavender-border` | `#C7D0F5` | Borders on lavender surfaces | R/S |
| `close-chip` | `#EEF1EF` + border `#C9D5D1` | Close button in full-screen modals (44×44 r13) | R |
| `info-panel` | `rgba(255,255,255,.55)` + border `#CFE0DA` | "How to take it" panel in reminder modals | R |
| `selected-tint` | `rgba(4,39,125,.05)` + 2px `#04277D` | Selected option tile (language, frequency) | R |
| `nav-active` | `rgba(4,39,125,.10)` | Active bottom-nav tab | R |

### 2.3 Text

| Token | Hex | Use | Src |
|---|---|---|---|
| `text-primary` | `#1E2E29` | Input text, option labels, names, date heading | R |
| `text-heading` | `#04277D` | Titles, field labels, button labels | R |
| `text-secondary` | `#2C3531` | Body paragraphs and captions. Rendered with `highContrast: true` (the default). | R |
| `text-secondary-low` | `#4A5955` | Same role when `highContrast` is false. Not rendered with default props. | S |
| `text-popup` | `#3A6359` | Body text on mint (auth tagline, snooze text, call-confirm text, "Connecting") | R |
| `text-modal-detail` | `#234B43` | Dose / time line in reminder modal | R |
| `text-modal-label` | `#2F5249` | "HOW TO TAKE IT" overline | R |
| `text-anna` | `#243A6E` | Anna sheet hint text, Anna toast text | R |
| `text-on-navy-muted` | `#A9D7CC` | Secondary text on the navy "Next dose" card | R |
| `placeholder` | `#BFC9C4` | Select-field placeholder ("Select relationship") | R |
| `icon-muted` | `#9AA8A3` | Inactive nav labels and icons, chevrons | R |

### 2.4 Borders

| Token | Value | Use | Src |
|---|---|---|---|
| `border` | 1.5px `#DCE4E2` | Inputs, select, back button, chips, stepper buttons (45 uses) | S |
| `border-strong` | 2px `#04277D` | Outline buttons, selected tiles and chips (22 uses) | S |
| `border-card` | 1.5px `#E8ECEA` | Cards (detail rows, contact card, schedule card) | S |
| `border-tile` | 1.5px `#E2E7E5` | Profile rows, day-navigation pills; 2px on intake tiles | S |
| `border-option` | 2px `#DCE4E2` | Unselected option tiles (language, frequency) | R/S |
| `divider` | 1px `#F0F2F0` (dropdown rows), 1px `#EEF1EF` (list rows) | S |
| `nav-border` | 1.5px `#EAEEEC` | Bottom-nav container | S |

### 2.5 AM/PM control (intentionally softer than chips)

| State | bg | text | border | Src |
|---|---|---|---|---|
| Selected | `#EAEEF7` | `#3E4A66` 20px/600 | 2px `#AEB9D6` | R |
| Unselected | `#F5F7FB` | `#707B95` 20px/600 | 1.5px `#DCE4E2` | R/S |

### 2.6 Scrims

| Use | Value | Src |
|---|---|---|
| Bottom sheets (call confirm, time picker, history, contact picker, action complete) | `rgba(8,30,24,.5)` | S |
| Centered dialogs (delete, log out) | `rgba(8,30,24,.55)` | S |
| Anna sheet | `rgba(8,16,40,.5)` + `backdrop-filter: blur(3px)` | S |

---

## 3. Typography

**Family:** `Inter, sans-serif`, loaded from Google Fonts at weights 400/500/600/700/800. **R**

All text renders in Inter. 42 buttons set no `font-family` inline; they now inherit Inter through `button:not([style*="font-family"]){font-family:inherit;line-height:1.15}`. The line height 1.15 keeps the line boxes of the former Arial fallback, so no button or container changed size (verified: 0 container size changes across 39 states). **R/S**

| Role | Size / weight | Letter-spacing | Line height | Colour | Example | Src |
|---|---|---|---|---|---|---|
| Time value (picker) | 64 / 800 | -2px | 64px | navy | Time picker digits | R |
| Time value (cards) | 60 / 700 | -1.5px | 60px | navy | Reminder Time cards | R |
| Brand title | 40 / 800 | -1px | normal | navy | "CarePill" (auth) | R |
| Meet Anna title | 38 / 800 | -0.5px | 1.2 | navy | "Meet Anna" | R |
| Modal title | 34 / 800 | -0.5px | 1.2 | navy | Reminder med name, "Reminder Snoozed" | R |
| Display | 32 / 700 | -0.5px | normal | navy | "Welcome, Maria!", "Taken!" | R |
| Screen title, large | 30 / 700 | -0.4px | normal | navy | "Choose your language", "What's your name?" | R |
| Detail name | 30 / 800 | -0.4px | normal | navy | Medication / contact details | R |
| Screen title | 28 / 700 | -0.4px | normal | navy | "Emergency Contact", medication steps | R |
| Success title | 26 / 700 | -0.4px | normal | navy | "Medication Added", "Edit Medication" | R |
| Date heading | 26 / 700 | -0.2px | normal | `#1E2E29` | "Thursday, June 18" | R |
| Dialog title | 25 / 800 | -0.3px | normal | navy | "Delete this medication?", "Log out?" | R |
| Sheet title | 25 / 700 | normal | normal | navy | "Do you want to call?" | R |
| Anna sheet text | 24 / 700 | normal | 34.8px | navy | "How can I help today?" | R |
| Primary button label | 22 / 700 | normal | normal | white | 90px CTAs | R |
| Modal button label | 23 / 700 | normal | normal | white | "Take Med", "Snooze 15 minutes" | R |
| Secondary button label | 18–21 / 700 | normal | normal | navy | Outline buttons | R |
| Option label | 20 / 600 | normal | 1.15 | `#1E2E29` | Frequency and language tiles | R |
| Body large | 20 / 400 | normal | 30px | `#2C3531` | Welcome / Taken paragraph | R |
| Body | 19 / 400 | normal | 1.45 (27.55px) | `#2C3531` | Screen intros | R |
| Body small | 18 / 400 | normal | 1.45–1.5 | `#2C3531` | Emergency intro, Meet Anna hint | R |
| Input text | 20 / 500 (forms), 21 / 600 (name, medication), 19 / 500 (profile) | normal | — | `#1E2E29` | Inputs | R |
| Field label | 17 / 600 | normal | normal | navy | "First Name", "Full Name" | R |
| Error text | 16 / 600 | normal | normal | `#BA1A1A` | Field errors | R |
| Overline | 15 / 600–700 | 0.4–0.6px | normal | `#2C3531` / navy, UPPERCASE | "STEP 1 OF 2 · SAFETY", "NEXT DOSE" | R |
| Detail overline | 14 / 700 | 0.4–0.5px | normal | `#2C3531`, UPPERCASE | Detail rows, "HOUR" / "MIN" | R |
| Status chip | 14 / 700 | normal | normal | `#AF5F3E` | "Missed" | R |
| Nav label | 13 / 700 | normal | 1.15 | navy active, `#9AA8A3` inactive | Bottom nav | R |
| Small caption | 13 / 600, 12 / 700 | 0.4px / normal | normal | `#2C3531` | Contact relationship (13), schedule "AM" (12) | R |

**Minimum size.** The earlier spec said "nothing below 14px". The app has three text styles below that: 13px nav labels, 13px relationship overline, and the 12px AM/PM inside the schedule time tile. **R**

**Text-size scale.** `[1, 1.13, 1.27, 1.4]`, applied with CSS `zoom` on screens and overlays (`feedZoom`). At the largest step, rendered elements carry `zoom: 1.4`. **R/S**

---

## 4. Spacing

| Item | Value | Src |
|---|---|---|
| Screen horizontal padding | 28px | R/S |
| Content width at 428px | 372px (428 − 2×28) for full-width buttons, inputs, cards | R |
| Footer CTA area | Primary button 372×90 at the bottom; stacked secondary actions below or above | R |
| Full-screen modal padding | `124px 28px 32px` (reminder), `88px 28px 32px` (snooze), `96px 28px 32px` (taken) | S |
| Bottom-sheet padding | `30px 28px 36px` (call confirm, action complete); `26px 28px 32px` (time picker); `26px 28px 34px` (Anna) | R/S |
| Dialog padding | `30px 26px 24px`, max-width 360px, outer padding 28px | R/S |
| Card padding | `18px 20px` (detail rows, med-added, schedule), `18px` (contact card), `24px 26px 20px` (time card), `26px` (next-dose card) | R |
| Input padding | `0 22px` (forms), `0 20px` (profile) | R |
| Option tile padding | `20px` (language, frequency), `18px` (intake), `16px 18px` (relationship rows) | S |
| Bottom nav | Wrapper `10px 24px 24px`; bar padding `10px 8px`; tab padding `9px 0`, gap 5px | S |
| Gaps | 5, 6, 8, 10, 12, 14, 16, 18, 22px (flex `gap`) | S |

---

## 5. Radius

| Element | Radius | Src |
|---|---|---|
| Phone frame | 46px | R |
| Primary buttons (90/88/86/80/78px) | 18px | R |
| Outline buttons | 16px for 64–76px buttons; 18px for 76–84px buttons (Log In, Edit Contact, Add Another Contact) | R |
| Inputs, select, option tiles, profile rows | 16px (inputs, tiles); 14px (profile input, language select, Skip button) | R |
| Back button | 14px (46×46) | R |
| Modal close button | 13px (44×44) | R |
| Dose chips | 14px (onboarding, 55px tall); 12px (Edit Medication, 46–48px tall) | R |
| Popular-medication chips, day pills, 12-hour toggle | 999px | R |
| Time-of-day chips | 16px | R |
| Cards | 18px (detail rows, info panel), 20px (contact, schedule, med-added), 22px (reminder time card), 26px (next-dose hero) | R |
| Time tiles | 18px (detail time buttons), 15px (schedule tile) | R |
| Icon chips | 14 / 20 / 22px | R |
| Bottom-nav bar / tab | 24px / 16px | R |
| Bottom sheets | 34px top corners | R |
| Dialog | 26px | R |
| Avatars, status circles | 50% | R |
| Auth logo tile | 32px (112×112) | R |

---

## 6. Elevation

| Use | Value | Src |
|---|---|---|
| Primary button | `0 12px 26px rgba(4,39,125,.22)`; Anna-sheet primary `0 10px 24px` | R |
| Destructive button | `0 10px 24px rgba(186,26,26,.25)` | R |
| Input / select / time card | `0 1px 2px rgba(0,0,0,.04)` | R |
| Detail row card, schedule card | `0 4px 14px rgba(13,92,77,.05)` | R |
| Contact / med-added card | `0 6px 18px rgba(13,92,77,.06)` | R |
| Next-dose hero (navy) | `0 18px 38px rgba(4,39,125,.26)` | R |
| Bottom nav | `0 12px 30px rgba(13,92,77,.1)` | R |
| Dropdown | `0 8px 22px rgba(0,0,0,.08)` | R |
| Dialog | `0 24px 60px rgba(8,30,24,.3)` | R |
| Anna sheet | `0 -10px 40px rgba(8,16,40,.28)` | R |
| History sheet | `0 -10px 40px rgba(8,30,24,.25)` | S |
| Toasts | `0 14px 34px rgba(4,39,125,.18)`, Anna toast `.22` | S |
| Status circles | Navy 96px: `0 12px 26px rgba(4,39,125,.28)`; teal 70px: `0 12px 26px rgba(13,92,77,.28)`; halo rings `0 0 0 5px #fff, 0 16–18px 36–40px rgba(…,.16)` | R |

---

## 7. Motion

| Name | Definition | Use | Src |
|---|---|---|---|
| `cpFade` | opacity 0→1; `.2s` dialogs, `.25s` sheets, `.3s` full-screen modals | Scrims, modals | S |
| `cpUp` | translateY(100%)→0, `.35s cubic-bezier(.2,.8,.2,1)` | Bottom sheets | S |
| `cpPop` | scale .7→1.06→1, `.3s ease` | Dialogs, success checks | S |
| `cpGlow` | inset navy glow pulse, `1.8s ease-in-out` infinite after `.3s` | Reminder modal background | S |
| `cpPulse` | scale 1→1.9 + fade, `2.2s` infinite | Anna button halo, Meet Anna mic | S |
| `cpRing` | scale .9→1.6 + fade | Call ripple | S |
| `cpWave` | scaleY .35→1, `1s` infinite | Anna "speaking" bars (`#A3BBFF`) | S |
| `cpToast` | translateY(14px)→0 + fade, `.3s` | Toasts and banners | S |
| `cpDots` | dot opacity cycle | Loading dots | S |
| `cpGlide`, `cpRoll`, `cpSway`, `cpDrift` | Welcome illustration loops | Welcome screen | S |
| Track | `transform .42s cubic-bezier(.4,0,.2,1)` | Onboarding slide | S |
| Small transitions | `transform .2s` (3 uses: carets / chevrons) | Dropdown carets | S |

**Reduced motion.** `@media (prefers-reduced-motion: reduce)` turns off only `.cp-ride` and `.cp-wheel` (Welcome riders and wheels). `cpPulse`, `cpGlow`, `cpWave`, `cpRing`, `cpDrift` and `cpSway` keep running. **S**

---

## 8. Components

All sizes are at 428px, text scale 1×. "Seen on" names the screen where the component was measured.

### 8.1 Buttons

| Variant | Size | Style | Label | Seen on | Src |
|---|---|---|---|---|---|
| Primary CTA | 372×90 (364×90 on Sign Up / Log In, where side padding is 32) | bg navy, r18, primary shadow, trailing chevron | 22/700 white | Continue, Sign Up, Send Code, Next Step, Finish | R |
| Primary, modal | 372×88 | as above | 23/700 | Take Med, Log as taken now | R |
| Primary, modal footer | 372×90 | as above | 23/700 | Snooze 15 minutes, Close (snoozed) | R |
| Primary, sheet / edit | 372×86 / 80 | as above | 21/700 | Save Changes, Save Time (86); Yes, call (80) | R |
| Primary, dialog | 308×78 | as above | 20/700 | Log Out (dialog) | R |
| Primary, Anna | 372×68 | r16, `0 10px 24px` shadow | 19/700 | Answer by voice | R |
| Destructive, dialog | 308×78 | bg `#BA1A1A`, r18, destructive shadow | 20/700 white | Delete | R |
| Outline, large | 364×84 / 372×80 / 372×76 | white, 2px navy, r18 | 20–21/700 navy | Log In (364×84), Edit Contact (80), Add Another Contact (76) | R |
| Outline | 372×76 / 72 / 70 / 66 / 64 | white, 2px navy, r16 | 18–21/700 navy | Go Back (76), Snooze / No (72), Cancel (70), Add New Contact (66), Add New Medication (64) | R |
| On-navy button | 320×74 | white, no border, r16 | 21/700 navy | Take Now (hero card) | R |
| Emergency outline | 330×56 | white, 2px `#AF5F3E`, r14 | 17/700 `#AF5F3E` | Resolve with Anna | R |
| Ghost | 372×60 | transparent, r14 | 19/700 `#5C6BB0` | Skip for now | R |
| Ghost destructive | 372×66 | transparent, r16 | 18/700 `#BA1A1A` | Delete Contact | R |
| Voice replay | 372×88 | `#E7ECFF`, 1.5px `#C7D0F5`, r18 | 19/700 navy + 15/600 `#5C6BB0` | Voice reminder playing | R |
| Back | 46×46 | white, 1.5px `#DCE4E2`, r14, navy chevron | — | All step screens | R |
| Modal close | 44×44 | `#EEF1EF`, 1.5px `#C9D5D1`, r13 | — | Reminder / missed | R |
| Call (round) | 46×46 | bg emergency, 50% | — | Contact cards | R |
| End call | 84×84 | `#E5453A`, 50% | — | Calling screen | R |
| Anna button | 56×56 at top 65 / right 28 | navy mic disc + `cpPulse` halo (opacity .24) | `aria-label` localized | See §8.5 | R |
| Day pill | 178×47 | white, 1.5px `#E2E7E5`, r999 | 15/700 navy | Previous / Next day | R |
| Stepper | 88×64 | `#FAF9F7`, 1.5px `#DCE4E2`, r18 | chevron | Time picker | R |

**States.** **S**

| State | Spec | Applies to | Src |
|---|---|---|---|
| Keyboard focus | `outline: 3px solid #04277D; outline-offset: 3px` on `:focus-visible`. On the navy hero card the ring is white (`.cp-on-navy`). Shown for keyboard focus only, not on tap. | `button`, `[role="button"]`, `input`, `select`, `textarea`, `a` | R/S |
| Pressed | `filter: brightness(.85)` on `:active`, instant, no transition | `button`, `[role="button"]` | R/S |
| Hover | None (touch-first app) | — | S |
| Disabled | None. No button in the app is disabled. | — | S |

Keyboard support added with the focus states:
- Tappable cards (medication cards, hero card, schedule items, contact cards) have `role="button"` and `tabindex="0"`, and Enter or Space activates them, like the existing tappable time cards.
- Screens that are not visible (other onboarding steps, layers under an open overlay) are made `inert`, so Tab stays on what is on screen. Before this, Tab moved focus into hidden onboarding screens and scrolled the track.

### 8.2 Inputs

| Variant | Size | Style | Src |
|---|---|---|---|
| Text input (forms) | 372×72 | white, 1.5px `#DCE4E2`, r16, padding `0 22px`, text 20/500, shadow `0 1px 2px rgba(0,0,0,.04)` | R/S |
| Text input (name, medication, dosage) | 372×74 | same; text 21/600 | R |
| Text input (Edit Medication) | 372×70 | same; text 20/600 | R |
| Text input (Profile) | 372×64 | r14, padding `0 20px`, text 19/500, no shadow | R |
| Error | — | border `#BA1A1A`. Phone field also gets ring `0 0 0 3px rgba(211,47,47,.14)`. Error row: 16/600 `#BA1A1A`. | R |
| Select (relationship) | 372×72 | like input; placeholder 20/500 `#BFC9C4`; caret rotates (`transform .2s`) | R |
| Dropdown list | 372 wide | white, 1.5px `#DCE4E2`, r16, shadow `0 8px 22px rgba(0,0,0,.08)`; rows 60px, 19/500, 1px `#F0F2F0` dividers, check 20/700 navy | R |
| Code input | 4 digits, numeric | not measured | A |

### 8.3 Selection controls

| Control | Unselected | Selected | Src |
|---|---|---|---|
| Option tile (language 84px, frequency 72px, edit frequency 66px) | white, 2px `#DCE4E2`, r16 | `rgba(4,39,125,.05)`, 2px navy, check icon (opacity toggle) | R |
| Intake tile (74px) | white, 2px `#E2E7E5`, r16 | `#E0E7FF`, 2px navy | R |
| Dose chip (onboarding 55px, r14) | white, 1.5px `#DCE4E2`, 18/700 navy | navy fill, white text | R |
| Dose chip (Edit Medication 46–48px, r12) | same, 16/700 | navy fill | R |
| Popular-med chip (46px, padding `12px 20px`) | white, 1.5px `#DCE4E2`, r999, 17/600 navy | No selected style. Tapping fills the input; the chip looks the same. | R |
| Time-of-day chip (57px, r16) | white, 1.5px `#DCE4E2`, 18/700 navy | `#E0E7FF`, 2px navy | R |
| AM/PM | see §2.5 | see §2.5 | R |
| 12-hour toggle | `#E0E7FF`, 1.5px `#C7D0F5`, r999, 15/700 navy, 115×41 | — | R |
| Text-size buttons | four "A" buttons in Profile | not measured in detail | A |

### 8.4 Cards

| Card | Size | Style | Src |
|---|---|---|---|
| Next-dose hero | 372×245 | navy, r26, padding 26, shadow `0 18px 38px rgba(4,39,125,.26)`. Icon tile 66×66 `rgba(255,255,255,.14)` r20. Name 26/700 white; detail 18/500 `#A9D7CC`; time 30/800 white. | R |
| Schedule item | 372 wide | white, 1.5px `#E8ECEA`, r20, padding `18px 20px`, shadow `0 4px 14px rgba(13,92,77,.05)`. Time tile 54×54 `#F1F5F3` r15 (18/800 + 12/700). Missed chip 14/700 `#AF5F3E`. | R |
| Reminder time card | 372×156 | white, 1.5px `#DCE4E2`, r22, padding `24px 26px 20px`. Overline 15/700 navy; time 60/700. | R |
| Detail row card | 372×86 | white, 1.5px `#E8ECEA`, r18, padding `18px 20px`. Overline 14/700; value 20/600. | R |
| Contact card | 372×102 (saved) / 140 (manage) | white, 1.5px `#E8ECEA`, r20, padding 18, shadow `0 6px 18px rgba(13,92,77,.06)`. Avatar 56 `#E0E8FF`; name 20–21/700; call button 46. | R |
| Medication-added card | 372×106 | as contact card, padding `18px 20px`; icon chip 52 `#E6F0EC` r14 | R |
| Profile row | 372×74 | white, 1.5px `#E2E7E5`, r16, padding `0 18px`, 19/700 navy | R |

### 8.5 Navigation

| Item | Spec | Src |
|---|---|---|
| Bottom nav | Bar 380×86, white, 1.5px `#EAEEEC`, r24, padding `10px 8px`, shadow `0 12px 30px rgba(13,92,77,.1)`. Wrapper gradient `#FAF9F7` 82% → transparent. | R/S |
| Nav tab | 121×64, r16, padding `9px 0`, gap 5. Active bg `rgba(4,39,125,.10)`, label navy; inactive transparent, `#9AA8A3`. Labels 13/700. | R |
| Anna button | See §8.1. Shown when `showAnna` is true on: onboarding step 7 onwards (Emergency Contact and later), the Log In flow, and all app tabs except Call. Meet Anna (step 6) uses its own centred 132px mic button instead. | S (rule `annaBtnVisible`), R |
| Back button | See §8.1 | R |

### 8.6 Overlays

| Overlay | Type | Spec | Src |
|---|---|---|---|
| Reminder, Missed | Full screen | `#E3F2EE` + `cpGlow`. Close 44×44 at top 70 / right 28. 140px halo circle. Title 34/800. "How to take it" panel. Voice replay button. Primary 88 + outline 72. | R/S |
| Taken, Snooze confirm, Snoozed | Full screen | `#E3F2EE`. 200px halo circle. Title 32–34. Body 20–22. Primary 90 (+ outline 76 on snooze confirm). | R |
| Call confirm | Bottom sheet | `#E3F2EE`, r34 top, padding `30px 28px 36px`, gap 10. 84px icon circle `rgba(4,39,125,.10)`. Title 25/700. Primary 80 + outline 72. | R |
| Action complete | Bottom sheet | `#E3F2EE`, same padding, gap 12. Shared by "Medication Saved", "Contact Saved" and similar. | S |
| Anna | Bottom sheet | `#E0E7FF`, r34 top, padding `26px 28px 34px`, gap 16, max-height 86%, blur scrim. Answer-by-voice 68px; action buttons 64px outline. | R |
| Time picker | Bottom sheet | White, r34 top, padding `26px 28px 32px`. Grab handle 44×5 `#DCE4E2` r3. Stepper 88×64. Digits 64/800. Save 86 + Cancel 64. | R |
| Medication history | Bottom sheet | White, r34 top, max-height 780px | S |
| Contact picker | Bottom sheet | `#FAF9F7`, r34 top, max-height 560px | S |
| Delete / Log out | Centered dialog | White, r26, max-width 360, padding `30px 26px 24px`. Icon circle 72 (`#FBE9E9` delete, `rgba(4,39,125,.10)` logout). Title 25/800. Primary or destructive 78 + outline 70. | R |
| Medication / contact details | Full screen | `#FAF9F7`, header padding `70px 28px 6px` | S |
| Toasts / banners | Floating | Mint or lavender, 1.5px border, r18, padding `16px 18px`, `cpToast` | S |

---

## 9. Accessibility

| Item | Status | Src |
|---|---|---|
| Touch targets | Smallest interactive targets are 44×44 (modal close) and 46×46 (back, call). Medication Details' Edit and Delete render at 80px and 66px and grow with the text size (up to 112px and 92px). | R |
| Contrast | High-contrast secondary text `#2C3531` is the default | R |
| Selection | Option tiles combine colour, 2px border and a check icon. Chips combine fill and colour. AM/PM uses `aria-pressed`. | R/S |
| Focus | 3px navy ring (white on navy) on `:focus-visible`; hidden screens are `inert`; Enter / Space activate `role="button"` cards | R/S |
| Screen-reader labels | 31 static `aria-label`s are English only. Anna button and some others are localized. | S |
| Reduced motion | Partial (see §7) | S |
| Languages | English, German, Russian (395 strings each) | R/S |

---

## 10. Known inconsistencies in the app (not fixed)

These are present in `index.html` today. They need your decision before anything in the app is changed.

1. ~~Fonts~~ — fixed, see §10a.
2. ~~Medication Details buttons compressed~~ — fixed, see §10a.
3. **Text below 14px.** Bottom-nav labels (13px), the relationship overline on the contact card (13px), and AM/PM in the schedule tile (12px).
4. ~~No focus or pressed states~~ — fixed, see §10a. Hover and disabled styles still do not exist (none are used).
5. **Reduced motion covers only the Welcome illustration.**
6. **Not responsive.** A fixed 428px frame is clipped on phones narrower than about 442px.
7. **Props vs fallbacks.** `emergencyColor` and `highContrast` defaults (`#AF5F3E`, true) differ from the code fallbacks (`#E07B4F`, false).
8. **Language after reload.** The app always starts in English, although the chosen language is saved to `localStorage`.
9. **Onboarding track width.** It is declared 6420px wide for 16 screens of 428px (6848px). The last screen overflows the container, but still renders.

## 10a. UI fixes applied (2026-11-18)

| # | Issue | Fix in `index.html` | Verified |
|---|---|---|---|
| 1 | 42 buttons rendered in Arial | `button:not([style*="font-family"]){font-family:inherit;line-height:1.15}`; inputs, selects and textareas also inherit | All button and container sizes unchanged in 39 states; only glyph widths changed by 1–7px. EN, DE, RU. |
| 2 | Medication Details Edit / Delete squeezed to 46 / 37px (as low as 33 / 27px at larger text) | `flex: none` on both buttons in the scrolling column | 80 / 66px at text size 1, 90 / 75, 102 / 84, 112 / 92px at sizes 2–4, in EN, DE and RU. No text clipping. The content scrolls. |
| 3 | No focus or pressed states | Focus ring and pressed filter (§8.1); keyboard access for tappable cards; `inert` on hidden screens | Keyboard test: Tab stays on screen and inside overlays; Enter opens cards and selects tiles. |

## 11. Changes from the previous spec (handoff)

| Topic | Previous spec | App (verified) |
|---|---|---|
| Emergency colour | `#E07B4F` | `#AF5F3E` (default prop) |
| Secondary text | `#4A5955` default | `#2C3531` (high contrast on by default) |
| Reminder / missed / snooze / taken | Mint bottom sheets | Full-screen mint modals |
| Anna | Inline "Speak to Anna" tiles, floating entry | One top-right Anna button; lavender Anna sheet with voice input; Meet Anna screen |
| Languages | EN, ES, DE, FR, RU | EN, DE, RU |
| Minimum text size | 14px | 12px and 13px exist (see §10) |
| Button press feedback | "darken / settle" | 15% darker on press (`brightness(.85)`), no animation |
| Reduced motion | All decorative motion | Welcome illustration only |
| Input text | 19px/500 | 20/500, 21/600 or 19/500 depending on screen |
| Outline button radius | 16px | 16px or 18px depending on height |
| New tokens | — | `#234B43`, `#2F5249`, `#243A6E`, `#A9D7CC`, `#E7ECFF`, `#BFC9C4`, `#EEF1EF` / `#C9D5D1`, `#CFE0DA`, `#EAEEEC`, `#E5453A` |
