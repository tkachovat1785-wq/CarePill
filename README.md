# CarePill

CarePill is an interactive prototype of a medication-reminder app for older adults.
It runs entirely in the browser on a single 428 × 926 mobile artboard.

## Files

| File | Purpose |
|---|---|
| `index.html` | The app (exported from the design tool as `CarePill Onboarding.dc.html`). |
| `support.js` | Runtime that `index.html` needs. Keep it next to `index.html`. |
| `docs/` | Design-system and screen documentation. See [`docs/README.md`](docs/README.md). |

## Opening the app

- **GitHub Pages / any web server:** serve the repository root and open `index.html`.
- **Locally:** run `python3 -m http.server` in this folder and open <http://localhost:8000/>.

An internet connection is required. At start-up the app loads:

- React 18.3.1 and ReactDOM 18.3.1 from `unpkg.com`
- the Inter font from Google Fonts

## Languages

English, German and Russian.

## Voice features (Anna)

- **Speech output** uses the browser's built-in speech synthesis and the voices installed on the device.
- **Voice input** uses the browser's Web Speech API (`SpeechRecognition`) and needs microphone permission.
- **When voice input is unavailable**, the app shows a message and everything can still be done by tapping. This happens when the browser has no speech recognition or the microphone is blocked.

## Previous version

The version that was on `main` before this update is preserved in two places:

- the branch `backup/original-2026-07-04`
- the tag `original-2026-07-04` (commit `c64042c`)
