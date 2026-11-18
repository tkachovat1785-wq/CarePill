# CarePill documentation

These files come unchanged from the CarePill design project's handoff bundle (`design_handoff_carepill/`).

| File | Content |
|---|---|
| `DESIGN_SYSTEM.md` | Colours, typography, spacing, radius, shadow, motion, component recipes, accessibility. |
| `SCREEN_INVENTORY.md` | Screens, overlays, flows and state, as described in the handoff. |
| `tokens.css` | Design tokens as CSS custom properties. All 31 colour values in it are used in `index.html`. |

## Differences from the app (checked 2026-11-18)

The handoff documents were written before the latest app version. Where they disagree, `index.html` is the source of truth.

1. **Languages.** `SCREEN_INVENTORY.md` lists Spanish and French on the Language screen. The app supports English, German and Russian only.
2. **Onboarding order and step numbers.** The app's order is:
   - 0 Splash
   - 1 Language
   - 2 Phone
   - 3 SMS code
   - 4 Name
   - 5 Welcome
   - 6 **Meet Anna**
   - 7 Emergency contact
   - 8 Contact saved
   - 9 Medication intro
   - 10–14 Medication steps 1–5 (name, dosage, frequency, reminder time, how to take it)
   - 15 Medication added

   Sign Up / Log In is a separate entry screen after Language. `SCREEN_INVENTORY.md` uses an older order and has no Meet Anna screen.
3. **Anna entry point.** The app has one Anna button at the top right. The inline "Speak to Anna" tiles described in `SCREEN_INVENTORY.md` are no longer in the app.
4. **`emergencyColor` default.** `DESIGN_SYSTEM.md` and `tokens.css` give `#E07B4F`. The app's default prop value is `#AF5F3E`, and `#E07B4F` is one of its options.
5. **Missing folders.** `react-tailwind/` and `prototype/`, which the handoff refers to, were not part of the source and are not included.
