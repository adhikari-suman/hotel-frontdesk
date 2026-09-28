# Design 9: Bedside Clock

The front desk is designed as a bedside alarm clock, or any small LCD appliance. The housing is light matte plastic, and data sits in backlit blue LCD windows set into it. Every number that matters (times, room numbers, counts and money) is a seven-segment readout, with faint "ghost" 8s behind the lit segments, the way a real LCD shows its unlit segments. An acid-lime LED marks whatever is active. Navigation is a row of rubber keys along the bottom edge.

The desk works by day, so the housing is light rather than a dark night-stand panel. The theme sits in the details: segment numerals, annunciator labels and LED dots. Clocks, bezels and speaker grilles aren't drawn on every panel. There are only two surfaces, housing and windows.

## Topology

- **Device face (top).** A raised strip of housing holds the wordmark and a big LCD clock (for example 10:42, with day annunciators MO–SU where SU is lit, and 27 SEP 2026). Beside it are a secondary readout (Sold tonight 53 of 64 · 83%), the find field (an LCD entry window) and the signed-in user with a sign-out key.
- **Main.** The page title and meta sit on the housing, with the screen's one lime key when it belongs in the header. Content lives in LCD windows. Each window has a silk-screened legend above it (an `h2` in caps), not a card header.
- **Key row (bottom, fixed).** It has two groups of rubber keys, each with a printed label: **Front desk** (Today, Availability, Bookings) and **Admin** (Rooms, Promo codes, Users). Each key has an LED dot, and the current page's key is pressed in with its LED lit. On receptionist screens the Admin keys are dashed and carry a lock icon, and the group label reads "Admin · admins only".
- **Soft keys.** Where a list needs a per-row action (Check in, Check out, Remove/Add extra, Edit/Delete room type), the rows are glass and the keys sit beside the window on the housing, aligned row for row, like the soft keys next to an appliance screen.

## Tokens

### Colour

| Token | Hex | Role |
|---|---|---|
| `--housing` | #E3E5E4 | Page ground, matte plastic |
| `--housing-raised` | #ECEEED | Device face, save bar |
| `--housing-shade` | #C9CCCB | Key-row strip |
| `--housing-seam` | #B9BEBC | Molded grooves and seams (with a #FAFBFB highlight below) |
| `--ink` | #1A2427 | Printed legend on the housing |
| `--ink-2` | #4A5452 | Secondary legend (6.2:1 on the housing) |
| `--lcd` | #BDE8F1 | Backlit LCD window (from #88DDEE) |
| `--lcd-off` | #CFD6D4 | Unlit glass: vacant rooms, full nights |
| `--seg` | #0E2A33 | Lit segments and all text on glass (11.4:1 on `--lcd`) |
| `--seg-2` | #2F5562 | Secondary text on glass (6.1:1) |
| `--ghost` | rgba(14,42,51,.095) | Ghost 8s and unlit annunciators |
| `--lime` | #DDEE22 | LED: active, selected, primary key face (#0E2A33 text, 11.7:1) |
| `--lime-soft` | #CCEE88 | Selected glass: a chosen room, selected nights, the row being edited |
| `--lilac` | #BB88DD | Reserved and scheduled (#0E2A33 text, 5.5:1) |

There is no red. Warnings use a heavy #0E2A33 frame, a triangle icon and the light segment hatch instead of an alarm colour.

### Type

- **DSEG7 Classic Bold** (keshikan/DSEG, OFL) for numerals: the clock (60 px), money totals (28–40 px), room numbers (17–21 px), counts and times (12.5–17 px). Each readout is `<span class="sg" data-g="88:88">10:42</span>`. The ghost is the same string with every digit mapped to 8, drawn with `::before` at 9.5% alpha (`content: attr(data-g) / ""`, so screen readers skip it). `!` is DSEG's all-off digit and is used for leading blanks, so counts line up in fixed-width readouts. Commas and `$` are set in Chivo, because a segment display has no comma.
- **Chivo** (variable, 100–900) for all UI text: 28/800 page titles, 18/750 form section heads, 13/800 caps +0.12em window legends, 14–15/400–700 body, 11/800 caps annunciators. Nothing is set below 11 px.
- **Chivo Mono** for promo codes (`autumn26`), booking refs (`HVK-2094`) and promo ids.
- Tabular numerals are on globally. DSEG is monospaced by construction.

### Spacing, radius and depth

