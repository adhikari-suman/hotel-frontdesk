# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Stack

Static HTML/CSS for the design phase. Each screen is a self-contained HTML page exported to PNG, kept together in one folder (`designs/`) so the whole set can be committed and handed to the developer. The production framework is not decided yet.

## Users

- **Receptionist** (the brief also says "specialist"; this record treats them as the same role). Works the front desk through a shift, usually with a guest standing at the counter or on the phone. Their jobs: make a booking, rebook, check in, check out, cancel, add extras (dinner, arrival pickup, breakfast), and apply a promotion code.
- **Admin.** Runs the property's setup and oversight. Their jobs: create users, view call logs, add, update and delete rooms, and create promotion codes.

## Product Purpose

A front-desk SaaS for a single hotel. It turns the desk's daily loop (arrivals, stays, departures) into fast, low-error actions, and it keeps inventory, pricing and promotions under admin control.

## Operating Context

- One property with about 60–90 rooms across the four room types. Currency is USD.
- Receptionists act in real time, often while a guest is waiting, so speed and certainty come before exploration.
- Admin work is occasional and deliberate: configuring rooms and promotions, managing staff, reviewing logs.

## Capabilities and Constraints

- **Roles:** Receptionist and Admin. Permissions are strict:
  - Only Admin can add, update or delete rooms, create users, and create promotion codes.
  - Receptionists can apply existing promotion codes but cannot create them.
- **Booking actions (Receptionist):** make, rebook, check in, check out, cancel, add extras.
- **Extras:** dinner, arrival pickup, breakfast.
- **Room:** has a type (Deluxe, Twin Double, Family Suite, Queen), a price and a count (inventory of that type).
- **Promotion code:** has an id, a code identifier (e.g. `summer2020`), a name or title (e.g. "Summer 2020"), a required date range, and an optional usage count.
- **Call logs (Admin):** two things.
  - Phone call logs: inbound or outbound, guest or room, duration, handled by, outcome.
  - A staff activity trail: who did what in the system.
- **Open decisions:** production framework, payment processing, channel manager / OTA integration, and hotel name and brand.

## Evidence on Hand

No real guest data, hotel brand, photography or metrics exist yet. All names, bookings and figures in the designs are synthetic and must be replaced. Do not invent a hotel brand claim, customer or benchmark.

## Product Principles

1. **The guest at the counter sets the pace.** Every receptionist action should finish in the fewest decisive steps, and the current state is always visible.
2. **Permissions are visible, not hidden.** A role's limits show up clearly in the interface, so nobody hits a dead end.
3. **Inventory is truth.** Room counts, availability and promo validity are shown exactly, never approximated.
4. **Reversible where possible, explicit where not.** Cancel, delete and checkout confirm what changes.
