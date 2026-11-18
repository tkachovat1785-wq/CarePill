# CarePill — Screen Inventory

**Version:** 2026-11-18. Rebuilt from `index.html` (commit `55aede1`). Component specs are in [`DESIGN_SYSTEM.md`](DESIGN_SYSTEM.md).

**How this was checked:**
- Every screen and overlay listed here was rendered and walked through in Chromium.
- Where a screen was not rendered, the entry is marked **(source only)**.

**Phases.** The app has four phases:
- `onboarding`: a horizontal track of 16 screens, index `obStep`
- `auth`: the Sign Up / Log In choice
- `login`: phone and code for existing users
- `app`: the tabs Pillbox, Call and Profile

Modals are driven by one `overlay` value. A separate `done` value drives completion popups.

**Anna button (top right):**
- Shown from onboarding step 7, in Log In, and on every app tab except Call.
- Tapping it opens the Anna sheet. The sheet speaks a hint for the current screen and offers "Answer by voice".

## A. Onboarding track

| # | Screen | Key content | Next |
|---|---|---|---|
| 0 | Splash (`#E3F2EE`) | App mark with halo, "CarePill", tagline, page dots. Tap anywhere. | 1 |
| 1 | Language | "Choose your language"; tiles English / Deutsch / Русский with translated subtitle and check; Continue | Sign Up / Log In |
| — | Sign Up / Log In (`#E3F2EE`, separate `auth` phase) | Logo tile 112px, "CarePill" 40/800, tagline; Sign Up (primary 90), Log In (outline 84) | Sign Up → 2, Log In → Log In flow |
| 2 | Phone | "Let's get started", phone input, SMS consent, Send Code | 3 |
| 3 | SMS code | "Enter your code", 4-digit input, "Resend code", Verify | 4 |
| 4 | Name | Icon chip, "What's your name?", First Name input (error if empty), Continue | 5 |
| 5 | Welcome | Animated couple-on-skateboard illustration, "Welcome, {name}!", Let's Begin | 6 |
| 6 | **Meet Anna** | "Meet Anna", 132px mic button that plays Anna's introduction in the chosen language, hint lines, Continue. The top-right Anna button is not shown here. | 7 |
| 7 | Emergency contact | "STEP 1 OF 2 · SAFETY"; Relationship select (Caregiver / Daughter / Son / Spouse / Friend / Other); Full Name; Phone (errors when empty); Choose from Contacts; Continue; Skip for now | 8 or 9 |
| 8 | Contact saved | Contact card with call button, Add New Contact, Next Step | 9 |
| 9 | Medication intro | "Medication Setup", Add Medication | 10 |
| 10 | Medication · Step 1 | Medication name input, popular chips (Aspirin, Metformin, Lisinopril) | 11 |
| 11 | Medication · Step 2 | Dosage input, chips 5 / 10 / 25 / 50 / 100 / 500 mg, ＋ Custom | 12 |
| 12 | Medication · Step 3 | Frequency tiles: Once a day / Twice a day / Three times a day / Weekly | 13 |
| 13 | Medication · Step 4 | Reminder time cards (60px time, "Tap to change" opens the time picker), time-of-day chips | 14 |
| 14 | Medication · Step 5 | "How to take it": Before / With / After meals; water ½ / 1 / 2 glasses; optional own instructions; Save Medication | 15 |
| 15 | Medication added | Teal check, "Medication Added", med card, Add Another Medication, Finish | App, Pillbox |

## B. Log In flow (`login` phase)

| Step | Content |
|---|---|
| 0 | "Welcome back", phone input, Send Code |
| 1 | Code input, Verify. Then the app opens with demo data (Maria Garcia, 3 doses). |

## C. App tabs

| Tab | Content |
|---|---|
| Pillbox | Date heading; greeting; Previous / Next day pills; "NEXT DOSE" navy hero card with Take Now; "X of Y taken today"; "TODAY'S SCHEDULE" items (status Taken / Missed with "Resolve with Anna"); Add New Medication; bottom nav. After 3 s idle on today, the next due reminder opens automatically. |
| Call | Without contacts: missing-contact screen. With contacts: confirm sheet, then simulated "Calling emergency contact" screen with 84px end-call button. No real call is placed. |
| Profile | Avatar and name; Medication History; Emergency Contact; personal info (first and last name); Language select; Text size (4 × "A"); Sound sliders (System, Reminder chime, Anna's voice); Log Out |

## D. Overlays

| Overlay | Type | Content |
|---|---|---|
| `reminder` | Full screen | "⏰ Time for your medication", med name, dose · time, "How to take it" panel, voice replay, Take Med, Snooze, close |
| `missed` | Full screen | "Missed dose check-in", same layout, Log as taken now, Snooze |
| Taken (`done`) | Full screen | "Taken!", "{med} marked as taken.", Go Back to Pillbox Menu |
| `snoozeConfirm` | Full screen | "Snooze this reminder?", Snooze 15 minutes, Go Back |
| `snoozed` | Full screen | "Reminder Snoozed", Close (manual close) |
| `snoozeFollowup` | Full screen | Follow-up reminder **(source only)** |
| `medDetail` | Full screen | Name, dose, tappable scheduled times, frequency, instructions, water, additional info, Edit Medication, Delete Medication |
| `medEdit` | Full screen | Name, dosage chips, frequency tiles, Save Changes, Cancel |
| Time picker | Bottom sheet | Hour / minute steppers, AM/PM, 12-hour toggle, Save Time, Cancel |
| `confirmDeleteMed` / `confirmDeleteContact` | Dialog | Delete / Cancel |
| Action complete (`done`) | Bottom sheet | "Medication Saved", "Contact Saved", "Time updated." etc., Close |
| `history` | Bottom sheet | Medication history by day **(source only)** |
| `manageContacts` | Full screen | Contact cards with call buttons, Add Another Contact |
| `contactDetail` / `contactEdit` | Full screen | Relationship, phone, status, Edit Contact, Delete Contact; edit form |
| `contacts` | Bottom sheet | Contact picker **(source only)** |
| `callConfirm` | Bottom sheet | "Do you want to call?", Yes, call / No |
| `missingContact` | Full screen | Set up emergency contact, or call 112 **(source only)** |
| `anna` | Bottom sheet (lavender) | Spoken hint, "Answer by voice" (speech recognition), context actions (Add a medication, View today's schedule, Call emergency contact), Close |
| `logout` | Dialog | Log Out / Cancel. On confirm, all entered data is cleared and the app returns to Language. |

## E. Key rules (verified)

- **No dead ends.** Deleting the last medication returns to medication entry. **(source only)**
- **Times are editable.** Every displayed medication time opens the shared time picker. Verified: 8:00 → 9:00 is saved.
- **Calls are simulated.** No `tel:` links, no navigation.
- **Voice is optional.** If speech recognition is missing or blocked, Anna shows a message and the app works by touch.
