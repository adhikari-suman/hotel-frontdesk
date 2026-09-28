# Design 15: Leadlight

**Idea.** The front desk as an Arts and Crafts leaded window. Each of the 64 rooms is a glass pane set in dark lead came: 16 panes per floor, 4 floors. The glass texture shows the room's state, and the state is always printed as text too. The app is held together by the same leading. Navigation is one 3×3 window: six desk screens in clear glass and three admin screens in amber glass.

Open `index.html` for the gallery. The screens are in `screens/` and the @2x screenshots are in `png/`.

## Tokens

| Token | Hex | Meaning |
|---|---|---|
| `--lead` | #22302E | Lead came: structure, heavy region borders, header, body text |
| `--ground` | #EEF0EB | Glass ground: page background |
| `--pane` | #FAFBF8 | Frosted pane: panels and cells |
| `--teal` | #007274 | Teal glass: the one primary action, the current nav pane, selection |
| `--verd` | #43A099 (ink #1F6E68, tint #DDEFE9) | Vacant, ready, success |
| `--olive` | #868221 (ink #5E5B12) | In house (reeded glass) |
| `--amber` | #946A07 (tint #EBDDB0) | Arrivals (seeded glass), admin-only surfaces and markers |
| `--rose` | #9E3F63 | Departures (ribbed glass) |
| `--ruby` | #A3262A | Destructive actions, out of order (hatched glass), errors |
| `--came` | #C3CBC3 | Hairline came inside regions |

**Glass textures for status.** Colour is never the only signal. Each status has its own texture as well as a text label and an icon:

- In house: reeded (vertical ribs)
- Arriving: seeded (dots)
- Departing: ribbed (horizontal)
- Vacant: clear with a sheen
- Out of order: hatched

## Type

- **Federo** (display): screen titles, section headings, room numbers, big totals. It has Mackintosh-style straight-stroke lettering.
- **Figtree** (400–700, tabular figures): all UI and body text.
- Both fonts are self-hosted in `assets/fonts/` as woff2 files, with their OFL licences.
- Minimum text size is 11px. Labels use sentence case, never all caps.

## Layout and components

- **Transom header.** A dark lead band holds the 3×3 window nav, the screen title in Federo, the date and shift, and the user and role. A came-tick edge sits underneath it.
- **Window nav.**
  - The lit teal pane is the current screen.
  - Admin panes use amber reeded glass. For receptionists they are dimmed and carry a lock.
  - For admins the lock is removed, and a key badge sits on the role chip.
- **16-column content grid.** Regions are "leaded" with 3px lead borders, and dividers inside them are hairlines.
- **Room board.** 4 × 16 panes with type bands across the top (Queen 01–06, Twin 07–10, Deluxe 11–14, Suite 15–16 on every floor).
- **Lattice stats.** Cells separated by 3px lead.
- **Lattice meters.** 20 squares show promo usage: ruby when used up, grey when expired.
- **Buttons.**
  - Primary: teal with a squared-rose glyph and a hard lead offset shadow. Only one per screen.
  - Secondary: outline.
  - Destructive: ruby outline on a faint hatch, always visibly different.
- **Choice panes.** Room types, payment methods and roles are shown as leaded choice panes. The selected pane turns into teal glass.

## Permissions shown in the UI

- On receptionist screens the admin nav panes are locked.
- The promo field says "Codes are created by admins". On 08, a dashed amber panel shows the receptionist's read-only view of codes.
- 09 has a role matrix, with admin-only rows tinted amber.

## Features by screen

| Screen | What it shows |
|---|---|
| 01 Today | Status board with arrivals (Check in) and departures (Check out) |
| 02 Availability | 14-night matrix with tint by rooms free, a selected range and Start booking |
| 03 New booking | Dates, room type, guest, extras (breakfast, dinner, pickup), promo apply and a live total |
| 04 Booking | Extras add/remove, promo, charges, history, the Rebook panel open, and Cancel with terms and fee |
| 05 Check in | ID, room assignment, card guarantee, keys, extras upsell |
| 06 Check out | Dated folio with nights, promo, extras and tax, plus payment, holds and Settle |
| 07 Rooms | Type table with inline edit; add a room; delete a room. Delete is blocked for types and booked rooms and allowed for room 416, which has no bookings |
| 08 Promo codes | ID, code, title, required date range, optional limit, status; the create form shows the required-date error |
| 09 Staff | Staff by role and status (active, invited, deactivated), create user, what each role can do |

## Hero numbers

Deluxe 3 × $238 = $714.00. summer2026 at 15% off room nights = −$107.10. Breakfast 2 × 3 × $18 = $108.00. Pickup $55.00. Subtotal $769.90. Tax 12% = $92.39. **Total $862.29.**

## Data interpretation

- **Tonight counts.** "41 occupied tonight" is read as 32 staying + 9 arrivals. On the board, 7 departures (still in house this morning), 2 out of order and 14 vacant make up the rest of the 64 rooms, so 21 rooms are left to sell.
- **Check-out date.** Screen 06 is dated Sat 17 Oct 2026, the hero's departure day, so its folio is complete. The other screens are dated Wed 14 Oct.
- **Room assignment.** Room types are grouped by position on each floor. This is an invented layout.
- **Extra names.** The canonical guest list has 10 guests. Extra surnames and departing guests were invented to fill the 64-room board.

## Open decisions and placeholders

1. **Promo "offer" is a placeholder.** "15% off room nights" (and "7th night free" on longstay7) is not defined by the brief. It is marked "(placeholder)" in the UI.
2. **Promo date range semantics.** The hero booking uses summer2026, whose dates ended 30 Sep, for a 14–17 Oct stay. The design assumes the code's dates apply to when the rate is quoted or booked, not to the stay. It shows this as "honoured from quote Q-26-0932 (29 Sep)". This needs a product decision.
3. **Tax 12%** is a placeholder rate.
4. **Cancellation terms** are invented: free until 48 hours before check-in, then the first night is charged at the booked rate after promo.
5. **Rebook repricing.** When dates move to a different rate period, is the old rate kept? The design shows the same rate and a $0.00 difference.
6. **Pre-authorisation and incidentals hold** amounts ($150) are illustrative.
7. **Room-type delete** is modelled as "blocked while any room of the type has a booking ahead". Room delete is blocked the same way.

## Files

- `assets/leadlight.css` is the one shared stylesheet. `assets/fonts/` holds the woff2 fonts and OFL licences.
- Screens are static HTML with inline SVG icons: square caps, mitred joins, own drawings.
