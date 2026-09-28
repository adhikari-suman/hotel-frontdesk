# Design 4: Noughts & Crosses

Nine desktop screens (1440 px) for the Alder House front desk, in static HTML and CSS. Open `index.html` for the gallery, or go to `png/` for the 2x captures.

```
design-4/
├── index.html              gallery, palette, type, marks, states, placeholder note
├── README.md               this file
├── assets/noughts.css      tokens and components (the design system)
├── assets/fonts/           Schibsted Grotesk (variable 400–900) and Fragment Mono, woff2, OFL
├── screens/                01-today … 09-users as HTML
└── png/                    the same nine as PNG, 1440 px wide at 2x, full page
```

## The direction in plain words

This is Swiss International Typographic Style on a strict three-module grid. The page is a white field with big flush-left black grotesk, and 1 px black rules separate the modules. There are no cards, pills, shadows or rounded corners.

- **Colour:** there is one colour, a lavender field. It marks what you have selected, the item you are on, and keyboard focus. Taupe is the second neutral. It fills disabled things, danger messages and the admin area.
- **Status:** room status is drawn as the marks of noughts and crosses. O is a free room and X is a taken one. Small arrows show who is arriving or leaving.
- **The house:** Today shows the whole hotel as an 8 × 8 board of these marks, one row per floor.

The scene is a bright office by day, so the design is light.

## Topology

- **No sidebar.** Every page uses the same 3-column grid: 48 px margins and 24 px gutters, so each module is 432 px wide at 1440. Content snaps to 1, 2 or 3 modules.
- **Top band:** three modules separated by vertical 1 px rules.
  1. The wordmark.
  2. The navigation as two vertical text lists: *Front desk* (Today, Availability, Bookings) and *Admin* (Rooms, Promo codes, Users).
  3. The date, a large clock and the signed-in user.
- **Page head:** a huge flush-left title (88 px) and a one-line lede fill modules 1–2. Module 3 holds the one commitment for the page, or stays empty for asymmetric white space.
- **Receptionist vs admin:**
  - On receptionist screens the Admin list stays visible but locked ("Admin, for admins only", with a lock on each item).
  - On admin screens the whole band turns taupe, so you always know you are in the admin area.

## Tokens

### Colour (no other hues)
| Token | Hex | Role |
|---|---|---|
| `--paper` | `#FFFFFF` | Page ground |
| `--ink` | `#0B0B0C` | Text, rules, marks, the primary button |
| `--lav` | `#CCBBFF` | Selection field, current item (nav, board cell, list row), focus field |
| `--taupe` | `#CCBBAA` | Disabled, danger, out-of-order cells, admin band |
| `--ink-2` | `#4A453F` | Secondary text: 9.5:1 on paper, 5.5:1 on lavender, 5.1:1 on taupe |
| `--taupe-tint` | `#EEE8E1` | Tonight column, read-only fields, cells that can't be picked |
| `--hair` | `#CFC6BB` | Row hairlines inside a module (module rules stay ink) |

Inside a lavender field, secondary text steps up to ink. The primary action is ink with white text, and there is exactly one per screen.

### Type
- **Schibsted Grotesk**, the variable 400–900 axis, for everything except codes.
  - Display: 88 px / 0.92, weight 700, −0.03em. Page names only.
  - Section heads: 24 px / 650. Sub-heads: 17 px / 600.
  - Body: 15 px. Labels: 13 px, regular weight, no caps or small caps.
  - Smallest text: 11 px, used for board cell details.
  - Big single figures, such as totals, the balance and the clock, are 44 px, weight 650 and proportional.
- **Fragment Mono** only for codes and references: `autumn26`, `HVK-2094`, `PRM-0014`.
- **Status codes** (VC, OCC, ARR, DUE, OOO) are set in the grotesk at weight 650. In Fragment Mono at 11 px, OOO reads as 000.
- **Tabular figures** are used only in data columns: board and room numbers, table amounts, ledgers and availability counts. This face also tabulates punctuation, so running text keeps proportional figures.

### Spacing, radius, depth
- Spacing is on a 4 px base: 4, 8, 12, 16, 24, 32, 48, 72, 104.
- Radius is **0** everywhere, including checkboxes and radios, which are squares.
- There are no shadows. Depth comes from rules and fields only.

## Status without colour

Every status carries a drawn mark, a text code and, in lists, words. Colour is never the carrier.

| Status | Mark (SVG strokes) | Code | Extra cue |
|---|---|---|---|
| Vacant, ready | O | VC | "Ready" |
| In house | X | OCC | surname, out date |
| Arriving today | O with an inward arrow | ARR | ETA |
| Due out today | X with an outward arrow | DUE | out time, balance, "Late check-out 12:00" |
| Out of order | slashed square | OOO | reason and return date; the cell is also taupe |

