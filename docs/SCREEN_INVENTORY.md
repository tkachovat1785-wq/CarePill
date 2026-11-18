# CarePill — Screen Inventory

Two app phases:
- **`onboarding`** — a horizontal track of full screens, index = `obStep`, moved via
  `transform: translateX(-obStep * 428px)`.
- **`app`** — tabbed shell (Pillbox / Profile / Call) once setup completes.

Modals are **overlays** driven by a single `overlay` state value (`null` when none). A separate `done`
state drives the unified completion popup (layered above everything).

Legend: **bg** = screen background. All screens are 428×926.

---

## A. Onboarding track (obStep order)

### 0 — Splash  (`bg #E3F2EE`)
- **Purpose:** Launch screen; tap anywhere to begin.
- **Layout:** Centered logo: 128px area with pulsing `cpPulse` halo (`rgba(4,39,125,.14)`) behind a
  rounded-square pill icon. Tagline below.
- **Interaction:** Tap screen → obStep 1.

### 1 — Phone Entry  (`bg #FAF9F7`)
- **Purpose:** Enter phone number to receive an SMS code.
- **Components:** Back button (hidden if no history); title "Let's get started"; paragraph; **Phone
  Number** input (`inputmode=tel`, placeholder `+1 (202) 555-0147`); error row on empty; fine print
  ("one-time SMS"). Footer **Send Code** primary button.
- **Validation:** non-empty → obStep 2, else error.

### 2 — SMS Verification  (`bg #FAF9F7`)
- **Purpose:** Enter 4-digit code.
- **Components:** Back; title "Enter your code"; masked-number paragraph; large 4-digit code input
  (`inputmode=numeric`, maxlength 4, 96px tall); error row; "Didn't get it? **Resend code**" (fires a
  toast). Footer **Verify**.
- **Validation:** length ≥ 4 → obStep 3.

### 3 — Language  (`bg #FAF9F7`)
- **Purpose:** Pick language.
- **Components:** Back; title "Choose your language"; subtitle; scroll list of option tiles (English /
  Spanish / German / French / Russian — label + native subtitle, selected highlight). Footer **Continue** → obStep 4.

### 4 — Name Input  (`bg #FAF9F7`)
- **Purpose:** First name.
- **Components:** Back; "What's your name?"; **First Name** input (autofocus); error row. Footer
  **Continue** → obStep 5 (requires non-empty).

### 5 — Welcome  (`bg #FAF9F7`)
- **Purpose:** Warm confirmation; emotional anchor.
- **Components:** **Animated inline-SVG illustration** (332×258) of an older man (navy sweater, white
  hair/beard, balancing arm) + woman (teal polka-dot sweater, silver bun, round navy glasses, hand on
  his shoulder) riding a skateboard; mint blob + lavender accent circles bg; gentle motion lines.
  Heading "Welcome, {firstName}!"; paragraph. Footer **Let's Begin** → obStep 6.
- **Motion:** riders `cpGlide` bob, wheels `cpRoll`, hair `cpSway`, lines `cpDrift`; reduced-motion safe.

### 6 — Emergency Contact (Set-Up / selection)  (`bg #FAF9F7`)
- **Purpose:** Add an emergency contact (or skip).
- **Components:** Back row + "Step 1 of 2 · Safety"; title "Emergency Contact"; **Relationship** dropdown
  (Caregiver/Daughter/Son/Spouse/Friend/Other); **Full Name** input; **Phone Number** input; error rows;
  "Choose from Contacts" (opens Contacts picker overlay). **Footer:** primary **Continue** + secondary
  ghost **Skip for now**.
- **Interactions:** Continue → validates name+phone, saves contact, obStep 7. **Skip for now** → obStep 8
  (Med Intro), **preserving** entered fields. This screen is also the **redirect target when the last
  contact is deleted** (form cleared).

