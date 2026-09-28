# Front desk: 10 designs

Ten different visual directions for the same single-hotel front-desk web app. Each one is a complete set of **9 desktop screens (1440 px)** built from identical content and data, so you compare the design, not the content.

Open **`index.html`** to compare all ten on one page.

| # | Direction | In one line |
|---|---|---|
| 1 | **The Rack** | Rooms as colour slips in a steel room rack; records read like printed registration cards |
| 2 | **Two-Ink Print** | A two-colour risograph job: violet and cyan inks, round key-tag room badges |
| 3 | **Pool Lanes** | Motor-lodge modern: the day flows down vertical swim lanes |
| 4 | **Noughts & Crosses** | Swiss 3-module grid; rooms marked O free and X taken |
| 5 | **Reservation Book** | An open reservation diary with a ribbon and thumb-index tabs |
| 6 | **Night Console** | Dark, keyboard-first: a command bar, one queue, keycap shortcuts |
| 7 | **Mirror** | Bilateral symmetry: arrivals and departures mirror each other across an axis |
| 8 | **Lift Panel** | Lift-panel navigation, ▲ arriving / ▼ leaving, corridors of doors |
| 9 | **Bedside Clock** | Backlit LCD windows, seven-segment numerals, a rubber-key nav row |
| 10 | **Whiteprint** | An architect's diazo sheet: rooms as floor plans, a title block, a sheet index |

## Screens (every design)

| File | Screen | Role |
|---|---|---|
| `01-today` | Today board: all 64 rooms, arrivals (check in), departures (check out) | Receptionist |
| `02-availability` | Rooms free per type × 16 nights; room chart; start a booking | Receptionist |
| `03-new-booking` | Stay, room type, guest, extras (breakfast, dinner, pickup), promo code, totals | Receptionist |
| `04-booking-rebook` | Booking detail with extras, promo, history, cancel terms; Rebook panel open | Receptionist |
| `05-check-in` | ID, room assignment, payment guarantee, keys, dinner upsell | Receptionist |
| `06-check-out` | Folio, payment, pre-departure checklist, settle and check out | Receptionist |
| `07-rooms` | Room types with price and count; edit, add, delete (blocked while booked) | Admin |
| `08-promo-codes` | Codes with id, code, title, required date range, optional limit; create one | Admin |
| `09-users` | Staff with roles; create a user and see what each role can do | Admin |

## Folder layout
```
designs/
├── index.html          compare all 10 designs
└── design-N/
    ├── index.html      this design's gallery, palette and type
    ├── README.md       tokens, components, status encoding, open decisions
    ├── assets/         CSS + self-hosted fonts (no network needed)
    ├── screens/        9 HTML screens
    └── png/            9 PNGs @2x
```

## Placeholders, not spec
- **Promo "Offer" / discount.** Not in the brief; it was added so a code carries a value. Confirm the discount model.
- **Prices.** Extras (breakfast $18 and dinner $42 per guest per night, pickup $55 per trip), the 12% tax, and room prices and counts are all placeholders.
- **Data.** The hotel name "Alder House", every guest and staff member, the phone numbers (555) and the emails (example domains) are synthetic.
- **Admin access to front-desk actions.** Admins can *view* the front-desk screens, but the brief doesn't say whether they can book.
- **One promo code per booking.** This is assumed.
