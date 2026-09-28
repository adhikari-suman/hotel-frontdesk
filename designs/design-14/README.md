# Design 14: Lift Car

The front desk as a 1930s hotel lift. The navigation is the lift's floor indicator: a semicircular brass dial across the top of every screen. Each screen is a numbered floor on the arc and the needle points to the current one. The three admin screens are the "office floors", past a key-switch segment. Rooms are drawn as four landings of sixteen stepped deco doors, top floor first, the way you'd read them from the lift.

Open `index.html` for the gallery. Screens are static HTML in `screens/`, and screenshots at 2x are in `png/`.

## Layout

- **Band (top, full width, lacquer jade).** Hotel name, date and shift on the left. The dial nav sits in the middle. The signed-in user, their role and search are on the right. A brass double rule closes the band.
- **Dial nav.** Desk floors 1–6 (Today, Availability, New booking, Booking, Check in, Check out) rise up the left side of the arc. After them comes the key-switch segment. Office floors 7–9 (Rooms, Promo codes, Users) come down the right side.
  - A receptionist sees the switch as a brass lock labelled "Admin key", and the office floors are dimmed with a lock in place of their number.
  - An admin sees the switch turned to mint and labelled "Key on".
  - The current floor is filled mint, and the brass needle points at it.
- **Title row.** A Limelight page title, a one-line summary, and the screen's actions.
- **Content.** Bays (panels) on a flexible grid. Room grids always use 16 columns, one per room on a floor. Work screens use a main column plus a 400–440px side column for the totals slip or edit panel.

## Tokens

| Token | Hex | Meaning |
|---|---|---|
| `--jade` | #123F35 | Lacquer: nav band, occupied rooms, primary buttons |
| `--jade-3` | #2C6B5A | Jade as text on light; discounts, "Yes" |
| `--ground` | #EFF4EE | Ivory-mint page ground (cool, not cream) |
| `--card` | #FBFCF9 | Bay surface |
| `--ink` | #1D2A26 | Body text |
| `--ink-2` / `--slate` | #44524C / #5E6A64 | Secondary and meta text |
| `--line` / `--line-2` | #CAD7CD / #DFE8E1 | Hairlines |
| `--brass` | #C4A25B | Fittings, rules, table heads, arrivals, admin marks |
| `--brass-deep` | #86652A | Brass as text on light |
| `--brass-pale` | #F3E9CF | Arrival tint, notes, promo-code chips |
| `--mint` | #9ADCA0 | Current floor, receptionist role chip |
| `--mint-pale` | #DDF1DE | Ready rooms, active codes |
| `--rose` / `--rose-pale` | #9A4A3C / #F4DDD5 | Departures |
| `--verm` / `--verm-pale` | #B23A2E / #F7E0DB | Destructive actions, out of order, validation errors |

## Type

- **Limelight** (display, one weight): page and bay titles, room numbers, floor numerals, big totals. It is never used below 14px.
- **Urbanist** (variable, 100–900): all UI, forms, tables and money. Tabular lining figures, body 14px/500, and a minimum size of 11px.
- Both fonts are self-hosted from `assets/fonts/` under the SIL OFL. The licence texts are included.

## Components

- **Dial nav**: floors on an elliptical arc, a sunburst behind them, a needle, and the key-switch segment.
- **Door cell**: stepped ziggurat top, room number, type and one line of context (guest, "to 16 Oct", "To clean"). Each status is shown three ways: fill colour, a glyph in the corner and a word.
  - In house: solid jade with a dot
  - Due out: rose with a left arrow
  - Arriving: brass with a right arrow
  - Ready: mint with a ring
  - To clean: white with a dashed border and dashed ring
  - Out of order: vermilion hatch with a cross
