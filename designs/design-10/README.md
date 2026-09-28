# Design 10 · Whiteprint

Every screen is an architect's diazo whiteprint: violet linework on white paper. Each screen is one drawing sheet with a zoned border, a sheet index for navigation and a title block that says what the sheet is, when it was drawn and who drew it. Rooms are drawn as floor plans. Status is a drawing convention that still reads when printed in one colour, and it always comes with its code. Stays are drawn as dimension lines, and tables are set as drawing schedules.

The scene is a bright front desk in the daytime, so the sheet is light. The design uses no cards, no dark rail and no colour-coded tiles. The structure comes from the sheet itself: the frame, the title strip and the drawing titles.

## Sheet anatomy (every screen, admin screens included)

- **Frame.** A 1 px violet trim line sits 16 px inside the viewport. A 20 px zone band carries coordinates A–F along the top and bottom and 1–4 down both sides, with a tick line at each zone boundary. The drawing border inside it is 2 px.
- **Title strip (right, 216 px).** From top to bottom:
  - the project block (Alder House, front desk);
  - the **sheet index**, which is the navigation;
  - a middle area for the legend or general notes;
  - the **title block** at the bottom right: sheet title, date, time, drawn by (the signed-in user, with sign-out) and the sheet number in large lettering.
- **Sheet index.**
  - A-101 Today, A-102 Availability, A-103 Bookings. The four booking sheets, A-103.1 to A-103.4, appear under Bookings while one of them is open.
  - B-201 Rooms, B-202 Promo codes, B-203 Users. On receptionist sheets the B series is listed but locked and marked "Admin only", so the limit is visible rather than hidden.
- **Drawing titles.** Each section is labelled like a view on a drawing: a split bubble (detail number over sheet number), a name in Saira capitals with a 2 px underline, and a one-line note. On Today the plan's title sits *below* the plan, as view titles do on a real sheet.

## Tokens

### Colour

| Token | Hex | Role |
|---|---|---|
| `--paper` | `#FDFDFF` | The sheet and every surface |
| `--line` | `#8800DD` | Diazo violet: linework, links, focus of attention, the one primary action (6.7:1 on paper, white on it 6.8:1) |
| `--line-dk` | `#6A00AD` | Hover and pressed on violet |
| `--ink` | `#1D0F33` | Body text (17.7:1) |
| `--ink-2` | `#5E4E78` | Secondary text (7.3:1 on paper, 5.5:1 on poché) |
| `--ink-off` | `#7A6A92` | Disabled text (4.8:1) |
| `--poche` | `#E7D8F8` | Poché fill: in house; the share of a night already sold |
| `--wash` | `#F0E6FC` | Selection wash: chosen room, selected nights, selected row |
| `--grid` | `#ECE6F7` | Construction grid: read-only fields |
| `--rule` | `#D5C4EE` | Inner schedule rules (non-text) |
| `--field` | `#9D86C6` | Input outlines, disabled dashes (3.1:1) |
| `--red` | `#B0102A` | Redline, the architect's correction colour: errors, blocked actions, overlaps, destructive actions |

Hatching is `--line` at 52% alpha with 1 px lines every 6 px. There are no gradients, no shadows and no blur.

### Type

- **Saira**, variable width 50–125 and weight 100–900, self-hosted. It is the technical lettering:
  - sheet titles (27 px, 620);
  - drawing titles (15 px);
  - labels and table heads (11 px, +0.08em, 92% width);
  - dimension text, the title block and the sheet numbers.
  - It is always set in capitals.
- **Public Sans**, variable weight. Body and interface text at 12–16 px. It is also used for the status codes (OCC, ARR, DUE, VC, OOO) in bold capitals, because Saira's letter O and its zero are nearly identical and "OOO" read as "000".
- **Red Hat Mono** for codes: booking refs, promo codes and IDs.
- Every data cell uses tabular, lining figures.

