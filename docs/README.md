# CarePill documentation

Version 2026-11-18. These documents were rebuilt from the app in this repository (`index.html`, commit `55aede1`). They replace the earlier design-handoff versions, whose differences from the app are listed in `DESIGN_SYSTEM.md` §11.

| File | Content |
|---|---|
| `DESIGN_SYSTEM.md` | Layout, colours, typography, spacing, radius, elevation, motion, components, accessibility. Each value is marked R (rendered measurement), S (read from the app's CSS) or A (assumption). |
| `SCREEN_INVENTORY.md` | Every onboarding screen, app tab and overlay in the current flow, including the Meet Anna screen. |
| `tokens.css` | CSS custom properties and component recipes with the same values. |

## How the values were measured

- **Browser and states:** headless Chromium at 428×926 with the app's default props. 41 screen states were walked through in English, and in German and Russian where relevant.
- **Measurement:** `getComputedStyle` and `getBoundingClientRect` on every visible button, input, text and container.
- **Borders:** Chromium reports 1.5px borders as 1px, so border widths are taken from the CSS source.

## Open issues in the app

`DESIGN_SYSTEM.md` §10 lists issues found in the app. They are documented, not fixed, and wait for a decision:

- buttons rendering in Arial instead of Inter
- compressed buttons on Medication Details
- text below 14px
- no focus, hover or pressed states
- partial reduced-motion support
- no responsive layout below 442px
