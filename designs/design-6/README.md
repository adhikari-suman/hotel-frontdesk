# Night Console (design-6)

A keyboard-first command console for the 24-hour front desk at Alder House. It is built for the night shift under dim lobby light, so it is dark. There are no dashboard tiles. A command bar runs across the top and is the main way to move around. The day is **one time-ordered queue** where arrivals and departures are merged, with a live "now" line between what is done and what is next. Every action shows its keycap, and hot pink marks the cursor.

## Topology (the same on all nine screens)

- **Command bar**, full width at the top. It holds the mark, the input ("Type a guest, room, ref or command…", `⌘K`), recent commands as mono chips, the hotel name and the clock.
- **Slim icon rail** on the left (88 px). Each item has a label and its go-to keycaps (`G T` Today, `G A` Availability, `N` New booking, `G R` Rooms, `G P` Promo codes, `G U` Users). The rail has a Desk group and an Admin group, with the signed-in user at the foot. On receptionist screens the Admin group stays visible but locked ("Admin only", lock glyphs), so the limit is seen, not discovered.
- **Split view.** A list sits on the left (40%) on the ground colour, and the focused item's detail sits on the right (60%) on the surface colour. Forms open as inline panels in the detail pane, never as modals.
  - Today, Check-in and Check-out share the queue. Check-in and Check-out use the queue's Arrivals (`A`) and Departures (`D`) filters.
  - Availability lists nights down the page, like the queue, with the same now line.
  - Booking shows the booking record on the left and the Rebook panel on the right.
  - Rooms, Promo codes and Users list their records on the left and put the create or edit form on the right.
- **One overlay in the whole set:** the command palette on New booking, showing results for `haddad`. It drops from the command bar over the list pane only, so the form stays readable.

## Tokens

### Colour

| Token | Hex | Role |
|---|---|---|
| `--ground` | `#111016` | Page, list pane, input wells |
| `--surface` | `#1A1921` | Command bar, detail pane |
| `--raised` | `#23212C` | Focused rows, keycaps, buttons, summary panel |
| `--line` | `#2E2B39` | Hairlines between rows and sections |
| `--line-2` | `#3D3A4B` | Control borders |
| `--fill-occ` | `#34313F` | In-house (OCC) fill in the house matrix and room chart |
| `--text` | `#EEEBF6` | Body text (14.8:1 on surface); in house |
| `--muted` | `#A6A2B8` | Secondary text (7.0:1 on surface, 6.4:1 on raised) |
| `--faint` | `#8C889E` | Disabled text only (5.1:1 on surface) |
| `--pink` | `#FF33EE` | The cursor: focus rings, the now line, selection tint, and the one primary action per screen (with `#111016` text, 6.3:1) |
| `--arr` | `#7CC4FF` | Arriving (ARR) |
| `--due` | `#FFC24B` | Due out (DUE), warnings, changed fields |
| `--vc` | `#7BE3B0` | Vacant and ready (VC), valid, available |
| `--ooo` | grey hatch | Out of order (OOO), always a 135° hatch and never a hue |
| `--err` | `#FF9A85` | Error text and borders; Cancel booking |