### Spacing, radius and line weights

- **Spacing:** 4 / 8 / 12 / 16 / 20 / 24 / 32 / 40 px. Sections are separated by 28–32 px, not by boxes.
- **Radius:** 0 everywhere. Only drawing bubbles, radios and level markers are round.
- **Line weights:**
  - sheet trim 1 px; drawing border and title strip 2 px;
  - level shells (outer walls) 2 px, rooms 1.5 px;
  - schedule outer border 2 px, head rule 1.5 px, inner rules 1 px;
  - dimension lines 1 px with 2 px oblique ticks.

## Components (in `assets/whiteprint.css`)

- **Level plan** (`.plan`, `.lvl`, `.rm`)
  - Each level is a shell wall around 8 rooms and a corridor with a dashed centre line.
  - Column bubbles 01–08 above the plan are the room suffixes, and level bubbles on the left are the floors, so 704 is level 7, column 04.
  - Every room has a door opening on the corridor side. Arriving rooms show the door leaf and a swing arc.
  - The plan is reused on Today (all 8 levels), New booking (level 8 as a room picker) and Check-in (levels 6 and 7, where ready rooms are pickable and the rest are visible but disabled).
- **Dimension line** (`.dim`): `FRI 2 |/—— 2 NIGHTS ——/| SUN 4`, with extension lines, oblique ticks, text above the line and optional notes under each end ("from 14:00", "by 11:00").
  - Used for every stay, the availability selection, the rebook (the current stay is struck through) and the promo overlap check.
  - The `--strike` variant marks a stay that is being replaced.
- **Schedules** (`.sch`): tables set like door and room schedules. The screens use:
  - the arrivals and departures schedules;
  - the room, code and staff schedules;
  - the folio;
  - the revision log.
- **Revision log** (`.rev` + `.delta`): booking history and room changes. Each revision is numbered in a delta triangle, and an unsaved change gets a dashed delta. The same delta appears on the edited field, so the pending Deluxe price change on Rooms is tied to its log entry.
- **Title block, sheet index, drawing title, room tag** (`.rtag`: number over a label, boxed).
- **Stamp** (`.stamp`): a double-ruled approval stamp. It previews "Checked in · 27 Sep 2026 · 10:46 · NR".
- **Callouts:**
  - **Redline** (`.redline`): blocked or conflicting, for example "Can't delete Family Suite" or "Overlaps winter26".
  - **Note** (`.note`, dashed violet): information that governs the action.
  - **Permission line** (`.perm`, with a lock icon).
- **Buttons.** Primary is solid violet, one per screen. Secondary is outlined; quiet is text only; danger uses the redline colour. Disabled buttons have a dashed outline, grey-violet text and a stated reason nearby. A pressed button (Rebook while its panel is open) gets a wash with an inner line.
- **Fields.** Labels sit above in Saira capitals, and a red asterisk marks required fields. Fields have these states:
  - Focus: violet 1 px border, 1 px ring and a 4 px wash halo, plus a 2 px ink outline for keyboard focus on controls.
  - Changed: 2 px violet border on the wash, with "Was $238.00" below.
  - Error: redline border and message.
  - Read-only: construction-grid fill.
- **Other controls:** a square check with a violet fill, a round radio, and a stepper.
- **Also drawn:** the availability poché cells, the Family Suite room-by-night chart (break marks show stays that began earlier), the building section (A–A) with level datums, the 24-hour shift scale with a "now" line, and the promo overlap diagram.
- **Browser surfaces:** the text selection is violet with white text, scrollbars are a violet thumb on a wash track, the caret is violet, and link underlines are offset 3 px.

## Status without colour

| Status | Drawing | Code |
|---|---|---|
| In house | Poché: solid light fill | OCC |
| Arriving | Dashed outline plus a door leaf and swing arc | ARR |
| Due out | Diagonal hatch; the label sits on a paper wipeout | DUE |
| Vacant, ready | Empty outline | VC |
| Out of order | Cross-hatch plus a corner-to-corner X | OOO |

