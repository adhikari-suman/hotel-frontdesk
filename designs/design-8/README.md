# Design 8: Lift Panel

The hotel's lift car panel is the interface. The left column is a dark brushed-steel lift panel: a dot-matrix indicator window for the clock and the tonight tally, rectangular desk keys for the front-desk views, round floor buttons 8 to 1 whose rings light when a floor still has arrivals, arrival and departure counters, and round service keys for the admin sections. In the content area every floor opens as a corridor of eight doors, and each door carries a door-hanger tag with its status code and guest. Green with an up triangle means arriving or ready. Amber with a down triangle means leaving.

It refuses the category default of a flat table of rooms. The house reads as a building you walk through, while every action stays a plain, labelled control.

- Theme: dark, from the scene (a metal panel with lit rings under lobby light).
- Screens: `screens/01-today.html` to `screens/09-users.html`, PNGs in `png/` (1440 px, @2x, full page).
- Stylesheet: `assets/liftpanel.css` (tokens and every shared component). Each screen adds a small page `<style>`.
- No JavaScript and no runtime network requests. Fonts are self-hosted in `assets/fonts/` with their OFL licences.

## Tokens

### Colour

| Token | Hex | Role |
|---|---|---|
| `--ground` | `#24262B` | Page ground (steel) |
| `--panel` | `#2E3137` | Lift column, raised keys and buttons |
| `--face` | `#383B42` | Brushed content plates (with `--brush`, a fine horizontal repeating-linear-gradient grain) |
| `--face-2` | `#33363C` | Quieter plate, desk keys |
| `--well` | `#1D1F23` | Inset wells: inputs, room-number plates, toggles |
| `--glass` | `#0E0F11` | Indicator windows (with a faint unlit-dot grid) |
| `--leaf` | `#2B2E33` | Door leaf |
| `--text` | `#E8E9ED` | Engraved text |
| `--muted` | `#A9ACB5` | Labels, secondary text (4.9:1 on `--face`) |
| `--faint` | `#969AA3` | Disabled controls only |
| `--green` | `#44EEAA` | Arriving (up), ready, lit rings, selection, the primary action (ink `#062A1C`) |
| `--amber` | `#EEAA33` | Due out (down), leaving, changed fields, the rebook difference (ink `#2E1C00`) |
| `--blush` | `#FFCCCC` | In-house (OCC) door hangers (ink `#4B1E2B`) |
| `--plum` | `#AA5599` | Out of order, blocked, destructive. Text tint `--plum-hi` `#E3A6D6`; hatched fills use `#A04E90`/`#8A3F7C` so white text holds 5:1 |

The steel greys carry the layout. The four signal colours appear only on status, selection and the one committing action.

### Type

| Family | Use |
|---|---|
| **Onest** (variable 100–900) | All UI: headings, body, labels, buttons and data, with tabular numerals set on `body`. Labels are engraved plate caps: 11 px, weight 600, +0.085em tracking, uppercase, with a 1 px dark text-shadow. |
| **Doto** (dot-matrix, 100–900) | Indicator windows only: the clock, counts (arrivals, departures, nights, keys, promo uses, tonight tallies) and floor numbers. Never used for words in running UI. |
| **Red Hat Mono** (300–700) | Promo codes, booking refs and code IDs (`autumn26`, `HVK-2094`, `PRM-0014`). Kode Mono was tried first and dropped because its V reads as U at small sizes. |

Scale (fixed rem, product ratio): h1 24 / h2 15 / body 14 / secondary 12.5–13.5 / labels and captions 11–12. Nothing is under 11 px.

### Spacing and radius

- Spacing steps: 4, 8, 12, 16, 20, 24, 32, 40 px. Plates use 16–18 px padding and are 20 px apart.
- Radius: 6 (chips and inputs 8), 10 (rows and callouts), 14 (plates), 999 (pills). Round keys and buttons are true circles.

## Components

