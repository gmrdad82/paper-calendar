# paper-calendar — plan `plugin`

Prefix: WK
State: parked
Parked: 2026-09-20 — The calendar plugin (WK-16's plugin half), parked with Paper.

## Decisions
1. A plan is bound to one repository (his ruling 2026-09-20); a two-repository
   card of the split became one card per repository, the desk's half
   waiting on the plugin's as `<repo>/<ID>`.
2. Dependencies on retired cards (WK-18, SH-15) are dropped; dependencies
   on landed cards are dropped; IDs are kept so history and commits read
   true.
3. The plan's state is `parked` — its cards are not offered until `dispatch plan --resume`.

## Left open
- Every card's Context was true at the split book's writing; a session
  re-reads the tree at resume and notes what moved.
