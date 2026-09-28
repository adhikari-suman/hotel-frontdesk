# Design 5 — Drawing Set

**Idea:** the front desk as a set of architect's drawing sheets. Today is a floor plan of the four floors, with walls, a corridor and door swings. Stays are dimension lines across nights. Warnings and blocked actions are revision clouds. Navigation is the sheet index in a title block on the right edge of every sheet.

Open `index.html` for the gallery. The screens are in `screens/`, and 2× screenshots are in `png/`.

## Layout and navigation
- **Frame:** a drawing sheet on a grey drafting-table surround. The sheet has a double border, zone ticks along the top edge and a faint 8px/40px trace grid.
- **Title block (right edge, 212px, sticky):** hotel mark (north arrow), then the sheet index (nav), search, "Drawn by" (the signed-in user and role), date and shift, and a large sheet number.
  - Desk sheets are **A-01…A-06**. Admin sheets are **S-01…S-03**.
  - For receptionists, S-sheets are greyed out with a lock, and a note says rooms, codes and users are managed by admins.
  - For admins, S-sheets are unlocked, and the group carries an "Admin · you" tag.
- **Sheet body:** a header with the title (Josefin Sans light plus a semibold key phrase) and a double rule below it. The content uses an asymmetric main column and a 380–420px aside. There is no left rail and no top tab bar.
- **Details:** every panel is a numbered detail with a circle callout bubble showing the detail number over the sheet number, and a thick-and-thin underlined title.

## Tokens
| Token | Hex | Meaning |
|---|---|---|
| `--sheet` | #FFFFFF | Work surface |
| `--table` | #D5D9D7 | Surround behind the sheet |
| `--grid` / `--grid-fine` | #DCEFF5 / #EEF6F9 | Trace grid |
| `--ink` | #262A33 | Text, walls, rules |
| `--ink-2` / `--ink-3` | #5A606B / #8A919B | Annotation / disabled |
| `--pen` | #17617C | Cyanotype pen: primary action, in-house rooms, dimension lines |
| `--cyan` (highlighter) / tint | #D9A800 / #FFF3B0 | Selected range, current booking — like a highlighter on a print |
| `--olive` (leaf, text #2F6B17) | #4E9A2E | Free / ready / active / discounts |
| `--teal` (rose, text #962C5C) | #B0386F | Arrivals, Check in, receptionist tag |
| `--violet` | #5544C8 | Departures, Check out |
| `--red` (text #B42A21) | #D2352B | Destructive, out of order, blocked, required marks |

## Type
- **Josefin Sans** (300/400/600/700): geometric architectural lettering. It is used for sheet titles, big figures, room numbers, detail titles, buttons and codes.
- **B612** (400/700): a legible screen face for body text, tables and forms, at a minimum of 11px.
- The fonts are self-hosted in `assets/fonts/`, with the OFL licences alongside.

## Components
- **Plan-view room board:** 16 rooms per floor, split 8 and 8 across a corridor, with door-swing arcs. Each room cell shows its number, type, guest or state, and a status mark.
- **Status marks:** each status has a shape and a word, so colour is never the only signal.

  | Status | Mark |
  |---|---|
  | In house | ■ |
  | Arriving | ▲ |
  | Due out | ▼ |
  | Ready | ○ |
  | Out of order / repair | hatched square |
  | Scheduled | dashed ○ |
  | Expired | struck square |
  | Limit reached | red ▲ |

- **Dimension line:** a date range with tick ends and a label ("3 nights · 14 → 17 Oct"). It appears on availability, booking, rebook (current range ghosted, new range in pen), check-out and the promo timeline.
- **Revision cloud:** red for destructive or blocked actions (cancel terms, delete blocked while booked) and blue for information (price change, required end date, admin rule).
- **Schedules:** drawing-style tables with a heavy outer border, hairline cells and a double-ruled total.
- **Availability matrix** plus a "Section" view of occupancy by night, drawn with a sell-out line.
- **Promo code timeline:** each code's required window is a dimension line on a month ruler, with a "Today" marker.
- **Permissions matrix:** locked cells are hatched and say "Admin only".

## Rules
- Each screen has one solid cyanotype-blue primary button, with an offset shadow. Secondary buttons are outlined in graphite. Destructive buttons are outlined in red, and blocked ones are greyed with a lock.
- The minimum text size is 11px. Numbers use tabular figures.
- Receptionists apply promo codes but never create them. The UI says so on A-03, A-04 and in the title block.
- Rooms can't be deleted while booked. S-01 shows the disabled Delete and a cloud explaining why and what to do.

## Screens
| Sheet | File | Role |
|---|---|---|
| A-01 | 01-today | Receptionist |
| A-02 | 02-availability | Receptionist |
| A-03 | 03-new-booking | Receptionist |
| A-04 | 04-booking-rebook | Receptionist |
| A-05 | 05-check-in | Receptionist |
| A-06 | 06-check-out | Receptionist (shown on departure day, Sat 17 Oct) |
| S-01 | 07-rooms | Admin |
| S-02 | 08-promo-codes | Admin |
| S-03 | 09-users | Admin |

## Open decisions and placeholders
- **Promo "offer" is undefined.** "15% off room nights" is a placeholder. The create form has an Offer field marked as pending pricing rules.
- **summer2026 has expired, but the hero booking uses it.** Its window ended 30 Sep, and the booking is being made or served on 14 Oct.
  - We show the code as honoured because the phone quote was made on 28 Sep.
  - Product needs to decide whether a code's date range applies to the booking date or the stay dates.
- **Cancellation terms are a placeholder:** free until 48 h before arrival, and the first night after promo plus tax is charged after that ($226.58 for the hero).
- **Tax** is 12% on room plus extras after the discount. This is a placeholder.
- **Incidentals hold** of $150 at check-in is a placeholder.
- **Check-out date:** A-06 is shown on 17 Oct (departure day), while every other sheet uses "today" = 14 Oct.
- **Admins can also do receptionist work.** The permissions matrix assumes this, and it needs confirming.
- **Assumed extras.** Guest names beyond the canonical ten (for other occupied rooms), the room-number layout per floor, per-night availability counts, and the draft "Accessible Queen" type and "spring27" code are illustrative synthetic data.
