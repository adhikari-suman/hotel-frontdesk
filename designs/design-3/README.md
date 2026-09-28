# Design 3: Switchboard

**Idea:** the front desk as a hotel telephone switchboard. Rooms are jacks in a 16 × 4 jack field (one row per floor, 16 rooms per floor). Each jack has a lamp for its state. A booking is a crimson patch cord plugged into a room. The folio is a toll ticket with time-stamped, punched lines. Navigation is a **key shelf docked at the bottom** of the screen, where an operator's lever keys sat below the jacks. Admin keys sit in a separate locked group.

Open `index.html` for the gallery. Screens are in `screens/`, and the @2x screenshots are in `png/`.

## Tokens

| Token | Hex | Meaning |
|---|---|---|
| `--steel` | `#ECEEEB` | Exchange steel: page ground |
| `--face` | `#F9FAF7` | Faceplate: panels |
| `--plate` | `#E1E4DE` | Designation strip: panel title bands, code chips |
| `--rule` / `--rule-2` | `#C9CDC6` / `#B3B8B0` | Hairlines, input borders |
| `--graphite` | `#22252B` | Ink, primary "lever key" buttons, drawers |
| `--muted` | `#5D636B` | Secondary text (AA on faceplate) |
| `--shelf` | `#2B2F35` | Bottom key shelf |
| `--crimson` | `#A50D2A` | Patch cord, current selection, discounts, destructive actions |
| `--mint` / `--mint-ink` | `#74FDE0` / `#0B7A66` | Free room lamp / text |
| `--amber` / `--amber-ink` | `#F0B429` / `#8A5A00` | Arrival lamp / text, low availability |
| `--sky` / `--sky-ink` | `#6CC3F0` / `#1F6F9A` | Departure lamp / text |
| opal | `#FFFFFF` + graphite ring | In-house lamp |

Radius: 3px on panels and inputs, 2px on chips and jacks. There is one shadow, used only for drawers and the shelf.

## Type
- **Michroma** (400): a wide engineering face used like engraved designation strips. It sets page titles, panel labels, room numbers, codes, references and big totals, always in sentence case.
- **Archivo** (variable, 100–900, width 62–125%): all UI text, forms and tables, with tabular numbers.
- Both fonts are self-hosted in `assets/fonts/` with their OFL licences.

## Signature components
- **Jack** (`.jack`): lamp, jack hole, room number, status word and guest surname. `.plugged` adds a crimson ring and a crimson plug in the hole.
- **Patch cord** (`.cord`): an SVG cord from the booking card to the room jack, used for room assignment on Check in.
- **Designation strip** (`.panel > .ds`): the panel title band with two screw heads.
- **Toll ticket** (`.ticket`): the folio. Each line has a punch hole, a Michroma time stamp, the charge, qty and amount. The balance row is graphite.
- **Key shelf** (`.shelf`): the bottom nav. The active key is thrown, with a lit mint lamp and underline. Locked admin keys show a lock and read "Admin only" on receptionist screens.
- **Meter** (`.meter`): a lamp-bank count row.
- **Drawer** (`.drawer`): a graphite-headed side panel that holds the screen's one primary action.

## Rules
- A lamp colour always comes with a word, and the lamp shape changes too: ring = in house, diamond = out of order, hatched = to clean, hatched cell = full.
- Each screen has one primary action: a solid graphite button with a mint lamp. Destructive actions are crimson outline, or crimson solid for a final confirm. They never use graphite.
- Crimson means "this one": the selected booking, the plugged room, discounts, and destructive actions.
- Minimum text is 11px. Room numbers and codes use Michroma. People and prose use Archivo.
- Permissions are visible in several places. The shelf has locked admin keys. Promo code panels state "codes are created by admins". Delete is locked with a reason whenever a room or type is booked. Users has a role matrix.

## Screens
1. **Today**: the jack field of 64 rooms by floor, a meter row, an arrivals queue (Check in) and a departures queue (Check out), plus out of order, extras due and night handover.
2. **Availability**: free rooms per type × 14 nights with low and full states, the selected Deluxe 14–17 Oct range, a room-by-room Deluxe cord chart, and a selection drawer with **Start booking**.
3. **New booking**: stay, room type, guest, extras (breakfast, dinner, pickup), promo code field and a live total.
4. **Booking / rebook**: stay details, extras add/remove, promo remove/replace, charges and history. The Rebook drawer is open (15→19 Oct, moves to 309, +$266.89). Cancel shows terms and the fee.
5. **Check in**: ID check, room assignment by patch cord to 312, card pre-authorisation, key encoding and extras upsell.
6. **Check out**: toll-ticket folio (nights, promo lines, extras, tax) and a settle drawer.
7. **Rooms (admin)**: types with rate and count, edit/add type, a per-floor rooms list, delete blocked with an explanation, and a deletable draft room.
8. **Promo codes (admin)**: the list with ID, code, title, required date range, optional limit and uses; a code calendar; a create form showing the "end date required" error.
9. **Users (admin)**: staff with roles and status (active, invited, deactivated), a create-user form and the role permission matrix.

## Open decisions and placeholders
- **Promo offer**: "15% off room nights" is a placeholder. The brief doesn't define offer types, so the create form marks the field as a placeholder.
- **Promo validity vs. the hero booking**: `summer2026` ends 30 Sep 2026, but "today" is 14 Oct. This design assumes codes are checked against the **booking date**. So:
  - On screen 03 (a booking made today), `summer2026` is **rejected** as ended, `autumn26` is suggested, and the totals carry no discount.
  - On screens 04–06, AH-26-0417 was booked on 22 Sep with `summer2026` validly applied.
  - This needs a product decision.
- **Check-out date**: screen 06 is dated Sat 17 Oct, the hero's departure day. All other screens use Wed 14 Oct.
- **Check-out folio**: it includes one dinner for 2 ($84) added during the stay, to show extras posted mid-stay. Total $956.37.
- **Placeholder terms**: the 12% tax, the 48-hour cancellation policy, the first-night cancellation fee, and the $50/night incidentals hold are all placeholders.
- **Rebook pricing**: the rebook keeps the original promo. Whether a promo survives a rebook is undecided.
- **Waiving fees**: whether receptionists can waive a cancellation fee is shown as "needs note". This is to be confirmed.
- **Guest names**: surnames for in-house guests beyond the canonical 10 are synthetic filler.
