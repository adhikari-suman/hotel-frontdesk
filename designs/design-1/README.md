# Design 1 · The Rack

Nine desktop screens (1440 px) for the hotel front-desk web app. They cover both roles: Receptionist and Admin. Everything is static HTML/CSS, and each screen is also exported as a PNG at 2x.

Open **`index.html`** for the gallery, or go straight to `png/`.

```
design-1/
├── index.html            gallery of this design's 9 screens + system summary
├── png/                  the 9 screens as PNG @2x (2880 px wide)
├── screens/              the 9 screens as HTML (open in a browser; no network needed)
└── assets/               frontdesk.css (tokens + components) and fonts/ (self-hosted Archivo, JetBrains Mono, OFL)
```

## Screens

| # | Screen | Role | What it shows |
|---|--------|------|---------------|
| 01 | Today | Receptionist | Room rack: 64 rooms as slips, one row per floor. Arrivals and departures queue beside it with Check in / Check out |
| 02 | Availability | Receptionist | Rooms free per type × 16 nights, a room-by-room chart for one type, and range selection that leads to "Start booking" |
| 03 | New booking | Receptionist | Stay → room type → guest → extras → promo code, with a live reservation slip and totals |
| 04 | Booking detail + rebook | Receptionist | Registration card, extras (add/remove), promo, charges, history, cancellation terms; Rebook panel open |
| 05 | Check in | Receptionist | ID check, room from a mini rack (only ready rooms can be picked), payment guarantee, keys, dinner upsell |
| 06 | Check out + bill | Receptionist | Folio (room nights, promo, extras, tax, deposit), payment method, pre-departure checklist |
| 07 | Rooms | Admin | Room types with count, price, occupancy and upcoming bookings; inline edit; delete blocked while bookings exist; floor map |
| 08 | Promo codes | Admin | Code calendar, a printed code register (status, uses, ID), and a New code form: ID, code, title, required dates, optional limit |
| 09 | Users | Admin | Staff as a key-card board by role (active, invited, void), and a Create user form that lists what each role can and can't do |

## Design system in brief

**Idea:** the old front-office *room rack*. Every room is a coloured slip in a steel pocket, and every record reads like a printed registration card.

**Colour.** Status colours always come with the front-office code, so colour is never the only signal:

| Token | Hex | Meaning |
|---|---|---|
| `--peri` | `#5B5BD6` | **ARR** arriving today / reserved (pale: `--peri-slip`) |
| `--mustard` | `#AAAA22` | **DUE** due out today |
| `--rose` / `--rose-slip` | `#E66DAA` / `#F8D6E7` | **OCC** in house |
| `--mint` | `#66DAA2` | **VC** vacant and ready. Also "active" and "free" |
| `--hatch` | striped steel | **OOO** out of order |
| `--cobalt` | `#3366DD` | The single primary (commit) action on each screen, plus selection and focus |
| `--raspberry` | `#CC3366` | Destructive actions |
| `--ink` / `--ground` | `#1D1B2C` / `#E8E9EF` | Text and rail / page ground |

**Type.**
- **Archivo**, a variable font with a width axis:
  - `font-stretch: 62%` for room numbers and big figures
  - `75%` for the printed field labels (small caps)
  - `100%` for UI text
- **JetBrains Mono** is used *only* for codes: promo codes and booking references. Its `zero` feature is on, so 0 and O can't be confused.
- Minimum text size is 11px.

**Components** (all in `frontdesk.css`):
- `.pocket` + `.slip`: the rack
- `.sheet` + `.ruled` + `.pcode`: printed register with stamped status codes (promo codes)
- `.fg`: form grid, boxed cells sharing hairlines
- `.st`: status code chip
- `.tape`: embossed label tape for promo codes
- `.stamp`: rubber stamp shown on confirmation
- `.mslip`: mini slip used in lists
- `.tbl`, `.seg`, `.btn`, `.note`, `.panel`

**Rules the screens follow**
- Exactly one cobalt button per screen: the action that commits.
- All inventory is always shown. Rooms that are unavailable or can't be picked are ghosted, never hidden.
- Time views mark *now*: the tonight column is highlighted, and a TODAY line runs through the promo calendar.
- Permission limits are stated where they bite. Examples: "Codes are created by admins", the delete-blocked tooltip, the role cards on Create user.

## Synthetic data: replace before any real use

All data is invented. Replace the hotel name ("Alder House"), guest and staff names, phone numbers (555 numbers), emails (`example.com`, `alderhouse.example`), and booking references.

## Open product decisions (not in the brief)

1. **Promo discount.** The brief lists id, code, title, date range and count. The designs add an **Offer** field (e.g. "15% off room nights"), because a code needs a value. Confirm the discount model.
2. **Prices of extras.** Breakfast $18 per guest per night, dinner $42 per guest per night, and arrival pickup $55 per trip are placeholders.
3. **Tax.** A flat 12% is a placeholder.
4. **Room pricing.** Queen $136, Twin Double $166, Deluxe $238, Family Suite $366, with 24 / 16 / 16 / 8 rooms. All placeholders.
5. **Whether admins can also run front-desk actions.** The admin nav can *view* Today, Availability and Bookings. The brief doesn't say whether admins can book.
6. **One promo code per booking.** This is assumed in the overlap warning on the Promo codes screen.

Icons are from [Lucide](https://lucide.dev) (ISC licence), embedded as an inline SVG sprite. Fonts are self-hosted under the SIL Open Font License (see `assets/fonts/`).
