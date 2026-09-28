# Design 1: Transit Map

**Idea.** The hotel drawn as a transit diagram. Each room type is a coloured line, and every stay is a journey on that line, from an arrival stop to a departure stop, so availability, rebooking, check-in and the folio use the same picture. Today's departures are the one loud surface, printed on line yellow. The navigation is a route map too: a solid desk line for receptionists and a dashed admin branch, locked for anyone without the admin role.

Open `index.html` for the gallery. The screens are in `screens/`, and the @2x screenshots are in `png/`.

## Tokens

| Token | Hex | Meaning |
|---|---|---|
| `--yellow` | `#F6E94B` | Departures board, primary button label, totals band, active station |
| `--yellow-soft` | `#FBF4B0` | Warnings, "2 or fewer left", selected table row |
| `--ink` | `#202428` | Text, occupied rooms, primary button fill |
| `--ink-2` / `--muted` | `#4A5159` / `#6B737C` | Secondary and tertiary text |
| `--platform` | `#ECEEEF` | Page ground |
| `--paper` | `#FFFFFF` | Boards and sheets |
| `--rule` / `--rule-2` | `#D3D8DC` / `#E4E7EA` | Hairlines |
| `--queen` | `#3F74C4` | Queen route line and arrivals |
| `--twin` | `#4F7064` | Twin Double route line, admin branch, admin role |
| `--deluxe` | `#6510DE` | Deluxe route line, current selection, focus ring |
| `--family` | `#C23F7C` | Family Suite route line |
| `--red` | `#D9262B` | Destructive actions, out of order, sold out, errors |
| `--ok` | `#2F7A4E` | Settled, verified, discounts |

Radii are 2px on boards, 4px on fields and buttons, and round on stations and route ends.

## Type

**Jost** (SIL OFL, self-hosted in `assets/fonts/`, licence in `assets/fonts/OFL.txt`) is used for everything. It is a geometric sans in the tradition of transit-map lettering. Tabular lining figures are requested globally. Out-of-order rooms read "Closed" rather than "OOO" because Jost's round O looks like a zero.

- Display: 34/900 page titles and 96/900 on the gallery page
- Board title: 20/900
- Times and room numbers: 16 to 18/900
- Body: 13 to 14/400 to 500
- Labels: 12/700, and 12px is the floor everywhere
- The smallest text on any screen is 12/700

## Components

- **Route nav** (`.route`, `.stn`): the stations are screens. The active station is a larger yellow stop. Admin stations sit on a dashed sage branch. Receptionists see them with dashed rings and a lock; admins see solid rings.
- **Board** (`.board`, `.board.yellow`): a heavy 2px ink rule under the header and a stop-list table (`.tt`) with a large time column and room numbers.
- **Room cell** (`.rc`): shows the room number, a short status word and a type-coloured bottom stripe. Each status also has its own fill: solid ink for occupied, blue-tinted for arriving, yellow for departing, dashed outline for free and red hatching for out of order.
- **Stay line** (`.bk`): a coloured bar with round stops at each end. The proposed stay is dashed violet.
- **Availability matrix** (`.mx`, `.cell`): free count, a word ("free", "left", "sold out") and an occupancy bar.
- **Ticket** (`.ticket`): the booking summary, with a journey header (arrival stop to departure stop), line items and a yellow total band.
- **Steps** (`.steps`): the check-in sequence. Done steps are solid; steps still to come are dashed track.
- **Status tag** (`.st`): an outlined word, used for every state, so meaning never depends on colour alone.
- **Callouts** (`.note`): `warn` in yellow, `red` for blocked or destructive, `lock` in sage for permissions.

## Rules

- Each screen has one primary action: an ink button with a yellow label. Everything else is outlined. The stylesheet is `assets/transit.css`.
- Destructive actions use red outlines or red fill and are placed apart from the primary action. A blocked delete shows a locked button and a red note that gives the reason.
- Permissions are always visible:
  - Admin stations are locked on receptionist screens.
  - Admin screens carry an "Admin only" tag.
  - Promo code fields say codes are created by admins.
  - The Users screen has a role matrix.
- Room types always show both a colour and a name (or a two-letter code: Q, TD, DX, FS).

## Screens

1. **Today.** Arrivals and departures boards, pickups and turnover, and all 64 rooms by floor.
2. **Availability.** The 14-night free matrix, Deluxe stay lines and a pick panel.
3. **New booking.** Four ordered stops (dates and room, guest, extras, promo) and a live ticket.
4. **Booking detail.** Extras add/remove, promo, charges and a history route. The rebook panel is open (moving to room 315), and the cancel panel shows the terms and fee.
5. **Check-in.** ID check, room assignment on the floor plan, payment pre-authorisation (the current step), keys and an extras offer.
6. **Check-out.** The folio by date, holds, settlement and folio changes. The screen is dated Sat 17 Oct.
7. **Rooms (admin).** Type CRUD with an inline price edit, delete blocked while booked, per-room edit (207 out of order) and an add-room form.
8. **Promo codes (admin).** Five codes with their date ranges on a timeline, optional limits with usage meters, and a create form showing a required end-date error.
9. **Users (admin).** Staff with roles and status (active, invited, deactivated), a create-user form, the permission matrix and recent changes.

## Open decisions and placeholders

- **Promo "offer."** "15% off room nights" (and 10% for autumn26) is a placeholder. The brief doesn't define offers.
- **Promo window.** The hero booking uses summer2026 (1 Jun to 30 Sep) for a 14 to 17 Oct stay. Screens 03 and 04 show it accepted because the quote was issued on 28 Sep. It is still open whether the window applies to the booking date or the stay dates.
- **Tax.** The 12% rate is a placeholder and is applied to every line, extras included.
- **Placeholder amounts.** The cancellation terms (free until 48 hours before arrival, then the first night after promo), the $100 incidentals hold and the room move rule on rebook are all placeholders.
- **Check-out date.** Screen 06 is dated Sat 17 Oct, the hero's departure date. It includes a dinner added on 15 Oct, so the folio total ($956.37) is higher than the booking total ($862.29).
- **Extra guest names.** Some departures and stay-line guests (Nadia Haddad, Lars Eriksen, Grace Liu and others) are extra synthetic names, added to fill the canonical counts.
- **Room layout per floor.** This is an assumption: floors 1 and 2 have Queen 01–10 and Twin 11–16; floor 3 has Queen 01–04, Twin 05–08 and Deluxe 09–16; floor 4 has Deluxe 01–08 and Family Suite 09–16.
