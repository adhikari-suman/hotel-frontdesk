# Design 10: Stamp Sheet

**Idea.** The hotel is a sheet of postage stamps. Each of the 64 rooms is a perforated stamp, 16 across and one row per floor. Room prices are engraved denominations, an out-of-order room carries a diagonal overprint, and a booking is a franked cover (an airmail-edged envelope) that carries its extras as small stamps. The date in the top strip is a circular postmark.

Open `index.html` for the gallery. The screens are in `screens/`, the @2x screenshots in `png/`.

## Where the direction came from
The seed string had no repeated three-letter runs and no palindromes, so every stamp in the sheet is a unique issue. In an otherwise choppy mix of upper and lower case there was a single long same-case run, which became the overprint. Its digits sum to a hue in the ultramarine range. Short digit runs set the other hues (carmine, gold, olive, bistre), all of them classic stamp-ink colours. The string was 16 × 16 characters long, which matches 16 rooms per floor.

## Tokens
| Token | Hex | Meaning |
|---|---|---|
| `--ultra` | #292DA3 | The one primary action per screen, in-house rooms, selection |
| `--ink` | #191A2E | Text, and the album-index nav rail |
| `--carmine` | #A92340 | Destructive actions, out of order, validation errors |
| `--olive` | #6E6819 | Vacant or free, discounts, success |
| `--gold` | #EDB21D (text #7A5500) | Arrivals, low availability, warnings |
| `--bistre` | #674C32 | Departures |
| `--page` | #F0F1F5 | Album-page background |
| `--sheet` | #C8CBD6 | Gutter behind stamp sheets, so the perforations show |
| `--perf` / `--rule` | #D9DBE2 / #E3E5EB | Borders and hairlines |
| tints | #E5E6FA, #FBE9ED, #F2F2DC, #FCEFCF, #F1E8DE | Status backgrounds |

## Type
- **Bodoni Moda** (600–700): room numbers, prices, totals and page titles. Not used below 15px.
- **Red Hat Text** (400–700, tabular figures): all UI text, tables and forms. Minimum 12px.
- The fonts are self-hosted in `assets/fonts/` (woff2 from fontsource), with the SIL OFL licences alongside.

## Layout and navigation
- **Franking strip** (64px, top): hotel mark, search, postmark date and shift, signed-in user and role badge.
- **Album index** (212px, right edge, dark ink): thumb-index tabs. The active tab joins the page. *Front desk* sits above a dashed lock line and *Admin only* below it. For receptionists the admin tabs are locked, and Promo codes reads "View only".
- **Content**: a left-aligned single canvas. Detail screens use a working column plus a 360–420px side column, which holds the booking cover, the rebook panel or the create form.

## Components
- **Room stamp** (`.stamp.room`): perforated with a CSS mask. Shows the number, the type letter (Q/T/D/F), a detail line and a status word. Hatching marks occupied and departing rooms, and out of order gets an overprint. Colour is never the only signal.
- **Denomination stamp** (`.denom`): room types and promo previews.
- **Cover** (`.cover`): a panel with an airmail edge, used for booking summaries and totals.
- **Postmark**: an SVG circle with the date and wavy cancel lines.
- **Status tag** (`.tag`): an icon plus a word.
- **Buttons**: primary (ultramarine, one per screen), default, ghost, danger (carmine outline), and danger-solid (only inside a delete confirmation).
- **Room tape**: room × night bars on the availability screen.
- **Validity timeline**: a Jun–Feb strip on promo codes, with a line for today.

## Rules
1. Each screen has one primary action.
2. Status always carries a word or glyph as well as colour.
3. Destructive actions are carmine and sit apart from other actions: cancel has its own box, and room deletion needs a confirm card. Deletion is blocked while a room has bookings.
4. Receptionists apply promo codes but never create them. The UI says so wherever a code appears.
5. Perforation is used only on stamps (rooms, types, extras, swatches). Other panels are plain.

## Open decisions and placeholders
- **The promo "offer" is undefined in the brief.** The screens show "15% off room nights" as a placeholder, and the create form says so.
- **The hero promo summer2026 expired on 30 Sep, but the stay starts 14 Oct.** This design assumes a code's date range applies to the booking date. The hero booking was made on 28 Sep (see the history on screen 04), so the code is still honoured. Screen 03 shows the same booking being entered and should be read as an illustration of the form. Whether ranges apply to the booking date or the stay dates needs a product decision.
- **Tax** is a 12% placeholder applied to everything, extras included.
- **Cancellation terms** are placeholders: free until 48 hours before arrival, then the first night after the promo plus tax. The pickup is refunded if cancelled before the trip.
- **The check-out screen is set on Sat 17 Oct** (its postmark changes) so that the hero's real departure day is shown. The folio adds one dinner for 2 (15 Oct) to show charges made during the stay.
- **Pre-authorisation** of stay + $100 incidentals, key-card encoding and ID capture are assumed desk workflows.
- **The rebook panel** keeps the original promo terms. That is a policy assumption.
- Guest names beyond the canonical ten (departing and in-house guests, bar labels) are synthetic filler.
