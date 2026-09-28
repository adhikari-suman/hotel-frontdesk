# Design 13: Tide Table

The front desk read like a hydrographic chart and tide almanac. Occupancy rises and falls night by night as a tide curve, the 64 rooms are soundings on a four-floor chart, and every status is a buoy with its own shape as well as its colour.

Open `index.html` for the gallery. Screens are in `screens/`, @2x screenshots in `png/`, and the shared stylesheet and fonts in `assets/`.

## Direction

- **Metaphor.** Nautical chart + tide table. The Availability screen shows an "occupancy tide" (rooms occupied per night, with the peak nights marked as high water). Free rooms per type are shaded like water depth: pale for shoal (few free), deep channel for plenty, and hatched red for sold out.
- **Navigation.** No side rail and no top tab bar. The navigation is docked at the **bottom** as a graduated chart scale bar. Desk stations (Today, Availability, New booking, Bookings) sit left of a **datum mark**; admin stations (Rooms, Promo codes, Staff & roles) sit right of it, hatched. Receptionists see the admin stations locked and labelled "Admin only". The current station is filled channel yellow.
- **Almanac band (top).** Hotel, the date in italic serif, the time, a 14-night occupancy sparkline with tonight marked, search, and the signed-in person with a role badge (Receptionist in aqua, Admin hatched).

## Tokens

| Token | Hex | Meaning |
|---|---|---|
| `--ink` | #13294B | Chart ink: text, primary buttons, occupied rooms |
| `--paper` | #EEF3F4 | Survey paper page ground (cool, with faint contour lines) |
| `--sheet` | #FAFCFC | Panel surface |
| `--rule` | #C9D6DA | Borders and table rules |
| `--slate` | #5B6B7C | Secondary text |
| `--aqua` | #73CAD0 | Shoal aqua: fills, tide area, free-room depth (never text) |
| `--aqua-deep` | #2E8F98 | Deep channel: tide line, most free |
| `--sea` | #2F8466 | Vacant and ready, discounts, valid |
| `--channel` | #E8B530 | Arrivals, current nav station, focus ring, selected range |
| `--depth` | #3C6FA8 | Departures |
| `--buoy` | #C8321E | Destructive actions, out of order, errors |
| `--u` | 6px | Base spacing unit |

## Type

- **Source Serif 4 Italic** (OFL): the "hydrographic italic". It is used for headings, dates, nights, big totals and floor numbers, which are the things that flow.
- **Archivo**, variable width (OFL): UI, tables and forms. Room numbers use a condensed width (about 78%), and tables use about 88–94%. It sets upright for fixed things. All figures are tabular.
- Self-hosted woff2 files and licences are in `assets/fonts/`.

## Components

- **Soundings.** Room tiles show number, buoy, type and guest surname. Occupied tiles are filled ink. Arriving and due-out tiles carry a coloured top edge, out-of-order tiles are hatched red, and rooms to clean are hatched grey.
- **Buoys.** Status glyphs: occupied is a filled circle, vacant is a hollow green circle, arriving is a yellow triangle, due out is a blue square, out of order is a red diamond, and to clean is a hatched circle. A word always goes with the glyph.
- **Chart panels.** A sheet with a 3px ink "depth rule" on top. Open editing panels (Rebook, Edit room type, Create code, Create user) use a heavier 2px ink frame with an offset aqua shadow. Destructive panels have a buoy-red top rule.
- **Depth matrix.** Free rooms per type × 14 nights, shaded by depth. The selected stay is outlined with a yellow keel line.
- **Reckoning.** Totals list with the calculation under each line and a large italic total.
- **Legs.** Numbered steps, used only where the flow really is a sequence (new booking, check-in).
- **Permission notes.** Hatched, dashed-border note with a lock icon, e.g. "Codes are created by admins".
- **Code calendar.** Promo codes are drawn as bands across June 2026 to February 2027 with a Today line.

## Rules

- There is one primary (ink) button per screen. Secondary buttons are outlined. Destructive actions are red, outlined until confirmation and solid only on the final confirm.
- Status is never shown by colour alone: shape + colour + word.
- Minimum text size is 11px. Sentence case everywhere, no all-caps labels.
- Admin-only features are marked in three places: locked nav stations, the "Admin only" badge in the page header, and the permissions table.
- Delete is blocked while a room type or room has future bookings, and the reason is stated. Deleting a room with no bookings needs the room number typed to confirm.

## Open decisions and placeholders

- **Promo "offer"** (e.g. "15% off room nights", "20% off room nights") is a placeholder. The brief defines a code, title, date range and limit, but not the discount itself.
- **summer2026 vs hero dates.** The code runs 1 Jun to 30 Sep 2026, but the hero stay is 14–17 Oct. We assume the date range governs the **booking date**; the hero booking was made on 18 Sep. Screen 03 still shows the code applied so the totals match the other designs. Decide whether the range means booking date or stay date.
- **Tax 12%** is a placeholder applied to the subtotal after discount (room, extras and discount).
- **Cancellation terms** are placeholders: free until 48 h before arrival, then the first night is kept.
- **Deposit** of the first night ($238) and a **$100 incidentals hold** are placeholders.
- **Check-out screen** is dated Sat 17 Oct 2026 (the hero's departure day) and includes dinner for 2 added at check-in ($84). All other screens are dated Wed 14 Oct.
- **Rate-change effective date** and **draft room 317** on the Rooms screen are illustrative.
- Extra guest names on the Today board (departures, stay-overs) are synthetic additions beyond the canonical list.

## Totals used

Hero booking: $714.00 room − $107.10 promo + $108.00 breakfast + $55.00 pickup = $769.90, tax $92.39, total **$862.29**. With dinner at check-in: subtotal $853.90, tax $102.47, total **$956.37**, balance after the $238 deposit **$718.37**.
