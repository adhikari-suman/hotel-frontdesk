# Design 7: Mirror

Alder House front desk, 9 screens. Static HTML and CSS, no scripts, no network requests. All data is synthetic and comes from the shared content spec.

## The direction in plain words

The app is laid out like the lobby of a grand old hotel: everything is arranged symmetrically around a central axis, and that axis is drawn on every page as a thin double vertical rule.

- The wordmark "Alder House" sits on the axis at the top. The front desk items (Today, Availability, Bookings) are on its left. The admin items (Rooms, Promo codes, Users) are on its right. Both groups are the same width. The signed-in person is at the far left end and the clock is at the far right end.
- Each page title is centred on the axis and framed by double hairlines.
- The one primary action on every screen also sits on the axis.
- Pink and green face each other across the axis:
  - The left face is green: arrivals, the front desk, the receptionist, check-in.
  - The right face is pink: departures, admin, check-out.
- Anything built on the axis has an arched top, like a lobby archway: the house on Today, the folio on New booking, the room on Check in and Check out, the tonight panel on Availability, and the floor map on Rooms.
- Readability rule: placement is mirrored, reading direction never is. Text inside rows always reads left to right, and time always runs left to right.

### Signature moves, screen by screen

| Screen | What it shows |
|---|---|
| 01 Today | Arrivals (green field) on the left and departures (pink field) on the right. The departures side also sums the balances still to settle ($1,807.74 across 3 rooms), notes the 12:00 late check-out, and shows the 4 rooms checked out this morning with their new status (303 and 608 VC, 402 and 507 re-let as ARR). The 8 × 8 house sits under an arch on the axis, split between rooms n04 and n05. "53 of 64 tonight" and **New booking** are beneath it. The rows are mirrored: the room tile is on the outer edge and the button faces the axis on both sides. |
| 02 Availability | Centred on tonight. An arch lists the 9 rooms free tonight, by type, in two mirrored halves. Below it are 16 nights per type with a double-ruled tonight column, a selection band with **Start booking** on the axis, and the Family Suite room-by-room chart on the same column grid. |
| 03 New booking | Stay and room on the left, guest, extras and promo on the right. The folio for 807 is under an arch on the axis, ending in **Confirm booking**. |
| 04 Booking and rebook | The current stay (struck through, pink) and the new stay (green, focused) face each other across the axis. The 7-night Deluxe strip is centred, so Fri 9 sits on the axis. Then come the difference, **Confirm rebook**, and the booking details below. |
| 05 Check in | Guest and ID in the green face on the left. Room 704 on the axis, with the Deluxe floors 6–7 as a mini house to pick from, the ARR → OCC outcome, the stamp and **Complete check-in**. Payment and keys are on the right. |
| 06 Check out | The mirror image of check-in: payment and checks on the left, 505 on the axis with the Twin Double floors 4–5, DUE → VC and **Settle $489.14 and check out**. The guest and folio are in the pink face on the right. |
| 07 Rooms | Room types ledger. Deluxe is edited in place and **Save changes** sits on the axis. Family Suite delete is blocked with the reason. Recent changes, the floor map (arch) and out-of-order rooms are below. |
| 08 Promo codes | The new-code form on the left faces its reflection on the right: what receptionists will see, plus the overlap with `winter26`. **Create promo code** is on the axis, and all codes are listed below. |
| 09 Users | Create-user fields, then the two roles as a diptych: Receptionist (green, selected) and Admin (pink). Each lists what the role can and can't do. **Create user and send invite** is on the axis, and the team table is below. |

## Tokens

### Colour

| Token | Hex | Role |
|---|---|---|
| `--ground` | `#FCEEF8` | Page ground, the lobby floor. Also the in-house (OCC) fill |
| `--ground-2` | `#F6DFF0` | Second neutral layer: table heads, read-only fields, selected segment |
| `--leaf` | `#FFFFFF` | Forms, lists, arches. Also the vacant (VC) fill |
| `--green` | `#AAEEAA` | Arriving (ARR), selected room type, selected nights, receptionist role |
| `--green-2` | `#D9F7D9` | The green face (arrivals, check-in guest), reserved bars, the tonight column |
| `--pink` | `#FFAAFF` | Due out (DUE), admin active nav, admin role, valid promo result |
| `--pink-2` | `#FFD6FB` | The pink face (departures, check-out guest), chosen extras, the row being edited |
| `--ink` | `#2A1231` | Aubergine. All text, borders, and the primary button (white text, 17:1) |
| `--ink-2` | `#5A3A62` | Secondary text. At least 5.6:1 on every fill above |
| `--alert` | `#8A0F3E` | Blocks, warnings, required marks. At least 5.6:1 on every fill |
| `--hatch` | aubergine 135° hatch on ground | Out of order (OOO), full nights, expired codes |

There is no gold, no metallic and no gradient. Selection highlight is pink, and scrollbars are aubergine on `--ground-2`.

### Type

- **Bodoni Moda** (variable, optical size on): page titles (46 px), panel headings (25 / 19 px), and all figures that matter: room numbers, ETAs, money totals, counts and the clock. Always lining, tabular figures.
- **Red Hat Text** (variable, 300–700): all UI. Body 14 px, labels 12.5 px, nothing below 11 px.
- **Red Hat Mono**: status codes (ARR, DUE, OCC, VC, OOO, RES), promo codes, booking references, IDs and emails in tables.
- The fonts are self-hosted as latin-subset woff2 in `assets/fonts/`, with the OFL texts alongside.

