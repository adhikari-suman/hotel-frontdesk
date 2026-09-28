# Design 12: House Lights

**Idea:** the hotel as a small theatre's box office after the house lights go down. The 64 rooms are seats in a curved four-row auditorium (one row per floor, floor 4 at the back) facing the front desk as the stage. A stay is a ticket with a perforated stub. Today's arrivals and departures run down the left edge as a timed cue list. Navigation is a row of footlights along the bottom of the screen.

Open `index.html` for the gallery. The screens are in `screens/`, and the @2x screenshots are in `png/`.

## Tokens

| Token | Hex | Meaning |
|---|---|---|
| `--house` | #1E1024 | Page ground. Velvet-dark, not black |
| `--velvet` | #2A1733 | Panels |
| `--raised` | #36203F | Inputs, nested cards, empty seats |
| `--seam` / `--seam-soft` | #4B3457 / #3A2544 | Borders, hairlines |
| `--text` | #FFFFFF | Primary text |
| `--muted` / `--dim` | #B9A5C3 / #A898B3 | Secondary and tertiary text |
| `--spot` | #9B6BFF | The spotlight: the one primary action per screen, the current nav item, your hold |
| `--free` | #3ED6BB | Free rooms, valid input, completed steps, discounts |
| `--arr` | #F2B544 | Arrivals, attention, admin-role marks |
| `--dep` | #7FB2FF | Departures (steel-blue stage gel) |
| `--rose` | #FF4F7B | Destructive actions, out of order, errors |
| `--inhouse` | #6D4F86 | Occupied seat fill |

Radii: seats 12/12/5/5 (a chair back), panels 14, controls 8, tags as pills.

## Type
- **Darker Grotesque** (500, 700, 900) for display: screen titles, room numbers, guest names on tickets, totals and counts. It is set tight and heavy, like a playbill.
- **Commissioner** (400–700) for the interface, with tabular figures everywhere.
- Both are self-hosted as woff2 in `assets/fonts/` with their OFL licences.
- Minimum text size is 11px.

## Components
- **Auditorium seat map** (01): 4 × 16 seats set on an arc, with an aisle between the Twin Doubles and the price-labelled type bands above. A ringed seat marks the next arrival.
- **Ticket**: booking header with a perforated stub that carries the room number (01, 04, 05). A vertical variant holds the running totals (03, 06).
- **Cue list** (01, 05): timed arrivals and departures, each with an inline Check in or Check out button.
- **Footlight dock**: bottom navigation in two groups, Front desk and Admin only. Admin items always show a lock. On receptionist screens they are dimmed and the dock says they are read-only.
- **Availability matrix** (02): free rooms per type across 14 nights, plus a room-by-night strip for the chosen type.
- **Status tags**: each has a glyph and a word as well as a colour. Ring means free, dot in house, ▲ arriving, ▼ departing, ✕ with hatching out of order, ◆ your hold, ✓ done.

## Rules
- There is one `.btn.primary` (violet, glowing) per screen. Check in and Check out use amber and orchid outline buttons.
- Destructive buttons use a dashed rose outline (`.btn.danger`) and are never filled violet. If a delete is blocked, the button is dimmed and the reason is spelled out: a note on room types, and an overlay for room 416.
- Permissions are visible on the screens. Promo codes are apply-only for receptionists ("Admins create them"). Admin nav items are lock-marked. Users (09) has an explicit role matrix. The admin screens are signed in as Daniel Reyes.

## Open decisions and placeholders
- **Promo "offer"**: the brief does not define it. "15% off room nights" is a placeholder, and the create form offers % off, $ off or a free night, marked *Placeholder*.
- **summer2026 has expired** (30 Sep) but the hero booking uses it on 14 Oct. The design shows it as *honoured from quote Q-2291 (29 Sep)*. The real rule (validity checked by booking date or stay date, and whether overrides are allowed) is undecided.
- **Tax 12%** is a placeholder, applied to rooms and extras alike.
- **Check-out (06)** uses the scenario date Sat 17 Oct, the hero's departure day, and the screen says so. Its folio includes one dinner (2 × $42) added at check-in: total $956.37.
- **Screen 04** shows a rebook to 15–18 Oct as an unsaved in-progress state. Other screens show the original 14–17 Oct booking.
- The cancellation terms (free until 48 h before arrival, first night charged), the $150 incidentals hold, the key encoder and the guest's past-stay lookup are all assumptions.
- Board split for "now": 32 in house, 9 arriving (2 already in), 7 departing (3 out), 14 free, 2 out of order = 64. Tonight: 41 occupied, 21 free, 2 out of order.
- Guest names beyond the canonical ten (for example Noor Haddad, Leo Hartmann and the in-house surnames) are synthetic fill.