- **Status tag**: a pill with a glyph and a word. It covers rooms, promo status (active, scheduled, expired, limit reached) and user status (active, invited, deactivated).
- **Occupancy dial** on Today: a segmented arc from 0 to 64 with the needle at 41.
- **Floor steps**: numbered circles used only for real sequences (booking flow, check-in).
- **Totals slip**: itemised lines, subtotal, tax, and the total in Limelight between brass rules.
- **Bay**: 1px border and a 2px radius. `.deco` bays get a brass-tinted border and a warm header wash. Nothing uses one-sided accent borders.

## Rules

- There is one primary action per screen: solid jade with a brass edge. Secondary buttons are outlined, and ghost buttons are for dismiss/clear.
- Destructive buttons are vermilion outlines (solid only inside a confirmation) and state the consequence, e.g. "Cancel booking and charge $226.58".
- Colour is never the only signal. Every status has a glyph and a word.
- Permissions are always visible:
  - The office floors are locked on the dial for receptionists.
  - "Codes are created by admins" appears next to every promo field.
  - Room delete is replaced by a disabled "Booked" button while a room has bookings.
  - The role matrix is on Users.

## Screens

| File | Role | Notes |
|---|---|---|
| 01-today | Receptionist | Occupancy dial, arrivals with Check in, departures with Check out, 64-room landings |
| 02-availability | Receptionist | 4 types × 14 nights, selection Deluxe 14–17 Oct, Start booking bar |
| 03-new-booking | Receptionist | Stay, room type, guest, extras (breakfast, dinner, pickup), promo field rejecting summer2026 and suggesting autumn26, live totals |
| 04-booking-rebook | Receptionist | AH-26-0417 detail, extras add/remove, promo (read only), charges, history, Rebook panel open (15–19 Oct, +$266.89), Cancel with terms |
| 05-check-in | Receptionist | ID, room 312 on the floor-3 map, card guarantee (current step), keys, dinner upsell |
| 06-check-out | Receptionist | Folio by night with promo lines, tax, settle $862.29 on the held card |
| 07-rooms | Admin | Types with price/count and edit/delete (delete blocked), per-room list with delete for unbooked 107, Edit Deluxe panel, delete confirm, Add room form |
| 08-promo-codes | Admin | PC-001…005 with id, code, title, required date range, optional limit and usage, create form with required-date validation |
| 09-users | Admin | 6 staff with role and status, create user (invite), what each role can do |

## Data notes and open decisions

- **Promo offer is a placeholder.** The brief doesn't define what a code gives. "15% off room nights" is used throughout, and "7th night free" is used as the label for longstay7. The Offer field on the create form is marked as a placeholder.
- **The hero booking uses summer2026, which ended on 30 Sep while "today" is 14 Oct.** The design assumes a code is checked against the date the booking is made:
  - AH-26-0417 was made on 22 Sep, so it keeps the discount.
  - A new booking made today is refused the code and offered autumn26 (03).
  - This rule needs confirming: it could instead be the stay dates, or both.
- **Rebooking keeps the original discount.** This is an assumption, stated in the Rebook panel.
- **Cancellation terms are a placeholder:** free until 48 hours before arrival, first night charged after that.
- **Check-out is shown on Sat 17 Oct**, the hero's departure day, so the folio is complete. All other screens use Wed 14 Oct.
- **Tax is 12% on everything, extras included.** This is a placeholder.
- **Admins can also do every desk action** in the role matrix. The brief only lists admin-only powers, so this needs confirming.
- **Added synthetic data.** These are needed for full lists and are not in the canonical set:
  - Departure guests beyond Ethan Park (Ingrid Solberg, Tariq Haddad, Chloé Martin, Arjun Mehta, Nora Kelly, Pieter de Vries), Marta Kowalski in 303 and Julien Moreau as Hannah's second guest.
  - The invited user Lena Hoffmann.
  - Previous-stay amounts, the card ending 5521 and the room-to-type mapping. The mapping is floors 1–2 Queen 01–12 and Twin 13–16; floor 3 Twin 01–04 and Deluxe 05–16; floor 4 Twin 01–04, Deluxe 05–08 and Family 09–16.
- **The two out-of-order rooms are 107 (Queen) and 406 (Deluxe).**
