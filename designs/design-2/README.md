# Design 2 · Two-Ink Print

Nine desktop screens (1440 px) for the hotel front-desk web app, covering both roles: Receptionist and Admin. Everything is static HTML/CSS with no JavaScript and no network requests, and each screen is also exported as a full-page PNG at 2x.

Open **`index.html`** for the gallery, or go straight to `png/`.

```
design-2/
├── index.html      gallery: direction, palette + type specimen, placeholders note, the 9 screens
├── png/            the 9 screens as PNG @2x (2880 px wide, full page)
├── screens/        the 9 screens as HTML (open in a browser; works offline)
└── assets/         twoink.css (tokens + components) and fonts/ (Bricolage Grotesque, Red Hat Mono, OFL texts)
```

## The direction in plain words

The front desk is printed as a two-colour risograph job. There are exactly two inks, **violet** and **cyan**, on a **cool white** stock. Where the inks overlap they print a deep **overprint blue**, and every line of text uses that blue instead of black. Lighter tints are halftone dot screens, not flat grey or pastel fills. The only other effect is a deliberate 2 px misregistration on the big page headings: a cyan copy sits behind violet text and multiplies to overprint blue where they overlap.

Rooms are **round key tags**. The house is a **pegboard**: one hook-rail per floor, 8 tags per rail, 64 tags in all. There is no sidebar. A masthead strip carries the hotel, the clock and the signed-in person; a horizontal nav under it holds Front desk (Today, Availability, Bookings) and Admin (Rooms, Codes, Users). Content is set like a broadsheet: a 12-column grid, thin column rules, and a thick rule over every section heading.

It is a light design for a bright daytime lobby.

## Screens

| # | Screen | Role | Signature |
|---|--------|------|-----------|
| 01 | Today | Receptionist, 10:42 | Arriving (cyan-screened sheet) and Leaving (violet-screened sheet) with Check in / Check out; the 64-tag pegboard, ink key, OOO notes and the tonight tally. **New booking** is the primary. |
| 02 | Availability | Receptionist | 16 nights × 4 types as numbered ink dots (more ink, fewer rooms); tonight as a cyan pill column; the Fri 2 → Sun 4 Family Suite selection bar with **Start booking**; the 801–808 room chart. |
| 03 | New booking | Receptionist, 10:44 | Stay, all four room types (two full on Sat 3, Deluxe too small), tags 803/807 with 807 chosen, guest, extras, AUTUMN26, and a printed docket with an 88 px key tag and the total. **Confirm booking · $919.74**. |
| 04 | Booking + rebook | Receptionist, 10:50 | HVK-2094 with Check in disabled until Thu 1 Oct, Rebook open: old stay struck, Deluxe nights strip, keep 606, three checks, Was / New / Difference. **Confirm rebook**. |
| 05 | Check in | Receptionist, 10:46 | ID match, Deluxe floors 6–7 as a pegboard where only 704, 707, 608 can be picked, the guarantee and pre-authorisation, keys and the dinner offer, 704 ARR → OCC and a round stamp preview. **Complete check-in**. |
| 06 | Check out | Receptionist, 10:58 | Folio ledger to the $489.14 balance, Visa •••• 9032 selected, the before-leaving checklist, 505 DUE → VC. **Settle $489.14 and check out**. |
| 07 | Rooms | Admin, 11:05 | Room-type ledger, Deluxe edited inline ($238 → $248, bookings keep $238), delete blocked on Family Suite, Add room, the floor map and recent changes. **Save changes**. |
| 08 | Promo codes | Admin, 11:05 | Code register with status pills, a validity timeline with today and the 7-night winter26 overlap, the New promo code form and a receptionist preview. **Create promo code**. |
| 09 | Users | Admin, 11:05 | Staff ledger (role, shift, status, last active), Create user with Receptionist / Admin role cards that list can and can't. **Create user and send invite**. |

## Tokens

All tokens live at the top of `assets/twoink.css`.

**Colour.** Every surface is ink A, ink B, overprint or paper.

| Token | Value | Role |
|---|---|---|
| `--paper` | `#F7F8FA` | Stock: page, fields, pills |
| `--ink` | `#1A1AB8` | Overprint blue. All text, rules, checked controls, selection outlines. 10.5:1 on paper |
| `--ink-2` | `#4646C5` | Overprint at 80%: secondary text. 6.7:1 on paper, 5.4:1 on the light sheet screens |
| `--ink-3` | `#5C5CCC` | Overprint at 70%: hints, placeholders, disabled text. 5.1:1, used on plain paper only |
| `--violet` | `#AA11CC` | Ink A. The single primary action per screen, DUE tags, full nights, focus ring, danger |
| `--cyan` | `#11CCFF` | Ink B. Fills, tints and halftone only, never small text. ARR tags, active status, selected states |
| `--rule` / `--rule-2` | `#C6C7EB` / `#9F9FE0` | Overprint at 22% / 40%: hairlines and field borders |
| `--scr-v30`, `--scr-c30` | dot screens | 30% violet / cyan halftone (4 px pitch, 45°) for tag rims and small fills |
| `--scr-c20`, `--scr-v13`, `--scr-c13` | dot screens | Light sheets that carry text (5 px pitch) |
| `--hatch` | cyan + violet lines | Out of order |
| `--hatch-danger` | overprint lines on violet | Danger (no red: violet solid with a crosshatch) |
| `--rim` | radial mask | Paper centre inside a screened or hatched tag, so the number always sits on clean paper |

