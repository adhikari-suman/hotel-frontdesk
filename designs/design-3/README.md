# Design 3: Pool Lanes

A 1960s motor-lodge-modern front desk for Alder House. It's light, like a sunny resort lobby, and it's architectural rather than kitsch.

The day moves down tall vertical **swim lanes** (arriving, in the house, leaving) instead of stacked horizontal tables. Ropes of marigold and white buoys divide the lanes. All 64 rooms appear as a **pool deck**: 8 rows of rounded tiles. A single **marigold "sun"** button marks the one committing action on each screen, and every heading is set in all-lowercase Jost.

- Gallery: `index.html`
- Screens: `screens/01-today.html` … `screens/09-users.html`
- PNGs: `png/` (1440 px, @2x, full page)
- Styles: `assets/lanes.css`, which holds the shared tokens and components. Each screen adds a small page `<style>` block and an inline Lucide icon sprite (ISC licence).
- Fonts: `assets/fonts/` (Jost and Azeret Mono, SIL OFL; licence in `assets/fonts/OFL.txt`). The pages make no network requests.

## How each screen uses the lanes

| Screen | Signature |
|---|---|
| 01 today | A deck map of all 64 rooms and the tonight tally sit above three lanes: **arriving 10** (pale water), **in the house 43** (deep water, grouped by day out) and **leaving 5** (edged in marigold). "new booking" is the marigold sun in the top bar. |
| 02 availability | The 4 room types are vertical lanes with the nights running down, each cell carrying a water-level bar. Tonight is a solid start line. Beside them, the 8 Family Suite rooms are swim lanes with booking capsules. The Fri 2 → Sun 4 selection is ringed, and **start booking** is the sun. |
| 03 new booking | The booking moves left to right through three lanes: stay → guest and extras → price and confirm. All 4 room types are shown, with the 3 that can't take the party disabled and a reason given. |
| 04 booking, rebook | Lanes for guest and stay, and for extras and charges, plus an open **rebook** lane. It shows Deluxe nights as vertical water tanks and the difference in large numerals. |
| 05 check in | Lanes run guest and ID → room (Deluxe floors 6–7 as tiles, only the ready rooms can be picked) → payment and keys. The last lane is deep water, because that's where the guest ends up: 704 drifts from ARR to OCC and gets its stamp. |
| 06 check out | A folio lane edged in marigold, then pay with, then before the guest leaves. The outcome shows 505 going from DUE to VC. |
| 07 rooms (admin) | One sage lane per room type holds the price, count, sleeps, tonight and upcoming figures, plus that type's floors as tiles. Deluxe is mid-edit ($238 → $248), and delete is blocked with the reason. |
| 08 promo codes (admin) | Codes sit in **active / scheduled / ended** sage lanes next to the new-code form, which includes an overlap warning and a preview of what receptionists will see. |
| 09 users (admin) | **Admins** and **receptionists** are lanes, and the new user appears as a ghost card in the receptionists lane. Role cards list what each role can and can't do. |

## Tokens

### Colour (roles)

| Token | Hex | Role |
|---|---|---|
| `--ground` | `#F2F7F3` | Page background: pool-deck white with a green tint, never cream |
| `--deck` | `#E3EDE6` | Second neutral layer: tracks, read-only fields, scrollbar track |
| `--white` | `#FFFFFF` | Wells, cards, vacant tiles |
| `--line` / `--line-strong` | `#C6D8CF` / `#8FB0A6` | Hairlines / input borders |
| `--water-pale` | `#BDF1DC` | Arriving lane, current nav item, selection fills |
| `--water` | `#77EEBB` | Arriving status (ARR), focus halo, text selection |
| `--water-deep` | `#2FB38A` | In-house status (OCC) and lane, level bars |
| `--ink` | `#0B3F3A` | All text, rules, focus ring, rope line |
| `--ink-deep` | `#062A26` | Text on deep water (5.8:1; `--ink` would only reach 4.4:1) |
| `--ink-2` | `#2F5E58` | Secondary text (≥5:1 on every surface except deep water) |
| `--ink-off` | `#466A64` | Disabled text (≥5:1 on wells) |
| `--marigold` | `#EEBB33` | The one primary action ("sun"), due-out edge, buoys |
| `--marigold-pale` | `#FBEFC8` | Warnings, changed fields, late check-out |
| `--sage` / `--sage-pale` | `#CCDDAA` / `#E6EDD5` | Admin lanes and permission notes; out of order (hatched) |
| `--error` | `#A3243B` | Destructive words and error states only |

Terracotta, cream and gold aren't used anywhere.

### Type

- **Jost** (variable, weights 100–900), self-hosted. It carries headings, body, labels and numbers.
  - Headings are always lowercase (`h1` 44 px, lane `h2` 23 px with the count at 34 px regular).
  - Body is sentence case at 15 px.
  - Scale in rem: 11 / 12 / 13 / 14 / 15 / 16 / 19 / 23 / 28 / 34 / 44 px.
  - Data uses `lining-nums tabular-nums`.
  - Status codes (ARR, OCC, DUE, VC, OOO) are Jost caps at 11 px, weight 600, tracking 0.14em.
- **Azeret Mono** covers booking refs (`HVK-2094`), promo codes (`AUTUMN26`) and IDs (`PRM-0014`), with a slashed zero so 0 and O can't be confused.