### 7 — Emergency Saved  (`bg #FAF9F7`)  *(no back button)*
- **Purpose:** Confirm contact(s) saved; manage list.
- **Components:** 80px top spacer (back removed); 96px success circle (`#0D5C4D` check, `cpPop`); title
  "Emergency Contact Saved"; paragraph; contact card(s) (avatar initials + relationship/name/phone +
  round call button in `emergencyColor`; tap row → Contact Details overlay); outline **Add New Contact**
  (→ obStep 6, fields reset). Footer **Next Step** → obStep 8.

### 8 — Medication Intro  (`bg #FAF9F7`)
- **Purpose:** Introduce med setup.
- **Components:** Back; 200px circular illustration area; heading + copy; CTA → obStep 9.

### 9 — Medication Name  (`bg #FAF9F7`)
- **Purpose:** Name the medication.
- **Components:** Back + "Medication"; "What medication do you take?"; **Medication Name** input
  (placeholder "Example: Aspirin"); error row; "Speak to Anna" assist tile. Footer **Continue**
  (`continueMedName`) → obStep 10. **Redirect target when the last medication is deleted.**

### 10 — Dosage  (`bg #FAF9F7`)
- **Purpose:** Set dose.
- **Components:** Back; **Dosage** input + quick-pick dose chips (e.g. 100 mg…); "Speak to Anna" tile.
  Footer **Continue** → obStep 11.

### 11 — Frequency  (`bg #FAF9F7`)
- **Purpose:** Choose how often.
- **Components:** Back; option list — Once a day / Twice a day / Three times a day / **Weekly**. If
  **Weekly**: reveals a 3-col **day selector** grid (Mon–Sun, check when on) + a **time card** (tap to
  open time picker). Error if none. Footer: **Save** (weekly path → `saveWeekly`) or **Continue** → obStep 12.