- **Lift panel** (`.lift`): brand plate, main indicator (`.ind-main`: date, time, a floor slot with an arrow, and TONIGHT 53/64 83%), desk keys (`.rkey`), floor buttons (`.fl`, `.fl-btn`), the arriving and leaving counters (`.flow`), service keys (`.skey`) and the user plate (`.who`). The floor slot shows the floor the screen is about: up 7 on check-in, down 5 on check-out, 8 on the booking and availability screens, 6 on the rebook. It shows L (lobby) on the house-wide screens.
- **Corridor** (`.corridor`): a landing indicator with the floor number in Doto, then eight `.door`s over a floor strip. Each door has an engraved room-number plate, a knob, and a `.hanger` tag with a real punched hole (CSS mask) that sits over the knob. Door states: `s-arr`, `s-due`, `s-occ`, `s-vc`, `s-ooo`, `s-res`, `s-free`, plus `is-selected` (lit ring and a "Chosen" or "Assigned" tab) and `is-disabled`.
- **Inline hanger tag** (`.htag`): the same status tag at chip size, with the punched hole, used in legends, queues and headings.
- **Buttons**: pills with rings. `.btn-primary` is the green-lit pill, one per screen. `.btn-arr` and `.btn-due` are ring buttons for check in and check out. `.btn-danger` has a plum ring. `.is-pressed` is a latched key (the open Rebook). Disabled buttons flatten and grey out, with a hint underneath.
- **Round keys**: `.ibtn` icon keys, steppers with a Doto count window, `.rad` and `.chk` round radios and checks, `.tog` toggle.
- **Plates** (`.plate`, `.plate-head`, `.sect`, `.plate-foot`) and recessed `.well` windows. Sections inside a plate are divided by engraved rules, not nested boxes.
- **Choice rows** (`.choice`, `.rolekey`): radio options that light up with a green ring when selected and give a reason when unavailable.
- **Ledger** (`.ledger`): tabular money and data with engraved row rules and a heavier total rule.
- **Status lamps** (`.lamp`): a lit LED for Active, a ring for Scheduled or Invited, plum for Used up, and unlit for Expired or Deactivated. Every lamp has a word, and most have an icon.
- **Callouts** (`.note` ok / warn / stop / lock): framed with a full hairline. No side stripes.
- **Lamp bank** (availability): the number of rooms free, plus a row of pips, one lit pip per free room.

## Status without colour alone

Every status carries at least two non-colour cues:

| Status | Code | Shape and pattern | Words |
|---|---|---|---|
| Arriving | `ARR` plus an up triangle | Solid tag | "ETA 13:00" |
| Due out | `DUE` plus a down triangle | Solid tag. A late check-out is underlined and bold | "Out 11:00" / "Late 12:00" |
| In house | `OCC` | Solid tag | "Out Tue 29" / "In 09:05" |
| Vacant, ready | `VC` | Outlined tag on a dark face | "Vacant · Ready" |
| Out of order | `OOO` | Diagonal hatching on the tag and the door | "Repaint · Back 2 Oct" |
| Reserved (future) | `RES` | Grey solid tag | Guest name |
| Free for chosen dates | `FREE` | Outlined tag | "2 nights" / "Both nights" |

- The availability grid shows the number (or FULL on hatching) as well as the lamps.
- Lit floor rings are explained in the panel ("Lit ring: arrivals still to come"), and each floor also lists its counts with triangles.
- Promo and user statuses always show a word next to the lamp.
- Selection is a ring plus a label ("Chosen", "Assigned", "Selected").
- Disabled doors and options dim and give a reason ("Full on Sat 3", "Sleeps 2; this party is 4").

## Permissions, where they matter

- On receptionist screens the service keys (Rooms, Codes, Users) are locked with a lock badge and "Admin only. You can apply promo codes, not create them."
- The receptionist promo field says "Codes are created by admins".
- The admin promo form previews exactly what receptionists will see.
- Rooms: Family Suite delete is blocked with the reason (14 upcoming bookings and 7 rooms occupied tonight). Every delete key is disabled while its type has bookings.
- Users: role key-switches list what each role can and can't do.

## Open decisions

1. **Promo "Offer" field** (e.g. "15% off room nights", "7th night free") is not in the client brief. The brief defines a code as id, code, title, date range and optional count. The design shows Offer because totals need a discount, but its shape (percent, free night, fixed amount) is undecided.
2. **Placeholders, not spec:** the 12% tax, the extras prices (breakfast $18 per guest per night, dinner $42, pickup $55 per trip) and the room prices ($136 / $166 / $238 / $366) are placeholders.
3. **Lobby "L" in the indicator** on house-wide screens is part of the lift metaphor. Test it with staff, and fall back to a blank floor slot if it confuses.
4. **Deluxe price change copy:** "$248 applies to bookings made after you save" is our wording for the brief's "23 upcoming bookings keep $238". Confirm the rule for bookings made after the change for dates already sold.
5. **"Arriving drops to 9 of 11" / "Leaving drops to 4 of 9"** in the check-in and check-out outcome previews are derived from the canonical counts. The lift counters on those screens still show the state before the action.
6. **Surnames of other in-house guests** are invented, from a varied international set. Guests named in the future Family Suite chart are not reused in current rooms.
7. **Sticky lift panel:** the panel fits a 900 px-tall viewport. On shorter screens it scrolls inside itself.

## Detector notes (deliberate)

- `dark-glow`: lit rings on floor buttons, service keys, the primary pill, selected doors and LED lamps. The direction specifies offset-free, low-spread glows with a real inner shadow. Secondary controls (check-in/out buttons, radios, toggles, focus rings) were stripped of glow.
- `repeating-stripes-gradient`: the out-of-order hatching (a non-colour status cue) and the brushed-steel grain the direction asks for.
- `nested-cards`: inset wells (indicator windows, the booking summary window, the inline room editor), selected choice rows and framed callouts inside plates. None are cards inside cards.
- `cramped-padding`: door-hanger tags and chart stay bars are tight by design. Their text is centred and ellipsised within the tag.
