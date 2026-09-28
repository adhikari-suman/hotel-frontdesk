# Design 5: Reservation Book

## The direction

The front desk as the hotel's own bound reservation book, opened flat on the desk. Every screen is a two-page spread of printed, ruled paper on navy book cloth.

- **The spread.** The left page carries the day and date as its running head. The right page carries the section. Page numbers sit at the foot, with the check-in and check-out times printed beside them.
- **The margin.** A plum double margin rule runs down the outer edge of each page. The margin column works like a ledger's. On the left page it holds times, dates, field labels and room numbers. On the right page it holds amounts, so every total lines up like a money column.
- **The ruled lines.** Pale-blue rules every 36 px. Every block (a row, a heading, a form field, the committing button) is a whole number of lines tall, so content sits on the rules instead of floating over them. Form fields are underlines written on a rule, not boxes.
- **The ribbon.** A plum ribbon bookmark hangs over the top edge to mark today. On Availability it hangs over the tonight column.
- **Thumb-index tabs.** The navigation is a stack of tabs cut into the right fore-edge: Today, Availability, Bookings, then (after an "Admin" divider) Rooms, Codes and Staff. The active tab turns page-white and joins the page. On receptionist screens the admin tabs are shown locked, with a dashed outline and a lock, so the limit is visible rather than hidden.
- **The gutter.** A soft shadow shades both pages into the spine. A single sheet peeks out behind each page's outer edge to give the book some thickness.

It stays crisp and printed: no handwriting fonts, stains, torn edges or leather. The pages are white, never cream.

## Tokens

### Colour

| Token | Hex | Role |
|---|---|---|
| `--cloth` | `#1F2A44` | Cover cloth: the page ground, with a low-contrast weave |
| `--board` | `#19223A` | Cover board showing 10 px around the pages |
| `--paper` | `#FFFFFF` | Right-hand page |
| `--paper-2` | `#FBFCFE` | Left-hand page |
| `--rule` | `#CFDCF0` | Ruled lines and table rules |
| `--rule-2` | `#A9BBDA` | Header double rule, swatch and tag edges |
| `--plum` | `#BB22AA` | Margin rule, ribbon, "arriving", selection and the one primary action. White on plum is 5.4:1 |
| `--plum-wash` | `#FAEEF8` | Selected row or field in progress |
| `--ink` | `#1B2340` | Text, the in-house dot, filled bars, sum rules |
| `--ink-2` | `#353F62` | Secondary text |
| `--ink-3` | `#56607F` | Lowest text tone: 6.0:1 on the page |
| `--control` | `#7D8BAE` | Control borders and field underlines (3.4:1) |
| `--fill` | `#EEF2F9` | Disabled controls and "full" cells |
| `--ok` | `#1D6B45` | "Valid", "Settled", "Name matches" (always with an icon and a word) |
| `--err` | `#B3261E` | Destructive action and field errors |
| `--cloth-ink` / `--cloth-muted` | `#EEF2FA` / `#AEB8D0` | Text on the cloth (muted is 7.2:1) |

### Type

- **Petrona** (variable serif, 100–900, roman and italic) for page titles (31 px), section headings (20 px), dates, room numbers and big numerals such as totals. The italic is used once per spread, for the running-head date. Google's Petrona has no optical-size axis, so optical sizing is done by hand: tighter tracking and heavier weight at display sizes, and a plainer weight in data.
- **Figtree** (300–900) for all UI text, labels and figures. Body is 14 px. Labels, running heads, tab labels and status codes are uppercase with 0.1–0.16 em tracking. Nothing is set below 11 px.
- **Sometype Mono** only for codes: booking refs (`HVK-2094`), promo codes (`autumn26`) and code IDs (`PRM-0014`).
- Tabular, lining figures throughout data (`font-feature-settings: "tnum", "lnum"`).
- All three fonts are self-hosted as latin `woff2` files in `assets/fonts/`, with their OFL licences. The `→` glyph is outside the latin subset, so date ranges use a drawn arrow icon.

### Spacing, rhythm and radius

- `--r: 36px` is one ruled line: the vertical unit for everything.
- `--m: 84px` is the margin column. `--mg: 20px` is the gap that holds the margin rule. `--in: 30px` is the padding at the spine.
- The running head is 2 lines tall and closes with a 3 px double rule. The foot is 56 px.
- Radius is 3 px on controls and 5 px on the page corners. Paper is square, so nothing is pill-shaped.
- Shadows always have an offset and a blur: on the cover board, the pages, the tabs and the ribbon.

