# Hotel Front Desk: design exploration

Ten different visual directions for a single-hotel front-desk web app. Each direction is a complete set of **9 desktop screens** (1440 px) built from identical content, so the designs can be compared screen for screen.

**Receptionist screens**
- Today board (check in / check out)
- Availability
- New booking (extras + promo code)
- Booking detail with rebook and cancel
- Check in
- Check out and bill

**Admin screens**
- Rooms
- Promo codes
- Users

![Design 1 · Today](designs/design-1/png/01-today.png)

## Browse
- Open [`designs/index.html`](designs/index.html) in a browser to compare all ten directions.
- Each `designs/design-N/` folder contains:
  - `index.html`: that design's gallery
  - `README.md`: tokens, components, open decisions
  - `screens/`: HTML
  - `png/`: PNG @2x

| # | Direction |
|---|---|
| 1 | The Rack |
| 2 | Two-Ink Print |
| 3 | Pool Lanes |
| 4 | Noughts & Crosses |
| 5 | Reservation Book |
| 6 | Night Console |
| 7 | Mirror |
| 8 | Lift Panel |
| 9 | Bedside Clock |
| 10 | Whiteprint |

Static HTML/CSS with no build step, and every screen opens offline.

All guest data, prices, the 12% tax and the promo "Offer" field are placeholders, not spec. See [`designs/README.md`](designs/README.md).

Product context: [`PRODUCT.md`](PRODUCT.md).
