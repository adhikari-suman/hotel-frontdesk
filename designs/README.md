# Hotel front desk: 15 design directions

Fifteen visual directions for the same single-hotel front-desk web app. Each direction has the same **9 desktop screens (1440 px)**, all built from identical synthetic data, so you compare the design, not the content.

Open **`index.html`** to compare them. Pick a screen (Today, Availability, and so on) to see all 15 directions side by side.

| # | Direction | In one line |
|---|---|---|
| 1 | **Transit Map** | Room types are coloured lines; each stay is a journey from an arrival stop to a departure stop. The nav is a route map with a locked admin branch |
| 2 | **Split-Flap** | A station concourse: arrivals and departures on split-flap boards, and screens are stops on one route line |
| 3 | **Switchboard** | Rooms are jacks with lamps, a booking is a patch cord and the folio is a toll ticket. Lever keys run along the bottom |
| 4 | **Fob Rack** | The pigeonhole wall behind the counter: a hanging key fob means the key is at the desk |
| 5 | **Drawing Set** | Architect's sheets: a floor plan with door swings, stays as dimension lines and warnings as revision clouds. A title-block sheet index is the nav |
| 6 | **Mountain & Valley** | Folded paper: each room's fold shows its state. Screens are tri-folds and the nav is folder tabs |
| 7 | **Counting Frame** | A soroban: each room is a rod with one bead, raised when occupied and halfway when arriving |
| 8 | **Elements** | The hotel as a periodic table: rooms are element tiles with two-letter status symbols |
| 9 | **Lit Windows** | The hotel from the street at dusk: every room is a window. The nav is a lift panel with an admin key switch |
| 10 | **Stamp Sheet** | Perforated room stamps, engraved prices and out-of-order overprints. A booking is a franked airmail cover |
| 11 | **Warp & Weft** | Cloth on a loom: stays are woven across nights, and status is a weave pattern plus a glyph and a word |
| 12 | **House Lights** | A theatre box office after dark (the only dark UI): rooms are seats and stays are tickets. Footlights are the nav |
| 13 | **Tide Table** | A hydrographic chart: occupancy is a tide curve and statuses are buoys, each with its own shape |
| 14 | **Lift Car** | A 1930s lift: the nav is a brass floor dial, with admin floors past a key switch |
| 15 | **Leadlight** | An Arts & Crafts leaded window: rooms are glass panes, and a 3 × 3 window is the nav |

Each direction was built from its own seed string in `seed.json` (design *N* uses key *N*). The seeds are not reproduced anywhere in these designs.

## Screens (every design)

| File | Screen | Role |
|---|---|---|
| `01-today` | Today board: all 64 rooms by status, arrivals (check in) and departures (check out) | Receptionist |
| `02-availability` | Rooms free per room type over about 14 nights; pick a range to start a booking | Receptionist |
| `03-new-booking` | Dates, room type, guest, extras (breakfast, dinner, pickup), promo code, totals | Receptionist |
| `04-booking-rebook` | Booking detail with extras, promo, charges and history; Rebook panel open; cancel terms | Receptionist |
| `05-check-in` | ID check, room assignment, payment guarantee, keys, extras upsell | Receptionist |
| `06-check-out` | Folio (nights, promo discount, extras, tax), payment, settle and check out | Receptionist |
| `07-rooms` | Room types with price and count: add, edit, delete (delete blocked while booked) | Admin |
| `08-promo-codes` | Codes with id, code, title, required date range and optional limit; create a code | Admin |
| `09-users` | Staff with roles and status; create a user; what each role can do | Admin |

## Folder layout
```
designs/
├── index.html          compare all 15 designs, screen by screen
└── design-N/
    ├── index.html      the design's gallery, palette and type
    ├── README.md       tokens, components, rules, open decisions
    ├── assets/         one stylesheet + self-hosted fonts (OFL)
    ├── screens/        9 HTML screens (static; no network needed)
    └── png/            9 PNGs @2x
```

## Open decisions (placeholders, not spec)
- **Promo "offer" / discount.** The brief gives a promo code an id, code, title, date range and count, but no value. Every design shows "15% off room nights" as a placeholder.
- **The hero booking uses an expired code.** `summer2026` ends 30 Sep, but the hero stay is 14–17 Oct. The directions handle it differently: most assume a code is validated against the *booking* date, and a few reject it on New booking. Decide whether a code's date range applies to the booking date or the stay dates.
- **Prices.** Room prices and counts (Queen 24 × $136, Twin Double 16 × $166, Deluxe 16 × $238, Family Suite 8 × $366), extras (breakfast $18 and dinner $42 per guest per night, pickup $55 per trip) and the 12% tax are all placeholders.
- **Cancellation terms** are placeholders.
- **Admin access to front-desk actions.** The brief doesn't say whether admins can book.
- **Data.** "Alder House", every guest and staff member, the 555 phone numbers and the example.com emails are synthetic.
- **Check-out screens** are dated 17 Oct (the hero booking's departure). Every other screen is dated 14 Oct.