### 12 — Reminder Time  (`bg #FAF9F7`)
- **Purpose:** Set reminder time(s) — one slot per daily dose.
- **Components:** Back + "Medication · Step 4 of 4"; per-slot **time card** (caption + big time + "Tap to
  change" affordance — whole card opens the time picker) and a row of period chips
  (Morning/Afternoon/Evening/Night, selected highlight); "Speak to Anna" tile. Footer **Continue** → obStep 13.

### 13 — Medication Added (Success)  (`bg #FAF9F7`)  *(no back button)*
- **Purpose:** Confirm med saved; manage meds; finish or add another.
- **Components:** 80px top spacer; 96px success circle; "Medication Added"; "Your reminders are ready.";
  medication card(s) (centered pill icon, name, "dose · freq · time"; tap → Medication Details overlay);
  outline **Add another medication** (→ obStep 9, fields reset); "Speak to Anna" tile. Footer finishes
  onboarding → app phase (Pillbox).

---

## B. App phase (tabbed shell)

### Pillbox (Home / Today)  (`bg #FAF9F7`)
- **Purpose:** Daily medication schedule.
- **Components:** Header greeting; day navigator (prev/next day pills, relative label); **hero** upcoming
  dose card (navy, name/dose/time, **Take** button → Reminder overlay; tap → Med Details); "Today's
  schedule" list of dose cards with status chips (Taken `#E6F4EF`/`#0D5C4D`, Missed `#BA1A1A`, Upcoming);
  per-row action; "all done" state. Floating **Anna** assistant entry (if `showAnna`). Bottom nav.
- **State:** `taken{}`, `dayOffset`, `meds`, `deletedMeds`, `medEdits`.

### Profile / Settings  (`bg #FAF9F7`)
- **Purpose:** Personal info, language, text size, sound, history entry.
- **Components:** Back; **Personal information** (first/last name inputs); **Language** dropdown;
  **Text size** 4-step segmented control (drives the global font scale); **Sound** sliders (System
  volume / Reminder chime / Anna's voice); **Medication History** row → History overlay. Bottom nav.

### Call (Emergency call)  (`bg #E3F2EE`)
- **Purpose:** Simulated emergency call to a contact.
- **Components:** "Calling emergency contact" overline; pulsing avatar (`cpRing`); name/relationship/phone;
  "Connecting…" dots; round **End Call** button (`#E5453A`). Returns to origin screen on end.

---

## C. Overlays (driven by `overlay` state)

| `overlay` | Name | Style | Notes |
|---|---|---|---|
| `reminder` | Reminder | mint bottom sheet | "Time for your medication" + Take / Snooze. |
| `success` | Success (dose taken) | full mint screen | `cpPop` big check. |
| `takenFinal` | Taken — final dose | full `#FAF9F7` screen | Welcome-palette celebration. |
| `missed` | Missed / Anna prompt | lavender bottom sheet | missed-dose message + actions. |
| `anna` | Anna voice | lavender bottom sheet, blur scrim | animated waveform (`cpWave`). |
| `contacts` | Contacts picker | bottom sheet | pick a system contact → fills form. |
| `callConfirm` | Call confirmation | mint bottom sheet | "Do you want to call?" |
| `history` | Medication History | white bottom sheet (max-h 780) | grouped by **Day, Date** (header text `#1E2E29`/800) → time + med + status rows. |
| `medDetail` | Medication Details | full `#FAF9F7` screen | centered pill icon, **scheduled times (tap to edit)**, detail rows, **Edit Medication** (outline) + **Delete Medication** (ghost `#BA1A1A`). |
| `medEdit` | Edit Medication | full screen | name/dose/frequency/day-grid/time fields (tap to edit) /info; **Save Changes** + Cancel. Save → Medication Saved popup. |
| `contactDetail` | Contact Details | full screen | avatar, info rows, **Edit Contact** + **Delete Contact** (ghost `#BA1A1A`). |
| `contactEdit` | Edit Contact | full screen | relationship/name/phone; Save → Contact Saved popup. |
| `timePicker` | Time Picker | white bottom sheet | shared by ALL time edits (see DESIGN_SYSTEM §7). |
| `confirmDeleteMed` | Confirm delete medication | centered dialog | "Delete this medication?" Delete / Cancel. |
| `confirmDeleteContact` | Confirm delete contact | centered dialog | "Delete this emergency contact?" Delete / Cancel. |
| `snoozeConfirm` | Snooze this reminder? | mint bottom sheet | Snooze 15 min / Go Back. |
| `snoozed` | Reminder Snoozed | mint bottom sheet | **persistent**, manual **Close** only (no auto-dismiss). |

### Unified completion popup (`done` state — separate, top-most)
Reminder-Snoozed-sized mint bottom sheet with a check icon, title, body, and a single **Close** button.
Used for: **Medication Deleted, Contact Deleted, Medication Saved, Contact Saved.** An optional `onClose`
callback runs when Close is pressed.

---

## D. Key flows & rules

- **Direct time editing:** every displayed medication time (frequency weekly card, reminder slots,
  details, edit) is a tappable `role="button"` card opening the shared time picker; Save updates the time
  immediately and persists across screens.
- **Delete medication:** removes med + its reminders; if it was the **last** med, redirect to obStep 9
  (Medication Name) so the user never lands on an empty list. Then show "Medication Deleted" popup.
- **Delete contact:** show "Emergency Contact Deleted" popup; **do not redirect while open**; on **Close**
  redirect to obStep 6 (Set-Up Emergency Contact) and **clear all fields** (name, relationship, phone).
- **Skip emergency:** "Skip for now" advances to Med Intro without requiring/clearing data.
- **No "Anna added …" toast** for Metformin or Lisinopril specifically (other meds still toast).

---

## E. State variables (reference)
`phase` ('onboarding'|'app'), `obStep` (0–13), `tab` ('pillbox'|'profile'|'call'), `overlay` (see C),
`done` ({title, body, onClose}|null), `contacts[]`, `meds[]`, `deletedMeds[]`, `medEdits{}`, `taken{}`,
`dayOffset`, `hist[]`, form fields (phoneReg, code, language, firstName/lastName, relationship, fullName,
phone, medName, dosage, frequency, weekDays[], weeklyTime, times[], editName/Dose/Freq/Times/WeekDays…),
time-picker (`tpOpen, tpKind, tpIdx, tpH, tpM, clock24`), `fontStep` (0–3), volumes, `callTarget`.
