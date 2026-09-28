# Design 11 — Warp & Weft

**Idea.** The hotel read as cloth on a loom. Floors and room types are warp threads, nights are weft, and every stay is woven into the grid. Status is shown by **weave pattern** (plain, twill, dotted, striped, basket hatch) plus a glyph and a word, so it never relies on colour alone.

Open `index.html` for the gallery. The screens are in `screens/` and the @2x screenshots in `png/`.

## Tokens

| Token | Hex | Meaning |
|---|---|---|
| `--indigo` | `#1C2B49` | Text, primary action, the selvedge rail, in-house rooms (twill) |
| `--indigo-2` | `#2E4170` | Twill stripe, hover |
| `--indigo-wash` | `#DDE2EC` | Selected rows and cards |
| `--cotton` | `#E7E9E1` | Page ground, with a fine plain-weave texture |
| `--card` | `#FAFAF6` | Surfaces |
| `--celadon` / `--celadon-deep` | `#9BBFA0` / `#3F6E4A` | Free, OK, applied code |
| `--weld` | `#D1A53A` | Arriving, attention, the current step, selected range |
| `--walnut` | `#5A4632` | Departing |
| `--madder` | `#B9412E` | Destructive actions, out of order, admin-area notices |
| `--thread` / `--thread-2` | `#D3D3C7` / `#BDBEB0` | Rules, borders |
| `--muted` | `#5E6472` | Secondary text (AA on card) |

## Room status patterns

| Status | Pattern | Glyph and word |
|---|---|---|
| Free | Plain white, celadon border | ✓ Clean / Inspect |
| In house | Indigo twill (diagonal) | "Stay-over" |
| Arriving | Weld dots, dashed border | → guest surname |
| Departing | Walnut vertical stripes | ⇥ guest surname |
| Out of order | Madder basket crosshatch | ✕ reason |

## Type

- **Besley** (500/700/800, 500 italic) for headings, names and type labels. A Clarendon slab that reads like a woven label.
- **Hanken Grotesk** (400–700) for interface text, 11–16px.
- **Spline Sans Mono** (400–600) for room numbers, money, booking refs and codes.

All three are self-hosted in `assets/fonts/`, with their OFL licences.

## Layout

- **Selvedge rail.** An 84px indigo rail on the left with a zig-zag stitched edge. Desk items sit on top. Admin items (Rooms, Promo codes, Staff) sit below a dashed stitch line and show a lock for receptionists.
- **Pattern-draft header.** Breadcrumb, date and shift, search, and the signed-in user with a role badge (Receptionist in celadon, Admin in madder with a shield).
- **16-column grid.** It matches the 16 rooms per floor, and the Today board uses it directly.
- **Shuttle trays.** Working panels such as Rebook rise from the bottom as indigo-headed trays instead of opening in a right-hand drawer.

## Signature components

- **Room board (01).** 4 floor rows × 16 woven tiles under room-type warp bands.
- **Thread gauge (02).** Each availability cell draws one thread per room: light for free, dark for booked, hatched for out of order. The selected range is a weld band, and a shuttle bar summarises it.
- **Stitched primary button.** Indigo with an inner running stitch. There is one per screen.
- **Knot progress (05).** Diamond knots on a thread: solid when done, weld for the current step.
- **Pinked folio (03, 06).** A receipt with a pinking-shear bottom edge.
- **Woven code label (08).** Preview of a new promo code as a sewn-in tag.
- **History thread (04, 09).** A dashed thread with diamond knots.

## Rules

- Status always has a pattern, a glyph and a word. Colour alone never carries meaning.
- One stitched primary per screen. Destructive actions are madder: outlined for the entry point, filled for the final confirmation, and always with a ✕ or bin icon.
- A delete that is blocked shows a dashed, greyed icon with a tooltip that explains why (Rooms).
- Permissions are always visible:
  - rail locks for receptionists;
  - an "Admin area" band on admin screens;
  - "Apply only. Codes are created by admins." wherever a code is applied;
  - a role matrix on Staff.
- Minimum text size is 11px. Money, room numbers and references use tabular mono.

## Open decisions and placeholders

- **Promo offer is undefined.** "15% off room nights" on summer2026 is a placeholder. The other codes show "Offer not set".
- **summer2026 and the hero stay.** summer2026 runs 1 Jun–30 Sep 2026, but the hero stay is 14–17 Oct. This design assumes the date range is checked against the date the booking was made (28 Sep). Decide whether the range applies to the booking date or the stay dates.
- **Tax** is a placeholder of 12%, applied to the subtotal after the discount.
- **Hero totals.**
  - New booking: $714.00 − $107.10 + $108.00 + $55.00 = $769.90, plus tax $92.39, total $862.29.
  - Check-out adds dinner for 2 on 15 Oct (the upsell taken at check-in): total $956.37.
- **Check-out date.** The check-out screen is dated Sat 17 Oct (the hero booking's departure). The other screens use Wed 14 Oct.
- **Invented values.** These are not in the brief:
  - cancellation terms (first night charged for a same-day arrival; pickup refundable more than 3 hours before landing);
  - the $100 incidentals hold;
  - key-card count;
  - departing guests' names and their balances;
  - future-booking counts per room type.
- **Admin desk rights.** Whether admins can also do desk tasks is assumed "yes" in the role matrix.
- **Room map.** The room-number-to-type layout is a proposal: per floor, 01–06 Queen, 07–10 Twin Double, 11–14 Deluxe, 15–16 Family Suite.
