# CarePill documentation

Version 2026-11-18, rev. 2. These documents were rebuilt from the app in this repository (`index.html`, commit `55aede1`) and updated for the UI fixes listed in `DESIGN_SYSTEM.md` §10a. They replace the earlier design-handoff versions, whose differences from the app are listed in `DESIGN_SYSTEM.md` §11.

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

Fixed (see `DESIGN_SYSTEM.md` §10a): buttons rendering in Arial, compressed buttons on Medication Details, missing focus and pressed states.

Still open (`DESIGN_SYSTEM.md` §10), waiting for a decision:

- text below 14px
- partial reduced-motion support
- no responsive layout below 442px

## Visual component library

The repository `Design-System-Care-Pill-App` has a visual library with components captured from this app (pages "Verified App Components" and "Spec Audit"). It uses the same values as these documents. Update PR: https://github.com/tkachovat1785-wq/Design-System-Care-Pill-App/pull/1
