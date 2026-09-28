# Design 6 — Mountain & Valley

**Idea:** the front desk as folded paper. Every room is a square sheet and its fold shows its state. Screens are tri-fold sheets divided by dashed valley creases. Rebook, edit and create panels fold over from the right as a "flap", and navigation is a row of folder tabs folded out of the top edge of the sheet.

Open `index.html` for the gallery. The screens are in `screens/`, and the @2x screenshots are in `png/`.

## Layout and navigation
- **No sidebar and no top nav.** The top is one 48px line: hotel mark, date/time, search and the signed-in person with their role.
- **Sheet tabs:** the nav tabs are dog-eared paper tabs that stick out of the top edge of the content sheet, just under the page title. The *Desk* tabs sit on the left. The *Admin office* tabs sit behind a dashed fold line on the right. When a receptionist is signed in, the admin tabs are hatched and marked "Admins only" with a lock. The active tab is white, merges into the sheet and has a rose top edge.
- **Tri-fold content:** one `.fold` sheet with 2–3 `.panel`s. A mountain panel is flat white. A valley panel has shading at the crease. A `.flap` (pale rose, shadow on the fold edge) holds the side task: rebook, edit room type, create code, create user.
- Content is left-aligned. Each screen has one rose primary button, and it carries the clipped "folded corner".

## Tokens
| Token | Hex | Meaning |
|---|---|---|
| paper | `#F3F5F1` | page ground (cool, not cream) |
| sheet | `#FFFFFF` | panels, inputs, free rooms |
| ink | `#14212B` | text, dock; `#243441` for occupied rooms |
| crease | `#AFCBC4` / `#7FA59B` | fold lines, "plenty free" |
| rose kami | `#B4486F` | the one primary action, current selection, admin markers |
| sea kami | `#0B6E77` | arrivals, verified/done, discounts |
| slate | `#4F5E6B` | departures, settled, expired |
| persimmon | `#D7400F` | destructive actions, out of order, full, exhausted |

Colour is never the only signal. Room tiles carry a letter (S/A/D/V/X) and a distinct shape: fully folded, top-right dog-ear, bottom-right dog-ear, flat, or hatched cut. Tags always contain text, and locks carry an icon plus words.

## Type
- **Syne** 600/700/800: headings and panel titles only. Its wide geometric M and W stand for the mountain and valley folds. It is not used for numbers, because its figures are too quirky for money.
- **Bricolage Grotesque** 400–700: all UI text and all numerals (tabular). Body text is 13.5px, labels 12–12.5px, and nothing is smaller than 11px.
- Both fonts are self-hosted in `assets/fonts/` (woff2 from Fontsource) and include their OFL licences.

## Components
- **Room tile** (`.room.occ|arr|dep|vac|ooo`): a folded square with number, type abbreviation and state letter.
- **Fold step** (`.step` with `.done` / `.cur`): numbered markers, used only for real sequences (new booking, check-in, check-out).
- **Flap panel** (`.flap`, `.flap-tab`): the side task, marked with an "Open · not saved" or "Unsaved changes" tab.
- **Danger zone** (`.danger-zone`): persimmon outline with a folded corner. It holds cancel booking and delete room. Blocked deletes are shown as disabled buttons with a lock and a reason.
- **Totals / folio** (`.lines`, `.total`, `.bal`): the balance to settle sits on an ink slip with a clipped corner.
- **Ticket preview** (`.ticket`): shows a promo code as staff will see it.
- Icons are hand-made 24px line icons with square caps and mitred joins, inlined as SVG.

## Rules
- One primary (rose, clipped-corner) action per screen. Destructive actions are persimmon-outlined, or solid persimmon only at the final confirm.
- Numbered markers appear only on sequences.
- Permissions are always visible. Admin screens show an "Admin only" tag, and receptionist screens show locked admin tabs and a note: "New codes are created by admins in Promo codes".

## Data notes and open decisions
- **Promo "offer" is a placeholder.** The brief doesn't define the offer type. summer2026 is shown as 15% off room nights, and the new code as 10%.
- **summer2026 vs. the hero dates:** the code ran 1 Jun–30 Sep, but the stay is 14–17 Oct. I read the date range as the *booking* window and show the code as honoured from a quote made on 29 Sep. This needs a product decision: does the date range apply to the booking date or the stay dates?
- **Tax** 12% is a placeholder, charged on the subtotal after the discount.
- **Cancellation terms** (free until 48h before arrival, then first night plus tax) are invented for illustration.
- **Rebook** is shown as a proposal (15→19 Oct, +$266.89) that is not saved. Screens 05 and 06 keep the original 14→17 Oct stay. Dinner for 2 on 15 Oct is added at check-in, so the check-out folio is $956.37.
- **Check-out** is dated Sat 17 Oct, the hero's departure day. All other screens are dated Wed 14 Oct.
- Board states for tonight: 32 staying over + 9 arrivals = 41 occupied, 7 departures, 2 out of order (208, 407), 14 vacant. Room numbering: Queen 101–112 & 201–212, Twin 113–116, 213–216 & 301–308, Deluxe 309–316 & 401–408, Family Suite 409–416.
- Departing guests beyond the canonical ten names (Noor Haddad, Liam O'Connell, Greta Sørensen, Yusuf Demir, Clara Jansen, Inês Duarte) and new user "Lena Hartmann" are extra synthetic names.
- Admins are shown with full desk access. The brief doesn't say whether admins also work the desk.
- Room-type "Sleeps" values, room descriptions and upcoming-booking counts are illustrative.