**Type.**
- **Bricolage Grotesque** (variable: opsz 12–96, wdth 75–100, wght 200–800). Display headings at 60 px, 80% width, weight 780, with misregistration. Section heads at 24 px, 84% width. UI text at 14–15 px, 96% width. Tabular figures on by default.
- **Red Hat Mono** for codes and references only (`HVK-2094`, `autumn26`, `PRM-0014`, status codes in tags). Its zero is slashed, so 0 and O stay distinct.
- Scale: 11 / 12 / 13 / 14 / 15 / 17 / 20 / 24 / 32 / 60 px. The minimum is 11 px.

**Spacing.** 4 px base: 4, 8, 12, 16, 20, 24, 32, 40, 48. The page gutter is 32 px at 1440, 24 px at 1180 and 16 px on phones.

**Radius.** Pills and circles are the printed shapes: `--r-pill` 999 px for buttons, chips, bars and stay ranges, and 50% for tags, dots and avatars. Fields keep a soft `--r-field` of 10 px. Sheets use 3 px, like trimmed paper.

## Components (all in `twoink.css`)

- `.mast`, `.nav`: masthead strip with a double rule; horizontal nav with circle markers. The current item gets a violet dot with a cyan dot misregistered behind it. For receptionists, admin items show locked with "Admin only".
- `.mis`: the misregistered display heading (cyan copy under violet, multiply blend). Page headings only.
- `.bs` / `.col` / `.sh`: the broadsheet grid, column rules and section heads with a thick rule.
- `.sheet--c`, `.sheet--v`: screened sheets (Arriving, Leaving).
- `.tag` (+ `t-arr`, `t-due`, `t-occ`, `t-vc`, `t-ooo`; sizes `--xs` 34, `--s` 42, default 52, `--l` 88): round key tags with a punched hole. `.is-picked` adds a violet ring and a check mark.
- `.board` / `.rail`: the pegboard (perforated ground, one ink rail per floor, a hook into each tag's hole).
- `.av0`–`.av3`: availability dots. More ink means fewer rooms, and the number is always printed.
- `.btn` (`--primary` violet, `--fill` cyan, `--on` pressed, `--danger`, `--ghost`, disabled = dashed): printed pills.
- `.code`, `.pill`, `.chip-key`, `.danger-chip`, `.role-tag`: codes, status words, key chips.
- `.inp`, `.chk`, `.rad`, `.switch`, `.step`, `.seg`, `.opt`: form controls, with focus, changed (`.is-changed`), read-only, error (`.is-error` + `.err`) and disabled states.
- `.ledger`, `.tot`, `.kv`, `.tl`: tables, totals, key–value lists and history timelines.
- `.note` (`--box`, `--lock`, `--warn`, `--ok`, `--danger`): notes. The permission notes use a dashed outline and a lock icon.
- `.slug`: a printer's slug at the foot of each page, with the colour bar.

Browser surfaces are themed: cyan text selection, a violet caret and focus ring, an overprint scrollbar thumb, and tabular numerals.

## Status without colour alone

Each status is carried three ways at once: an **ink treatment**, a **pattern or shape**, and a **text code**.

| Status | Ink / pattern | Code |
|---|---|---|
| Arriving | cyan solid | `ARR` |
| In house | violet dot-screen rim, paper centre | `OCC` |
| Due out | violet solid, paper text | `DUE` |
| Vacant, ready | paper with an ink outline | `VC` |
| Out of order | cyan-and-violet crosshatch rim | `OOO` |

The key sits beside the pegboard with counts (10 / 5 / 43 / 4 / 2). The same rule applies elsewhere:
- Availability dots always print the number, and a full night also says "full".
- Chart bars carry the guest name and code.
- Promo and staff statuses are words in pills (Active, Scheduled, Used up, Expired; Active, Invited, Deactivated).
- Disabled rooms at check-in keep their code and a caption ("In house", "Out of order") on a dashed, un-inked tag.
- Blocked actions are dashed pills with the reason printed next to them.

## Permissions made visible

- Receptionist nav: Rooms, Codes and Users are shown but locked, marked "Admin only".
- New booking: "Codes are created by admins. You can apply an existing code but not create one."
- Booking: Check in is disabled with "From arrival day, Thu 1 Oct".
- Rooms: Delete is disabled on every type with bookings. Family Suite prints the reason: 14 upcoming bookings and 7 rooms occupied tonight.
- Rooms: the price edit says existing bookings keep $238.
- Users: the role cards list what a receptionist can and can't do, and what an admin can do.

## Synthetic data: replace before any real use

All data is invented and must be replaced. That covers the hotel name ("Alder House"), guest and staff names, phone numbers (555 numbers), emails (`example.com`, `alderhouse.example`), card endings and booking references.

## Open decisions (not in the brief)

1. **The promo Offer field.** The brief lists id, code, title, date range and count. The designs add an **Offer** (for example "15% off room nights", "7th night free"), because a code needs a value. The discount model needs to be confirmed.
2. **Extras prices** are placeholders: breakfast $18 and dinner $42 per guest per night, and arrival pickup $55 per trip.
3. **Tax.** A flat 12% is a placeholder.
4. **Room prices and counts.** Queen $136, Twin Double $166, Deluxe $238 and Family Suite $366, with 24 / 16 / 16 / 8 rooms, are placeholders.
5. **One promo code per booking** is assumed in the overlap warning and on the booking form.
6. **Admins at the desk.** The admin nav can open Today, Availability and Bookings. The brief doesn't say whether admins can run front-desk actions.

Icons are from [Lucide](https://lucide.dev) (ISC licence), embedded as an inline SVG sprite per page. The stamp, the brand mark and the key tags are drawn in CSS/SVG. Fonts are self-hosted under the SIL Open Font License (see `assets/fonts/`).
