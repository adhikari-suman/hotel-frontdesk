---
version: 1
slug: "designs-index-html"
primary_target: "designs/index.html"
related_targets: ["designs"]
---

# Surface brief: Front desk design exploration (10 directions × 9 screens)

**Scope.** Ten alternative visual directions for the single-hotel front-desk web app. Mode: Operate. Each direction covers the same 9 desktop screens with identical content, as static HTML/CSS plus PNG @2x:
- today
- availability
- new booking
- booking + rebook
- check in
- check out
- rooms
- promo codes
- users

Deliverable: `designs/` (index.html compares all ten; each `design-N/` has an index, a README with tokens, assets, screens and PNGs). Call logs were dropped from the brief on 28 Sep 2026.

**Direction source.** Pinned by the user. Each direction was derived from its own private random seed string, which is never shown. The concept-seed roll ran once (key 1e63daff); the user's method outranks it.

## Directions
1. **The Rack:** colour slips in a steel room rack; printed registration cards. Archivo and JetBrains Mono.
2. **Two-Ink Print:** a violet and cyan risograph job with round key tags. Bricolage Grotesque.
3. **Pool Lanes:** motor-lodge modern with vertical swim lanes and a marigold primary action. Jost.
4. **Noughts & Crosses:** a Swiss 3-module grid with O/X status marks and lavender selection. Schibsted Grotesk.
5. **Reservation Book:** a two-page ruled spread on navy cloth, with a plum ribbon and edge tabs. Petrona and Figtree.
6. **Night Console:** dark and keyboard-first, with a ⌘K bar, one queue and hot-pink focus. Geist.
7. **Mirror:** bilateral symmetry, a pink ↔ green diptych and aubergine ink. Bodoni Moda and Red Hat Text.
8. **Lift Panel:** lift-panel navigation, ▲ green / ▼ amber and corridors of doors. Onest and Doto.
9. **Bedside Clock:** LCD windows, DSEG7 numerals and a rubber-key nav row. Chivo.
10. **Whiteprint:** a diazo drawing sheet, rooms as plans, a title block and a sheet index. Saira and Public Sans.

## Shared contract
- Status is never shown by colour alone.
- Exactly one committing action per screen.
- Permissions are visible where they matter.
- The data is identical across designs. Offer, tax and extras prices are placeholders.

## Status
- Design-1 passed an independent finish review: 8/8 fixes resolved, plus 3 follow-ups fixed.
- Designs 2–10 were self-reviewed by their builders, run through the detector and cross-checked for data consistency. They have NOT had an independent finish review.
- DESIGN.md is deferred until the team picks a direction; then run `/impeccable document` on the chosen design.

FINISH: unreviewed and undocumented is unfinished; this build ends with the finish review, the verdict, DESIGN.md, and every shipping raster carrying its provenance