Hot pink is never decoration. It appears only where the cursor is (the focused row, the focused field, the palette's current result, the selected nights or option), on the now line, and on the single committing button.

### Type

- **Geist** (variable, 100–900) for the interface: names, labels, headings and money. Money uses tabular figures.
- **Geist Mono** (variable) only for what someone types or reads as data: the command bar, keycaps, times, room numbers, refs (`HVK-2094`) and codes (`autumn26`, `OCC`). It is never used for headings.
- Scale (px): 11 · 12 · 13 · 14 (base) · 15 · 20 (pane titles) · 26 (focused item) · 30 (room number block). Tracking tightens on the larger steps (−0.015 to −0.04 em).
- Both fonts are self-hosted from `assets/fonts/` under the SIL OFL (licence files included).

### Spacing and shape

- Space steps: 4 · 8 · 12 · 16 · 24 · 32 · 48. Panes use 24 px gutters, and sections are separated by 22 px plus a hairline.
- Radius: 4 px keycaps and tags · 6 px controls · 8 px panels and rows · 10–12 px summary panel and palette.
- Depth comes mostly from the three planes (ground, surface, raised). The only shadow belongs to the palette overlay: an offset, blurred black shadow with no coloured glow.

## Components

- **Keycap** (`kbd`): mono 11 px on the raised colour, with a 2 px bottom border as the key skirt. Return and Command are drawn SVG glyphs, not Unicode. Every action carries one: `⏎` runs the focused row's action, `⌘⏎` commits a form, `N` new booking, `E` add extra, `R` rebook, `C` cancel, `P` apply promo, `J`/`K` move, `G`+letter go to, `Esc` close.
- **Buttons:**
  - Primary: pink fill, dark text, keycap inside.
  - Secondary: raised fill with a border.
  - Quiet: transparent with a hairline.
  - Ghost: text only.
  - Open: a pink ring, for example Rebook while its panel is open.
  - Disabled: dashed border in faint text, with the reason written next to it.
- **Queue row:** time (mono), then the status tag, room (mono), guest and meta (type, nights, extras as icon plus word, promo code chip, balance or "settled"), then the action. Past rows are muted and sit above the pink now line. The focused row is raised and gets a 2 px pink ring all round (no side stripe).
- **Status tag:** glyph + code + outline, for example `→| ARR`, `|→ DUE`, `■ OCC`, `□ VC` (dashed), `⊘ OOO` (hatched) and `⊟ RES`.
- **House matrix:** 8 × 8 small cells, floors 8 to 1, with each floor's type and price. Each cell shows the room number and its code. The same cell becomes the room picker on Check-in, the before-and-after preview on Check-in and Check-out, and the floor map by type on Rooms.
- **Room chart (Family Suite):** stays drawn as bars. In house is filled, reserved is outlined, arriving has a blue outline plus the ARR glyph, and out of order is hatched. Free nights inside the selection are dashed. The selection is a pink column band, and the now line is a pink vertical.
- **Forms:** input wells on the ground colour. Focus is a pink 2 px outline, a changed field is amber with "was $238", an error is `--err` with a message that names the fix, and read-only fields are dashed.
- **Ledger:** a right-aligned tabular money table with subtotal, total and balance steps.
- **Notes:** hairline-bordered wells with an icon. Warning notes use an amber border and the lock note states the permission. There are no side stripes.
- **Palette:** results grouped as drafts, then bookings, rooms and refs (with an empty state that says what search covers), then commands for this draft. The footer has keycap hints.

## Status without colour

Every status carries at least two non-colour signals:

| Status | Code | Glyph | Pattern |
|---|---|---|---|
| Arriving | `ARR` | arrow into a bar | outline |
| Due out | `DUE` | arrow out of a bar | outline |
| In house | `OCC` | filled square | solid fill |
| Vacant, ready | `VC` | hollow square | dashed outline |
| Out of order | `OOO` | slashed square | diagonal hatch |
| Reserved (charts) | `RES` | square with a bar | outline |
| Done (queue) | `IN` / `OUT` | tick | muted text above the now line |

Promo and user states use a glyph and a word: Active, Scheduled, Used up, Expired, Invited, Deactivated. Full nights in Availability read "0 full". Disabled rooms on Check-in keep their codes.

## Permissions made visible

- The receptionist rail shows the Admin group locked.
- The promo field on New booking says "Codes are created by admins. Receptionists can apply a code but not create one." The Promo codes screen previews that same field.
- Check in on the booking is disabled until arrival day, and the screen says so.
- Deleting Family Suite is blocked in place ("14 upcoming bookings and 7 rooms occupied tonight").
- On Users, the role cards list what each role can and can't do.

## Screens

1. **01-today:** the queue from 09:05 to 19:40 with the now line at 10:42. Chidi Okafor is focused with "Check in ⏎", the house matrix and tonight's tally (53 of 64, 83%) sit below, and New booking is the primary.
2. **02-availability:** 16 nights × 4 types with Family Suite Fri 2 and Sat 3 selected, Start booking ($732.00) and the room-by-room chart.
3. **03-new-booking:** the command palette for `haddad` over the queue, the Leila Haddad draft and a sticky summary (total $919.74). Confirm booking is the primary.
4. **04-booking-rebook:** booking HVK-2094 with the Rebook panel open, moving the stay to Thu 8 → Sun 11 Oct for +$266.90. Confirm rebook is the primary.
5. **05-check-in:** Chidi Okafor (early), ID match, a room pick on floors 6–7, pre-authorisation of $713.76, keys and extras, and the stamp. Complete check-in is the primary.
6. **06-check-out:** Maja Lindqvist in 505, late check-out, the full folio, pay with, the leave checklist, and 505 going to VC. "Settle $489.14 and check out" is the primary.
7. **07-rooms (Admin):** the Deluxe price $238 → $248 in edit, the blocked Family Suite delete, recent changes and the floor map. Save changes is the primary.
8. **08-promo-codes (Admin):** six codes and the newyear27 form, with the winter26 overlap warning and a receptionist preview. Create promo code is the primary.
9. **09-users (Admin):** eight staff and the Mei Lin Tan form with role cards and the invite link. "Create user and send invite" is the primary.

## Open decisions

- **The promo "Offer" field is not in the brief.** The brief defines a code, title, date range and usage count only. The offer (15% off, 7th night free and so on) is shown so the totals are explainable. The team needs to decide whether it belongs in the promo code model.
- **Placeholders:** the 12% tax, extras prices, room prices, the hotel name and all guests and refs are synthetic.
- **The primary on Today.** The content spec makes New booking the primary action (pink). The direction's large "Check in ⏎" on the focused item is kept big but secondary, so each screen has one committing action. If the desk decides the focused item's action should be the primary, the pink moves to it.
- **The keymap is a proposal.** `C` for cancel may want a confirm step or a modifier. The `G`+letter go-to pairs need a check against screen-reader and browser shortcuts.
- **Early check-in before 14:00:** the design lets 704 be checked in at 10:46 because the room is ready. Whether an early check-in fee applies is not in the brief and is not shown.
- **No light theme.** This direction is dark on purpose for the night shift. A day shift might want a light variant.

## Files

- `assets/console.css`: tokens and all shared components. Each screen adds a small page `<style>`.
- `assets/fonts/`: Geist and Geist Mono (latin, variable woff2) plus `OFL-Geist.txt` and `OFL-GeistMono.txt`.
- `screens/*.html`: the nine screens, static HTML and CSS, each with an inline SVG sprite (Lucide icons under ISC, plus authored status glyphs). There is no JavaScript and no network request.
- `png/*.png`: 1440 px wide at 2x, full page.
