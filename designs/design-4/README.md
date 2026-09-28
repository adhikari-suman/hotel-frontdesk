# Design 4 — Fob Rack

**Idea.** The front desk as the wall of pigeonholes behind the counter. Every room is a recessed cubby; a coloured plastic key fob hanging in the cubby means the key is at the desk (room free or ready for an arrival), an empty cubby means a guest has the key. Navigation hangs from a rail as punched fobs. Whatever you are working on is written up on a perforated "counter slip" on the right.

Open `index.html` for the gallery, palette, type specimen and all 9 screens.

## Tokens

| Token | Hex | Meaning |
|---|---|---|
| `--ink` / `--band` | `#2A1A28` | Plum ink: text, top band, active filter chip |
| `--paper` | `#EEEBF5` | Lilac page ground |
| `--cubby` | `#FBFAFD` | Recessed panels (inner top shadow) |
| `--well` | `#E3DEEC` | Empty wells, neutral chips |
| `--rule` / `--rule-strong` | `#D6CFE2` / `#B9AFCB` | Hairlines, input borders |
| `--teal` | `#1F6F82` | Primary action, selection, active nav fob |
| `--amber` | `#C9861A` | Arrivals ("Due in"), low availability (2 or fewer) |
| `#8F7CD0` | | Departures ("Due out") outline |
| `--moss` | `#306515` | Free, verified, discount amounts |
| `--ox` | `#A71C0D` | Destructive actions, closed rooms, validation errors |
| `--fob-q` | `#BAABEA` | Queen fob |
| `--fob-t` | `#8CCBD9` | Twin Double fob |
| `--fob-d` | `#7A4A70` | Deluxe fob |
| `--fob-f` | `#8DBF5A` | Family Suite fob |
| `#F4EDDC` | | Office (admin) nav fobs, permission notes |

## Type
- **Big Shoulders Display** 600/800: room numbers, headings, dates in slips, totals. It's condensed, so 16 rooms fit on one floor row.
- **Atkinson Hyperlegible** 400/700: all UI and data. Slashed zero and distinct 1/l help when reading refs like AH-26-0417 aloud.
- Both self-hosted in `assets/fonts/` (woff2 from fontsource) with OFL licences.

## Components
- **Top band**: hotel, date, search, signed-in user with role badge (Receptionist lilac, Admin tan with shield).
- **Fob nav rail**: hex key-fob tabs on rings. Desk group | Office group. Office fobs carry a lock icon; for receptionists they are greyed and labelled "admin only".
- **Cubby**: recessed room cell. Status is always a word ("Free", "Staying", "Due in", "Due out", "Closed") plus a border treatment and fob presence, never colour alone. Closed rooms are hatched.
- **Counter slip**: white card with a perforated top edge. Holds the running registration card, quote, rebook panel, payment, or create forms.
- **Cubby box**: recessed section panel with a condensed heading.
- **Pills**: icon + text for every status (Active, Scheduled dashed, Expired, Used up, Invited, Deactivated).
- **Totals block**: dashed subtotal rule, solid rule over a large condensed grand total.
- **Promo ticket**: dashed moss border for an applied code.
- **Steps**: numbered circles on check in only, because it's a real sequence.

## Rules
- One teal primary button per screen. Destructive actions are oxblood outline, or solid oxblood only for the final confirm (Cancel and charge).
- Text is 11px minimum. Status never relies on colour alone.
- Admin-only features are marked with a lock in the nav and a note on the page. Receptionists see "Only admins create codes" next to the promo field.
- Delete stays blocked while a room has current or future bookings. A dark tooltip gives the reason and suggests an alternative.

## Screen notes and open decisions
- **Promo offer is a placeholder.** The brief doesn't define offers. "15% off room nights" (summer2026) is used as given. The other offers are invented: autumn26 10%, longstay7 7th night free, winter2026 free breakfast, staffkin 20%. The create form labels the Offer field "to be defined".
- **summer2026 vs. today.** The code's range ends 30 Sep but the hero booking uses it on 14 Oct. We treat the date range as a **booking window**: the code was applied to quote Q-0928 on 28 Sep and is honoured when that quote is confirmed. This needs a product decision.
- **Cancellation terms** (free until 48 h before arrival, then first night + tax as the fee) and the **waive-fee approval** are placeholders.
- **Incidentals hold** ($150), key encoding, card "Visa ending 0042", guest note, pickup time, the second guest and quote/folio numbers are all synthetic.
- **Check out** is shown on the departure date (Sat 17 Oct), so the top band shows that date.
- **Rebook** (04) shows the panel open, not yet confirmed. Screens 05 and 06 follow the original 14–17 Oct dates.
- **Rooms** (07) shows an unsaved Deluxe price edit ($238 → $248) as an example. Canonical prices elsewhere stay $238.
- Occupancy numbers on Today: 41 in house (7 of them due out), 9 arrivals, 12 free, 2 closed = 64. After changeover tonight: 43 occupied, 19 free.
- Tax 12% is a placeholder.
