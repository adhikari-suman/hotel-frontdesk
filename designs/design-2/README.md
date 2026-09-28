# Design 2: Split-Flap

**Idea:** the front desk as a station concourse. Arrivals and departures appear on split-flap boards. Every room number, date, booking reference and total sits on a hinged flap tile with an upper and a lower half. The app's screens are stops on one route line.

Open `index.html` for the gallery. The nine screens are in `screens/` and the 2x screenshots are in `png/`.

## Tokens

| Token | Hex | Meaning |
|---|---|---|
| `--board` | `#172A6B` | Flap boards, occupied rooms, route line sidebar, selected state |
| `--board-hi` / `--board-lo` | `#22387F` / `#12225A` | Upper and lower halves of a flap tile |
| `--signal` | `#FFC72C` | The one primary action per screen, current route stop, flap text on the date |
| `--ground` | `#E9ECF2` | Page background ("concourse") |
| `--card` | `#FFFFFF` | Panels, inputs |
| `--ink` | `#141B3A` | Text |
| `--steel` | `#5B6478` | Muted text, labels |
| `--rule` | `#D3D8E3` | Borders |
| `--arr` | `#2656BE` | Arrivals, Check in button (code ARR) |
| `--dep` | `#7A5BA8` | Departures, Check out button, Fri/Sat nights (code DEP) |
| `--go` | `#2F8A3B` | Free rooms, completed steps, discounts (code FREE / OK / ON) |
| `--stop` | `#B51B77` | Destructive actions, out of order (code OFF), required marks |
| `--amber-bg` | `#FFF4D2` | Attention: low availability, current step, cleaning (code CLN) |

## Type

- **Antonio** (variable, 100–700): the flap characters, page titles, panel headings and big numbers. Its narrow width suits a flap display.
- **Instrument Sans** (variable, 400–700): all interface text, tables and forms, with tabular figures turned on.
- Both fonts are self-hosted in `assets/fonts/` with their OFL licences. There is no monospace face.

## Layout

- **Route-line sidebar (232px, navy).** The six desk screens are stations on a solid yellow line (codes D1 to D6). Past a dashed "Admin zone" box, the line turns dashed and grey for Rooms, Promo codes and Users (A1 to A3). For a receptionist these stops show a lock. The current stop is a large yellow dot.
- **Flap strip (top).** It shows the date and clock as flap tiles, plus tonight's counts: 41 in house, 9 arrivals, 7 departures, 2 out of order. Search sits on the right.
- **Content.** A work area on the left and a fixed right column (360–440px). The right column holds the running total, the open action panel (Rebook, Edit room type, Create code, Create user) or the payment block.
- **Rooms.** Always shown as 4 floors × 16 columns, matching the physical building (Today board, Rooms admin grid).

## Components

- **Flap tile** (`.flap`): one tile per character, with a split gradient and a 1px hinge line. Variants: yellow text (`.y`) and light (`.lite`).
- **Room tile** (`.rm`): room number, type code, guest surname, then a status code chip. The states are OCC, IN, ARR, DEP, FREE, CLN and OFF, and every state carries text plus a fill or hatch.
- **Status tag** (`.tag`): a short code in a flap face followed by words.
- **Departure-board tables** (`.dtable`): ETA or due time as flap tiles, then an action button in the arrival or departure colour.
- **Ticket** (`.ticket`): a navy header with flap tiles, dashed line items, a total row and the primary action.
- **Action panel** (`.rebook`): a navy-headed panel with a 2px navy frame, used for Rebook, Edit room type, Create code and Create user.
- **Step bar** (`.steps`): only where the content is a real sequence (check-in).
- **Blocked delete** (`.blocked`): a dashed magenta box that explains why deletion is locked.

## Rules

- Each screen has one yellow primary button. Arrival (cobalt) and departure (violet) buttons act as row actions.
- Destructive actions use a magenta outline, and their label names the consequence ("Cancel booking and charge $226.58").
- Colour is never the only signal: every status has a code or a word, and out of order is also hatched.
- Text is 11px or larger.
- Permissions are visible:
  - Receptionist screens lock the admin stops.
  - The promo field says codes are created by admins.
  - Admin pages carry an "Admin only" pill.
  - Users shows a role-by-permission matrix.

## Feature coverage

- **Booking actions:** create (03), rebook with a price difference (04), cancel with terms and a charge (04), check in (05), check out and settle (06).
- **Extras:** breakfast, dinner and pickup, added or removed on 03 and 04, offered as an upsell on 05, itemised on the folio on 06.
- **Promo codes:** a receptionist applies one (03, 04). An admin creates one, with a required date range and an optional limit (08).
- **Rooms CRUD:** add a type, edit price, delete (allowed for a draft type, blocked while booked), and add a room number or mark it out of order (07).
- **Users:** create and invite a user; change role, deactivate, reactivate, and resend or revoke an invite; view the permission matrix (09).

## Open decisions and placeholders

1. **Promo offer.** The brief doesn't define what a code gives. "15% off room nights" is a placeholder on every code, and the Create code form shows an "Offer: not defined" field.
2. **summer2026 dates.** The hero booking applies summer2026, but that code ended 30 Sep and "today" is 14 Oct. The design says the booking was made on 29 Sep, inside the window, so the code is honoured. That assumes a code's dates are checked against the booking date, not the stay dates. This needs confirming.
3. **Rebook keeps the promo.** Rebooking keeps the original code at its percentage, even though the code has now expired.
4. **Tax 12%** is a placeholder, applied to room nights after discount plus extras.
5. **Cancellation terms** (free until 48 h before arrival, then first night plus tax) are invented for the screen.
6. **Admin desk rights.** The design assumes admins can do all receptionist tasks, marked * on the Users screen.
7. **Check-out date.** Screen 06 shows the hero's departure day (Sat 17 Oct, 10:48), not "today", so the flap strip there shows no tonight counts.
8. **Room layout by floor** is our own assumption: Queen on 101–116 and 201–208, Twin Double on 209–216 and 301–308, Deluxe on 309–316 and 401–408, Family Suite on 409–416. The out-of-order rooms are 207 and 414.
9. **Synthetic extras.** Departures guests beyond the canonical list, the incidentals hold ($150), the draft "Accessible Queen" type and the upcoming booking counts on Rooms are synthetic, added to show the states.
