# Design 9 — Lit Windows

**Idea.** The hotel seen from the street at dusk. The Today board is an architectural elevation of Alder House (4 floors × 16 windows) and every room chip is a window: lit amber = in house, blind half down = arriving, violet = departing, dark glass = vacant, boarded hatch = out of order. The same façade reappears wherever rooms are chosen (availability, check-in, room admin).

**Navigation.** A narrow lift panel on the right edge: round call buttons with icon + label, an LED readout showing the desk date at the top. Admin screens sit below a key switch. For receptionists the switch reads "Admin only" and the Rooms / Promo codes / Users buttons are dashed with a lock badge; for admins the switch is lit ("Admin key on").

**Layout.** Content left of the lift panel on a golden-ratio split, 61.8 / 38.2 (work area / summary-and-action column). The primary action always sits at the bottom of the right column.

## Tokens
| token | hex | meaning |
|---|---|---|
| --ink | #1D1B3A | text, lift panel, façade sky |
| --blue | #3355DD | the single primary action per screen, focus rings |
| --lamp | #EE8833 | occupied (lit window), active nav button, arrivals accents |
| --lamp-soft | #FBD9B6 | arriving blind, occupancy fill in availability cells |
| --violet | #7755FF | departing, selected date range, rebook panel |
| --plum | #664488 (+ hatch) | out of order |
| --glass | #DCE3F5 | vacant |
| --stone / --stone-2 | #E6DAD6 / #D9C9C4 | façade |
| --wall | #EDE4EC | page background (dusk-haze mauve, deliberately not cream) |
| --crimson | #B82A43 | destructive actions and errors only |
| --ok | #237A57 | discounts, completed steps, "can" |
| --rule | #DCD0D2 | hairlines |

## Type
- **Unbounded** 500/600: headings, room numbers, big totals, promo codes (building-sign lettering).
- **Instrument Sans** 400–700, tabular figures: everything else.
- Self-hosted woff2 in `assets/fonts/` with OFL licences. Minimum text size 11px.

## Components
- **Window** (`.win` / `.pane.lit|arr|dep|vac|ooo`): status is shown by fill, pattern and content (initials, half blind, hatch, ×), never colour alone; legend on the Today board.
- **Façade** (`.facade`, `.facade.mini`): sky strip with the sign, cornice, floors, lobby doors carrying arrival/departure counts.
- **Lift panel** (`.lift`, `.lbtn`, `.keyswitch`): primary nav + permission cue.
- **Availability cell** (`.cell`): arched window with free count; fill height = how busy the night is; dashed hatch = full; violet = picked range.
- **Plate** (framed panel) vs **ledger** (open list under a 2px ink rule): two panel types so the page isn't one card grid.
- **Money table** (`.money`), **promo chip**, **stepper**, **steps** (only check-in, which really is a sequence), **notes** (info / warn / lock / danger / ok).

## Rules
- One blue primary button per screen; secondary actions are outline pills; destructive actions are crimson outline and name the charge ("Cancel booking and charge $226.58").
- Delete is disabled while a room or type has bookings, with the reason and booking refs shown next to it.
- Receptionists see admin areas as locked, not hidden; promo codes are "apply only" at the desk.

## Numbers used (hero booking AH-26-0417)
Deluxe 3 × $238 = $714.00; summer2026 15% off room nights −$107.10; breakfast 2 × 3 × $18 = $108.00; pickup $55.00; subtotal $769.90; tax 12% $92.39; total $862.29. Rebook to 14→18 Oct: +$266.89, new total $1,129.18. Late cancel (inside 48 h): first night after promo $202.30 + tax = $226.58.

## Open decisions / placeholders
- **Promo "offer"** (15% off room nights) isn't defined in the brief; the create-code form shows an Offer field marked as a placeholder.
- **summer2026 ends 30 Sep but the hero stay is 14–17 Oct.** We assume a code is validated against the *booking date*, so the hero booking is shown as quoted/booked on 29 Sep. If the rule is stay date instead, the hero booking can't use this code.
- **Check-out screen date** is shown as Sat 17 Oct (the hero's departure), not the canonical "today" of 14 Oct.
- Tax 12%, cancellation terms (free until 48 h before arrival, then first night), the $50/night incidentals hold, and the admin approval for refunds over $200 are placeholders.
- Guests beyond the ten canonical names (departing guests, stayover initials) and the card "Visa ending 4418" are synthetic filler.
- Room-to-floor layout (Queen/Twin on 1–2, Queen/Deluxe on 3, Deluxe/Family on 4) and which rooms are out of order (207, 415) are our assumption.
- Fixed two roles; custom roles not designed.