## Components

- **Ledger line (`.ln`)**: a grid row one rule tall, with a margin cell (`.m`) and a text cell (`.c`). `x2` and `x3` make it 2 or 3 lines tall; `mid` centres controls; `wash` highlights a line in plum wash without covering its rule.
- **Title and section heading**: the title takes 2 lines and sits on the second rule. Section headings take one line after a blank line, so there is more space above a heading than below it.
- **Field (`.fld`)**: an underline that lands exactly on the rule. Its states are focus (a 2 px plum underline over a faint wash), read-only (a dotted underline), error (a 2 px red underline plus `.fld-err` text) and disabled.
- **Buttons**: the primary is a plum bar exactly one ruled line tall. There is one per screen. Secondary buttons are 28 px outlined. Quiet buttons are underlined text. Disabled buttons are dashed, on the fill colour. Pressed or expanded buttons (Rebook) turn solid ink. Destructive buttons use red text and a red outline.
- **Checkbox, radio, segmented choice and stepper**: plum when checked, dashed when disabled.
- **House chart (`.house`)**: a ruled 8×8 table. Each room cell is two lines tall. Occupied cells are opaque, as if written in. Vacant cells stay transparent so the ruling shows through. Out-of-order cells are cross-hatched. On Check in the same cells become radio choices.
- **Money**: a dotted leader runs from the item to its amount. The amount sits in the right-hand margin or at the end of the line. A subtotal gets an ink rule on top, and the total gets a double rule underneath.
- **Stamp**: a double-bordered plum date stamp that previews the check-in outcome ("Checked in · 27 Sep 2026 · 10:46 · NR").
- **Role card**: a ruled card of "can" and "can't" lines, selected by radio. It is the only card in the design, because the brief names it.

## Status without colour

Every status has a distinct shape and always has its code or word beside it.

| Status | Mark | Code / word |
|---|---|---|
| Arriving | plum hollow ring | ARR, arriving |
| In house | filled ink dot | OCC, in house |
| Due out | ink ring with a tick | DUE, due out |
| Vacant | empty ruled cell (no mark) | VC, ready |
| Out of order | cross-hatched cell | OOO, back date |
| Reserved / scheduled / invited | hollow ink ring | the word |
| Used up | half-filled ring | Used up |
| Expired / deactivated | ring with a slash | the word, plus a strike-through on the name or code |

In the availability chart, "in house" is a solid ink bar, "reserved" an outlined bar, "arriving" a plum-outlined bar with the ring, and "out of order" a hatched bar with the words. A full night reads **FULL** on a grey fill. The selected nights are boxed with a 2 px plum outline and listed in words in the heading.

## Permissions, where they matter

- Receptionist screens show the Rooms, Codes and Staff tabs locked and dashed, marked "admin only".
- The promo-code field says: "Codes are created by admins. You can apply a code, not create one."
- On Rooms, Delete is disabled with a lock, and the reason is written beside it. Family Suite shows "Has 14 upcoming bookings and 7 rooms occupied tonight".
- The role cards on Staff list what each role can and can't do.
- Check in on a future booking is disabled with the reason "Check-in opens on the arrival day, Thu 1 Oct".

## Responsive

- **At 1240 px and below**, the pages stack: left page, then right page. The right page's margin moves to the left and the spine shading drops.
- **At 760 px and below**, the tabs turn into a row of tabs along the top edge, the margin column narrows to 54 px, and dense grids (the house chart, availability) scroll sideways inside the page.

## Open decisions

1. **Offer on promo codes.** The brief defines a code as id, code, title, a required date range and an optional count. It never says what the code gives. The "Offer" field ("15% off room nights") is a placeholder for the client to confirm.
2. **Placeholders, not spec.** The 12% tax, the extras prices (breakfast $18 and dinner $42 per guest per night, pickup $55 per trip), the room prices and the name "Alder House" are all placeholders.
3. **The find field.** The top margin carries "Find a guest, booking ref or room" as a way to reach a booking. Search scope and behaviour are not in the brief.
4. **Page numbers.** The folios (540–557) are printed decoration. They could instead carry something real, such as the day of the year.
5. **Initials as signatures.** Staff are listed with the initials they sign entries with, as on the check-in stamp ("NR"). The real sign-off format is to be confirmed.
6. **Check-out of the four early rooms.** 303 and 608 are shown as vacant, and 402 and 507 as re-let to today's arrivals (Novak, Park), as the content spec states.