### Spacing, radius, depth, motion

- **Spacing:** 4 / 8 / 12 / 16 / 24 / 32 / 48 px. Lanes are 12 px apart, with an 18 px rope between them.
- **Radius:**
  - lanes 16 px ("pool tile" corners)
  - cards and wells 12 px
  - fields 10 px
  - tiles 8 px
  - buttons are pills
- **Depth:** soft offset shadows only (`0 1px 2px` plus `0 6px 14px -8px`). No hard offsets, glass or blur.
- **Motion:** 150–250 ms for UI feedback. The one authored moment is the **drift**: when a guest checks in or out, the card moves into the next lane and eases across the rope. It's a transform transition of 420 ms with an exponential ease-out (`.card[data-drift]` in the CSS). It's disabled under `prefers-reduced-motion`.

## Components

- **Lane.** A tall rounded column with a pool-tile grout texture, a floor line down its centre and a T-mark at the foot. Variants:
  - `--arr`: pale water
  - `--occ`: deep water
  - `--due`: white with a marigold edge all the way round
  - `--white`
  - `--pale`
  - `--sage` and `--sage-pale`: admin
- **Rope.** A column (or row) of alternating marigold and white buoys on a 1.5 px line. It turns horizontal when the lanes stack below 900 px.
- **Deck tile.** Room number plus status code. Each status has its own fill and edge; out of order adds a hatch.
- **Room-number block (`.rn`).** A large geometric numeral on the status fill, used in lane cards.
- **Card.** A lane "swimmer": number, guest and one secondary action.
- **Well.** A white panel on the water that holds a form or a ledger.
- **Buttons.**
  - `.btn`: ink outline pill
  - `.btn-quiet`
  - `.btn-danger`
  - disabled: dashed outline, muted text and a lock reason underneath
  - `.btn-sun`: the marigold primary with an ink disc; exactly one per screen
- **Fields.** Label above the input, plus these states:
  - focus: ink border with an aqua halo and a caret
  - changed: marigold-pale fill with a "was" value
  - valid
  - error
  - read-only: dashed on the deck colour
- **Choice cards.** Radio style, with disabled variants that explain why. **Switches** and **checkboxes** are drawn in the palette.
- **Ledger / folio.** Tabular numerals, a heavy rule above the total.
- **Notes.** `lock` (sage-pale, for permissions), `warn` (marigold-pale), `ok` and neutral. None uses a side stripe.
- **Browser surfaces.** Text selection is aqua. Scrollbars are deep water on the deck colour. The focus ring is ink, 2.5 px, with a 2 px offset.

## Status without colour alone

Each status always pairs a **code word** with a **distinct edge or pattern**, so it still reads in greyscale:

| Status | Code | Treatment |
|---|---|---|
| Arriving | `ARR` | Aqua fill (the arriving lane) |
| In house | `OCC` | Deep-water fill (the in-house lane) |
| Due out | `DUE` | White with a thick marigold edge |
| Vacant, ready | `VC` | White with a thin ink edge |
| Out of order | `OOO` | Sage with a diagonal hatch |
| Reserved (charts) | `RES` | White with a dashed edge |

Words back up the icons elsewhere too:

- Payment state reads "settled" (with a check) or "$212.40 due".
- A late check-out is a marigold-pale chip with a clock and the words.
- Promo state reads Active, Scheduled, Used up or Expired, each with its own icon.
- User status reads Active, Invited or Deactivated, with an icon and a solid, dashed or dimmed card.
- Full nights are hatched and say "FULL".

## Permissions shown where they matter

- **Receptionist promo field:** "Codes are created by admins."
- **Rooms:**
  - Deleting Family Suite is blocked: "14 upcoming bookings and 7 rooms occupied tonight".
  - The other types show their upcoming-bookings count as the lock reason.
  - An "Admins only" note is included.
- **Rebook screen:** check-in is disabled with "opens on arrival day, Thu 1 Oct".
- **Check-in:** rooms that aren't ready stay visible but are dimmed and can't be picked.
- **Users:** the role cards list what each role can and can't do.
- **Navigation:** the admin nav adds an "admin" group, and admins can still see the front-desk views.

## Open decisions

1. **The promo "Offer" field** (15% off room nights, 7th night free, 10%, 20%) isn't in the client brief. The form shows it so a code can do something. Whether codes carry an offer, and in what form, is still open.
2. **Placeholders, not spec:**
   - the 12% tax
   - the extras prices (breakfast $18 and dinner $42 per guest per night, pickup $55 per trip)
   - the room prices ($136 / $166 / $238 / $366)
3. **The in-house count is 43, not 48.** The direction sketch labelled the middle lane "in the house (48)", which is 43 staying plus 5 still due out. The lanes use the content's figure of 43 so that each room sits in exactly one lane; the 5 due-out rooms live in the leaving lane.
4. **Room count** is shown read-only: it follows from the rooms in each type, and "add room" is the way to change it. Whether admins can type a count directly is still open.
5. **Deleting a type:** only the Family Suite block message comes from the brief. Blocking deletion of the other types while they have upcoming bookings is this design's assumption.
6. **Drift motion** is specified only as CSS transitions. Moving the card between lanes needs app logic in the chosen framework.
7. **Hotel name and brand.** "alder house" is a placeholder wordmark.
