# WK-16 — Plugin: Calendar and reminders

Wave: 1 · Run: single · Depends on: none · Complexity: **
Branch: split-wk-16 · Base: main

## What
The book (section 6): "Calendar and reminders (dates on Pages, a month panel, desktop notifications)". His dump of 2026-09-12 named it as a plugin idea: "some kind of calendar, like maybe being able to set up calendar events and reminders for some specific things". The desk knows no dates beyond a Page's own timestamps;

## How
1. **The plugin crate.** `pito-plugins/plugins/calendar/` from the template: `plugin.toml` (id `calendar`, name "Calendar", version `0.1.0`, host `work`, capabilities `core:read` and `notify`; nothing else — it never writes a Page), `Cargo.toml`, `src/lib.rs` exporting `panel`, `sheet`, `command`, `settings`.
2. **The date grammar** (`src/dates.rs`): `@YYYY-MM-DD` and `@YYYY-MM-DD HH:MM` anywhere in the body outside fenced code; a ` ```when ` block with lines `YYYY-MM-DD[ HH:MM][ — label]`;
3. **The panel.** For the open Page: one row per date (date, time, label, the reminder state: none, armed at lead time, raised) and a "Remind me" button per row. Empty when the Page has no date (the host draws no panel).
4. **The month sheet.** `sheet`: a month grid (the week's first day from settings, Monday by default), each day cell listing the dated Pages of the active Notebook by display key and title (`core:read` list of Pages, then the grammar over each body; cache by Page `updated_unix` so an unchanged Page is not re-parsed);
5. **Reminders** (`src/remind.rs`): armed reminders live in the host's per-plugin key-value storage keyed by Page id and date; the lead time from settings (default 30 minutes;
6. **The command.** `command` "Remind me…" on the open Page: arms the Page's next date (or the only one); if the Page has no date, the notice says so.
7. **Settings page.** Lead time (minutes), first day of the week; stored in the plugin's storage.

## Guards
- Do not touch: - The host, the slots and the tree renderer (`pito-work/src/plugins/*`): WK-13's. - The desk's notice and toast mechanics: the plugin reaches them only through `notify`.
- Gate: the project's gate
- Accept: The grammar tests cover every form of step 2 including the ignored cases (test names in the runbook).
- Accept: The schedule test proves the next wake and the missed set from a fixed "now" (step 8).
- Accept: US-3: the notice appears at the due minute, once (the capture and the ceremony log's timestamp against the armed time, within one minute).
- Accept: US-4: a missed reminder raises once and never again (two captures).
