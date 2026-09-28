# Design 8: Elements

**Idea.** The hotel as its own periodic table. Every room is an element tile: the room number sits where the atomic number would, a two-letter mixed-case status symbol takes the centre, and the guest is the element's name. Navigation is a row of element tiles, with the admin screens split off as a separate series. A booking is an enlarged element card whose symbol is the guest's initials. The folio is also written out as a formula.

Open `index.html` for the gallery. The screens are in `screens/`, and the @2x screenshots are in `png/`.

## Tokens

| Token | Hex | Meaning |
|---|---|---|
| `--ink` carbon | `#1F2330` | Text, active nav tile, selected room, current step |
| `--pri` violet | `#5B45C8` | The single primary action on each screen, focus, the brand tile |
| `--oc` lilac / `--oc-ink` | `#DCD6F6` / `#3F2F95` | **Oc**, occupied; the availability scale (4 lilac steps) |
| `--ar` cyan / `--ar-ink` | `#C3E7F4` / `#0B6F96` | **Ar**, arriving; receptionist role (**Re**) |
| `--dp` apricot / `--dp-ink` | `#F8DDB6` / `#9A4E08` | **Dp**, departing; "low" availability; balance due |
| `--oo` rose / `--oo-ink` | `#F6CDD3` / `#B0243A` | **Oo**, out of order (always hatched); destructive actions; errors |
| `--ok` green / `--ok-ink` | `#CFEBD6` / `#22693A` | Active codes, completed steps, discounts |
| `--adm` pink / `--adm-ink` | `#F3D9E6` / `#8A2C5C` | The admin series (Rooms, Promo codes, Users) and the **Ad** role |
| `--ground` | `#F4F5F8` | Page ground |
| `--ground-2` | `#EBEDF2` | Detail column (left) |
| `--rule` | `#D3D6DF` | 1px rules |

Vacant (**Va**) is a white tile with a dashed rule, so it reads as "empty".

## Type

- **Geologica** (300–800, variable): symbols, room numbers, headings and all figures. Heavy (650) at tight tracking for symbols.
- **Public Sans** (400–800, variable): interface and body text.
- Both fonts are self-hosted in `assets/fonts/` (latin and latin-ext woff2) under the SIL OFL. The licence files are included.

## Components

- **Element tile** (`.el`): number at the top left, a two-letter symbol, and the name. It is used for navigation, the hotel mark and the signed-in user (Re or Ad).
- **Room tile** (`.room`): the room number and type letter (Q/T/D/F), the status symbol, and the guest or the reason the room is off sale. The fill shows the status family.
- **Key tile**: an annotated example tile that doubles as the legend on Today.
- **Symbol chip** (`.sym`): a two-letter status symbol used everywhere: Va Oc Ar Dp Oo for rooms, Ac Ex Sc Fu for codes, Re Ad for roles, Ac In Of for accounts.
- **Stat tiles** (`.stat`): the counts in the left detail column.
- **Element card** (`.ecard`): the booking context in the left column. The guest's initials are the symbol and the face colour follows the stage (violet draft, cyan arrival, apricot departure).
- **Formula** (`.formula`): the folio total written as arithmetic.
- **Availability matrix**: room types × 14 nights. It uses a sequential lilac scale, apricot "Low", hatched rose "Full" and an ink selection with a bracket.
- Standard pieces: panels, tables, fields, steppers, steps (for real sequences only), and a timeline (for history only).

## Layout

- The top header is a row of element tiles: brand, desk series 01–06, a gap labelled "Admin", then admin series 07–09, followed by search, the date and time, and the user tile.
- Below it is a 300px left **detail column** that holds the enlarged context (tonight's stats, the booking card, the inventory), with main content on the right.
- The layout is desktop-first at 1440px.

## Rules

- **Status is never shown by colour alone.** Every status carries its two-letter symbol, and out of order is also hatched.
- **Each screen has one primary action** (violet, solid). Everything else is an outline or ghost button.
- **Destructive actions are rose-outlined.** The final confirmation is solid dark rose and names the consequence ("Cancel booking and charge $226.58", "Delete room 116").
- **Permissions are always visible:**
  - Receptionists see the admin tiles locked and hatched.
  - Promo codes are "apply only" for receptionists.
  - Admin screens carry a pink admin note.
  - Users includes a role × permission matrix.
- **Delete is blocked while bookings exist**, and the screen gives the reason: disabled Delete buttons on room types, a note for Family Suite, and a confirm strip for room 116, which has no bookings.
- **Borders are 1px throughout.** There are no side-stripe accents and no thick borders on rounded shapes. Emphasis comes from a tint or an ink fill.
- **Text is at least 11px.**

## Open decisions and placeholders

- **Promo "offer":** the brief doesn't define what a code gives. The "15% off room nights", "10% off" and "7th night free" values are placeholders, as is the Offer field on the create form.
- **summer2026 vs a 14 Oct stay:** the code's range (1 Jun–30 Sep) doesn't cover the hero booking. We read the date range as the *booking window*: the rate was quoted on 22 Sep (quote Q-2609) and is honoured. On the rebook, the added night is at full price. This needs a product rule.
- **Tax:** the 12% is a placeholder, applied to rooms and extras after the discount.
- **Cancellation and rebook terms** (48 hours, first night charged) are placeholders.
- **Check-out timing:** the check-out screen is shown on the hero's departure day (Sat 17 Oct, 10:48). The other receptionist screens are set on Wed 14 Oct. The folio includes the dinner that was added at check-in (Thu 15 Oct, 2 guests), which brings the total to $956.37 instead of the booking's $862.29.
- **Extra synthetic data:** room-type layout by floor, extra guest surnames for density, balances, and staff "last active" times are all synthetic. The six extra arrival and departure names beyond the canonical ten are also synthetic.
- **Card and ID details** are synthetic placeholders: Visa ending 4242, passport ••••• 4127.