The code is printed in every room, and the legend in the title strip gives the counts (43 / 10 / 5 / 4 / 2 = 64; tonight 53 of 64 sold, 83%). Other screens use the same logic:

- **Availability:** the shaded height of each cell is the share sold, next to the number free. Full nights read "0 full".
- **Room chart:** poché for in house, an outline for reserved, a dashed outline for arriving today, cross-hatch for out of order.
- **Promo codes:** Active is poché, Scheduled is dashed, Used up is hatched, Expired is an X.
- **Users:** Active is poché, Invited is dashed, Deactivated is an X.
- **Roles:** Admin is a solid label, Receptionist an outlined one. Both carry the word.

Every symbol is paired with a word or code, so none of this depends on colour.

## Permissions made visible

- **Receptionist sheet index:** the B series is locked with "Admin only".
- **New booking promo field:** "Codes are created by admins. You can apply a code to a booking, not create or edit one."
- **Rooms:** delete is disabled on every type, and the Family Suite row explains why in a redline: 14 upcoming bookings and 7 rooms occupied tonight. The Deluxe price edit notes that the 23 upcoming bookings keep $238.
- **Users:** the role cards list what each role can do, and what it can't. The receptionist card lists: can't change rooms, create promo codes or manage users.
- **Promo codes:** a receptionist preview shows what the desk will see, including the permission line.

## Responsive behaviour

- **1440:** the full sheet. Today fits in one 900 px viewport, title block included.
- **≤ 1279:**
  - the title strip narrows to 200 px;
  - Today's schedules move under the plan;
  - the booking side columns narrow;
  - wide schedules scroll inside their frame.
- **≤ 760:**
  - the zone band is dropped;
  - the sheet index moves to the top as a compact list, and the legend and title block go to the bottom;
  - the level plans and schedules scroll horizontally inside the drawing border.

## Open decisions

1. **The promo "Offer" field is not in the brief.** The brief defines a code as id, code, title, date range and optional count. The offer column and field ("15% off room nights", "7th night free") are needed to price a booking but must be confirmed.
2. **Placeholders, not spec:**
   - the 12% tax;
   - extras prices (breakfast $18 and dinner $42 per guest per night; pickup $55 per trip);
   - room prices ($136 / $166 / $238 / $366);
   - the hotel name "Alder House".
3. **Booking detail sheet numbers.** A-103.1 to A-103.4 are this design's convention for open booking sheets under A-103 Bookings. A real bookings list sheet is not part of the nine screens.
4. **Status codes are set in Public Sans, not Red Hat Mono.** The direction asked for codes in Red Hat Mono. Red Hat Mono and Saira both make "OOO" look like "000", so status codes use Public Sans bold capitals. Red Hat Mono is still used for refs, promo codes and IDs.
5. **"Card now" guarantee option.** New booking shows it as the alternative to "Pay at check-in", which is selected, as the content asks. Whether card-now is offered depends on payments, which are out of scope.
6. **Search.** No global search is drawn, because the content does not call for one. The sheet index is the only navigation.

## Files

- `index.html`: the gallery or cover sheet (G-001). It holds the direction summary, palette, lettering, status key, the placeholders note and all nine PNGs.
- `assets/whiteprint.css`: tokens and components.
- `assets/fonts/`:
  - self-hosted `Saira-latin-var.woff2`, `PublicSans-latin-var.woff2` and `RedHatMono-latin-var.woff2`;
  - their SIL Open Font License texts (`OFL-*.txt`).
- `screens/01-today.html` … `09-users.html`: static HTML with no JavaScript and no network requests. Each file has an inline Lucide icon sprite (ISC licence).
- `png/`: the same nine sheets at 1440 px, @2x, full page.

All names, bookings and figures are synthetic demo data.
