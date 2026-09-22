# WK-16 — Plugin: Calendar and reminders

Wave: 1 · Run: single · Depends on: none · Complexity: **
Branch: split-wk-16 · Base: main

## What
Dates in an Idea's body feed a month sheet and armed reminders that raise a desktop notice once.

## How
1. The plugin crate: `core:read`, `notify`.
2. `src/dates.rs`: the date grammar; `src/remind.rs`: armed reminders in plugin storage.
3. The panel, the month sheet, the "Remind me" command, the settings page.

## Guards
- Do not touch: the host, the slots, the desk's notice mechanics.
- Gate: the project's gate
- Accept: grammar tests cover every form; a missed reminder raises once.