### Space, radius and rules

- **Spacing:** 4-based scale (4, 8, 12, 16, 24, 32, 48, 64). Page gutter 24 px, column gutter 32 px, axis gutter 56 px.
- **Grid:** symmetric 12 columns, used as thirds (4 | 4 | 4) or halves (6 | 6).
- **Radius:**
  - 4 px for fields, leaves and tiles.
  - Full pill for buttons and chips, so they have symmetric ends.
  - Arch tops are `50% / 96px` elliptical.
- **Rules:**
  - Hairlines are 1 px aubergine at 14–30%.
  - Ornamental and structural rules are `3px double`: two 1 px lines with a 1 px gap. This covers title wings, the axis, arches and total lines.

## Components

- **Top bar:** grid `1fr auto 1fr`, so the wordmark lands exactly on the axis.
  - Nav items have equal widths. Front desk icons sit on the outer left and admin icons on the outer right.
  - The active item is a pill: green for front desk, pink for admin.
  - For receptionists, the admin items are shown locked, with a dashed outline, a lock icon and "admins only" in the accessible name.
- **Title:** Bodoni h1 on the axis with double-rule wings, and an italic Bodoni subtitle below it. There are no eyebrow labels.
- **Panel heading:** centred on the panel's own axis with small double-rule wings.
- **Faces:** `.fg` is the green field and `.fp` is the pink field. Both have a 1 px aubergine border.
- **Arch:** a white leaf with a `3px double` aubergine border and an arched top, for anything on the axis.
- **Room tile / house cell:** the number in Bodoni, the code in Red Hat Mono, and the fill by status.
- **Queue row:** `[tile][details][button]` for arrivals and `[button][details][tile]` for departures. The details are always left-aligned.
- **Buttons:**
  - Primary: aubergine pill, 52 px, one per screen, on the axis.
  - Secondary: white pill with an aubergine outline.
  - Quiet: underlined text.
  - Pressed: green fill.
  - Disabled: dashed outline with `--ink-2` text.
  - Alert: raspberry outline.
- **Fields:**
  - Default: white with a 55% aubergine border.
  - Focus: 2 px aubergine ring with a 2 px offset (shown on New stay in 04 and the code field in 08).
  - Changed: pink field with a 1.5 px border and "Changed · was $238" (07).
  - Read-only: dashed, `--ground-2`.
  - Error: 1.5 px raspberry border plus a message.
- **Controls:** segmented control, stepper, drawn checkbox and radio, and option rows (the selected one is green).
- **Notes:** icon plus text, optionally boxed. Warnings are raspberry-outlined on pink. Blocks are dashed raspberry. There are no side stripes.
- **Stamp and seal:** a double-ruled pill for the check-in stamp (05) and the balance due (06).
- **Availability grid and room chart:** they share one CSS grid template, so the chart's night columns line up under the matrix. Stays are pill bars. A stay that started before tonight has a flat, dashed left edge.

## How status is encoded without colour alone

Every status carries its three-letter code in Red Hat Mono, as well as a distinct fill or outline:

| Status | Code | Fill | Extra cue |
|---|---|---|---|
| Arriving | ARR | green `#AAEEAA` | 1 px aubergine border |
| Due out | DUE | pink `#FFAAFF` | 1 px aubergine border. Late check-out adds a clock tag "Late check-out 12:00" |
| In house | OCC | ground tint | Heavier 1.5 px aubergine outline |
| Vacant | VC | white | Lighter 55% outline |
| Out of order | OOO | aubergine hatch | Code on a ground patch so it stays legible |
| Reserved (charts) | RES | pale green | Pill bar with the guest name |

Other status cues:

- **Full nights:** hatch plus the figure 0 plus the word "full".
- **Selection:** green plus a heavier outline. Tonight has a double-ruled column frame and the header reads "Tonight".
- **Promo status:** always spelled out with an icon: Active (check), Scheduled (clock, dashed), Used up (ban), Expired (hatch).
- **Roles:** tags carry both the word and an icon.
- **Locked and disabled:** a dashed outline and a lock icon.
- **Balances:** "Settled" with a check, or the amount followed by "due".

## Open decisions

1. **Promo "Offer" field (08).** The brief defines a promo code as id, code, title, date range and optional count. It does not say what the code gives. The "Offer" field (for example "10% off room nights", "7th night free") is a placeholder that needs a product decision.
2. **Placeholder figures.** The 12% tax, the extras prices (breakfast $18, dinner $42, pickup $55) and the room prices are demo values.
3. **Delete rules for room types.** Every type currently has upcoming bookings, so Delete is disabled on all four. Family Suite shows the full reason. We still need to decide whether delete is ever allowed with future bookings (for example, by moving them).
4. **Mirroring on narrow screens.** At 390 px the axis collapses into one column: the centre element first, then the green face, then the pink face. The symmetry becomes an order rather than a layout.
5. **Hotel name and brand.** "Alder House" is a placeholder wordmark.