- Spacing steps: 4, 8, 12, 16, 20, 24, 32. Columns sit 24 px apart, stacks 22 px, window padding 16–22 px, and grooves have 22 px above and below.
- Radius: key 11 px (13–14 px for large keys), LCD window 12 px, entry field 8 px, room cell 6 px, annunciator 3 px.
- Depth: windows are recessed, with a 1 px edge in segment ink at 34%, a neutral `inset 0 2px 5px` shadow and a 1 px housing highlight below. Keys are domed (a top highlight plus a soft, offset drop shadow), and a pressed key moves down 1 px and takes an inset shadow. There are no hard offset shadows. Cell and selection frames are outlines, not shadows.

## Components

- `.lcd` is a window, `.lcd--off` is unlit glass, and `.lcd-rule` is a divider.
- `.sg` (plus `--xxl` to `--xs`) is a segment readout with ghost digits. `.money` wraps `$` and the segments.
- `.ann` is an annunciator label, the LCD icon glyph. Variants: `--solid` (reversed), `--lilac`, `--lime`, `--dash`, `--hatch`.
- `.key` is a rubber key. Variants: `--primary` (lime-lit), `--lg`, `--xl`, `--sm`, `--xs`, `--icon` and `--quiet`, plus `[aria-pressed]` and `[disabled]` (dashed and flat). `.nkey` is a key-row key. `.led` / `.led--on` is the LED dot. `.tog` is a toggle key with its own LED.
- `.input` is an entry window. Variants: `--focus` (2 px #0E2A33 ring plus a drawn caret), `--changed` (lime glass), `--error` (heavy frame and hatch), `--ro` and `--mono`. `.stepper` pairs − and + keys with a segment readout.
- `.rc` is a room cell, with `--occ`, `--arr`, `--due`, `--vac`, `--ooo`, `--sel`, `--pick` and `--dim`. `.floor` is one row of the 8 × 8 matrix.
- `.softlist` is a glass list with the soft-key column beside it. `.lines` / `.line` is the receipt readout. `.ltable` is a table on glass. `.segbar` is a segment bar with one segment per room. `.note` and `.plate` are permission and terms notes. `.hist` is history. `.checks` is a checklist.

## Status without colour

Each room state has a code, a surface and, where it helps, a pattern, so it reads in greyscale.

| State | Annunciator | Surface |
|---|---|---|
| Arriving | **ARR**, reversed (solid) | Lilac glass |
| In house | **OCC**, outlined | Plain backlit glass |
| Due out | **DUE**, outlined, light on dark | Inverse LCD (dark cell, light segments) |
| Vacant | **VAC**, outlined | Unlit grey glass, "Ready" |
| Out of order | **OOO**, reversed | Unlit glass with a hatch of diagonal segment shapes, plus the reason and return date |

Elsewhere:

- Promo codes: Active has a lit LED and a solid "Active" label. Scheduled has a lilac label. Used up is hatched. Expired has a dashed label.
- Users: Active has a lit LED and the word Active. Invited has a lilac label. Deactivated is hatched, with the name struck through.
- A full night shows "0" with a FULL label on unlit glass.
- Selection always adds a 2–3 px #0E2A33 outline and an LED, not just lime.
- Disabled keys are dashed and flat. Permission locks add a lock icon and a sentence that names the rule.

## Permissions made visible

- The Admin key group is locked, with a lock icon, on every receptionist screen.
- The promo field on New booking reads "Codes are created by admins. You can apply a code here but not create one."
- On Rooms, Delete is disabled with a lock. For Family Suite the reason is spelled out ("14 upcoming bookings and 7 rooms occupied tonight"), and a rule note sits under the table.
- The Deluxe price edit states that the 23 upcoming bookings keep $238.
- On Users, the role cards list what a receptionist can and can't do, and what an admin can do.
- On the booking screen, Check in is disabled until arrival day ("Opens on arrival day, Thu 1 Oct").

## Open decisions

- **Offer on promo codes.** The brief defines id, code, title, date range and usage count, but no discount. The "Offer" column and field (15% off room nights, 7th night free, and so on) are placeholders until the client says how a code's value is defined.
- **Placeholder figures.** The 12% tax, the extras prices (breakfast $18 per guest per night, dinner $42 per guest per night, pickup $55 per trip) and the room prices are demo values.
- **Deleting a room type** is shown as blocked whenever bookings exist. What happens to a type with no bookings (delete, or archive) is undecided.
- **Nav home for check-in and check-out.** They light the Today key, because both start from the Today queues. A dedicated Bookings search isn't designed.
- **Fixed key row.** It sits over the page bottom (the body is padded for it). On small screens it scrolls sideways rather than collapsing into a menu.