The same grammar carries through the whole set:

- **Tonight's mark rows on Rooms:** X is sold, O is free, and a slashed square is out of order.
- **Promo status:** O is active, O with an arrow is scheduled, X is used up, and X with an arrow is expired.
- **User status:** O is active, O with an arrow is invited, and a slashed square is deactivated.
- **Role cards:** O lists what a role *can* do and X what it *can't*, each under a written "Can" or "Can't" label.
- **Other signals:** selection shows as lavender plus a 2 px ink outline or a checked control. Tonight shows as an inverted black column head plus the word "Tonight".

## Components (all in `noughts.css`)

- **Frame:**
  - `.band` / `.bm`: the three-module top band.
  - `.nav`: the vertical text lists, with the current item as a lavender field.
  - `.head` / `.display` / `.lede`: the page head.
  - `.sec`: a module section opened by a 1 px ink rule.
- **Board:**
  - `.board` / `.cell` / `.fl`: the noughts-and-crosses board. Rules sit only between cells, like the game grid.
  - `.strip`: one floor of cells, reused for picking a room on New booking and Check in.
- **Marks:** `.mk`, drawn from the `#m-o`, `#m-x`, `#m-arr`, `#m-due` and `#m-ooo` symbols embedded in each page.
- **Lists and choices:**
  - `.q` / `.q-row`: the arrivals and departures lists.
  - `.choices` / `.choice`: a list of options. The chosen row is a lavender field; rows that can't be chosen are taupe-tint with the reason in words.
- **Money:** `.ledger` for totals, and `.tbl` for tables (ink rule under the head, hairlines between rows).
- **Buttons:**
  - `.btn`: 1 px ink border. Hover and pressed turn it lavender; disabled is taupe-tint.
  - `.btn-primary`: ink with white text.
  - `.btn-text` / `.link`: underlined text actions.
- **Forms:**
  - `.input`: 1 px ink border, lavender field plus a 2 px ink outline on focus, taupe-tint when read-only.
  - `.err`: black on taupe, with a drawn X and words.
  - `.ck` / `.rd`: square checkboxes and radios.
- **Notes:**
  - `.note`: a bordered notice.
  - `.note.is-danger`: black on taupe, with a drawn X and words (for example, Delete blocked on Rooms).
  - `.perm`: a permission line with a lock.
- **Other:**
  - `.stamp`: the ruled line that shows how the booking will read after check-in.
  - `.outcome`: one mark turning into another (ARR → OCC, DUE → VC).
- **Browser surfaces:** text selection is lavender, and scrollbars are square ink on paper. Focus shows as an ink outline with a lavender field.

## Where permissions show

- **Receptionist band:** the Admin list is visible, but each item is locked.
- **New booking:** "Codes are created by admins. You can apply a code, not create one."
- **Rooms:** Delete is off on every type that has bookings. On Family Suite the danger note explains why: "14 upcoming bookings and 7 rooms occupied tonight". Beside the table, "Who can change rooms" lists the admins by name.
- **Promo codes:** the lede says who applies codes and who creates them. The form previews what a receptionist will see.
- **Users:** the role cards list what each role can and can't do.

## Responsive

- **At 1180:** the grid keeps three modules and the board cells shrink.
- **Below 1000:** the grid collapses to one column, the band stacks, and the board and wide tables scroll sideways.
- **At 390:** the display type drops to 56 px, and the margins become 16 px.

## Open decisions

1. **Promo "Offer" field.** The brief gives a code an id, code, title, date range and optional count, but no discount. These designs add an **Offer** (for example, "15% off room nights" or "7th night free") because a code needs a value. The discount model needs confirming.
2. **Placeholders, not spec:**
   - The 12% tax.
   - The extras prices: breakfast $18 and dinner $42 per guest per night, arrival pickup $55 per trip.
   - The room prices.
3. **Overlapping codes.** The form warns that `newyear27` overlaps `winter26` and that a booking can use only one code. Whether overlaps should be allowed at all is a policy call.
4. **Price changes.** On Rooms, existing bookings keep their price and only new bookings use the new price. This follows the content brief and needs product sign-off.
5. **Bookings list.** "Bookings" in the nav opens a booking record. A search or list view is not part of this set.
6. **Payment.** Pre-authorisation and card-on-file appear only as outcomes. Payment processing is out of scope.

## Synthetic data

All names, rooms, prices, phone numbers (555), emails (`example.com`, `alderhouse.example`) and references are invented for the demo. "Alder House" is a placeholder name.
