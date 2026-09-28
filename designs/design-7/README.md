# Design 7 — Counting Frame

The front desk read like a soroban (Japanese counting frame). Each of the 64 rooms is a rod with one bead. When a guest is in, the bead is pushed up against the beam. When a guest arrives today, it sits half-way. When the room is free, it rests low. An out-of-order room shows a broken red rod. A stay is drawn as a short rod with one bead per night. The nine screens are beads on a single rod across the top of the page, and the admin screens sit past a locked post.

Open `index.html` to see the gallery. The screens are in `screens/`, and 2× screenshots are in `png/`.

## Tokens

| Token | Hex | Meaning |
|---|---|---|
| `--frame` | `#1E2633` | Top frame, beam, primary buttons, dark tiles |
| `--face` | `#E9EDF2` | Work surface |
| `--band` | `#F4F6F9` | Title band under the frame |
| `--plate` | `#FAFBFC` | Panels |
| `--pale` | `#A9CDD6` | Selection: picked nights, selected rows, promo codes |
| `--green` / bead `#237548` | `#2F8F57` | Occupied, active, done, discounts |
| `--amber` | `#D99A1E` | Arriving, in progress, 1–2 rooms left (dark text on it) |
| `--peri` / bead `#4F5DB5` | `#6C7BD0` | Due out today |
| `--red` / bead `#AE2F28` | `#C23B32` | Out of order, full, destructive |
| `--plum` / bead `#6A3F7C` | `#7B4B8E` | Admin-only beads, tags and the locked post |
| `--ink` / `--ink-2` / `--ink-3` | `#1A2230` / `#4A5566` / `#566172` | Text, secondary text, muted text (AA on every surface) |

Bead fills are darker than the base tokens so that 11px letters on them pass WCAG AA.

## Type

- **Sofia Sans Condensed** (650–800) is used for room numbers, money, dates in tables, and panel and page titles.
- **Sofia Sans** (400–650) is used for body text and controls. Tabular figures are on everywhere.
- Both fonts are self-hosted in `assets/fonts/` under the SIL OFL (`assets/fonts/OFL.txt`). The minimum text size is 11px, used only for bead letters and rod captions.

## Components

- **Bead**: a hexagonal status marker that always carries a letter (O occupied, A arriving, D due out, V vacant, C needs cleaning, X out of order) or sits next to a text label. Colour is never the only signal.
- **Rod board**: 4 floors × 16 rods. The bead's height on the rod shows the room's state, and the beam runs through the whole floor. Room 312 (the hero booking) is outlined.
- **Nav rod**: the screens are hexagonal beads on one rod. The current screen is the light bead. Admin beads are plum and sit past a lock post. On receptionist screens they are greyed out, locked and labelled "Admin only".
- **Stay rod**: shows check-in and check-out with one bead per night. It's used in the selection, new booking and check-in panels.
- **Tally row**: bead or bar ticks show counts. Room types show rooms in use tonight, and promo codes show uses against the limit (each mark is 5%).
- **Context sheet**: a right-hand panel for the one active task, such as the selection, booking total, rebook, settle or create form. Each screen has exactly one dark primary button.
- **Danger zone**: destructive actions (cancel booking, delete room, deactivate, revoke, end code) are red-outlined or solid red. They never use the ink primary style.

## Rules

- Receptionist screens show admin nav beads locked. Promo codes are apply-only, with the note "Codes are created by admins".
- Admin screens carry an "Admin area" banner, and the signed-in role is always shown next to the user.
- Delete stays locked while a room or room type has current or future bookings. The reason is shown inline. Room 415 has no bookings, so it shows the delete confirmation.
- The date range on a promo code is required. The form shows the error state when the end date is missing. The usage limit is optional ("No limit").

## Open decisions / placeholders

- **Promo "offer"**: the brief doesn't define it. "15% off room nights" is a placeholder in the create form and on the hero booking.
- **summer2026 dates**: this code ended on 30 Sep 2026, but the hero stay is 14–17 Oct. The design treats the code's date range as the booking window and says the code was "honoured from the 28 Sep quote". This needs a rule.
- **Tax 12%** is a placeholder. The cancellation terms (free until 48 h before arrival, then the first night is charged) are also a placeholder.
- **Check-out** is shown as a departure-day view (Sat 17 Oct), so the hero folio is complete. Every other screen uses Wed 14 Oct.
- Should admins also be able to take booking actions? This design says no.
- The guest surnames on the room board beyond the brief's ten guests are synthetic filler.
