# Kneuron (dev fork)

Chrome MV3 extension enhancing the Knack Builder. No build step, no npm — edit files directly. Core logic lives in `Kneuron.js` (~all features); small helpers: `popup.js`, `page-script.js`, `drag-block-*.js`.

## Remotes — INVERTED naming (verify before pushing)
- `origin` = upstream `cortexrd/Kneuron`. `fork` = our fork `ivojolo/Kneuron`.
- Push feature branches to `fork`; open PRs against `origin` (cortexrd).

## Fragile code
Read `DEVNOTES.md` BEFORE touching sidebar, filter, or density code. The vue-recycle-scroller overrides (`kneuron-dense` class, `fixScrollerPool` timing) break easily.

## Test loop
Load unpacked at `chrome://extensions` (once). After each change: reload the extension there, then refresh the Knack Builder tab.

## Engineering standard

Optimize for the best outcome, not the least effort. When making a technical decision, don't let development cost, effort, or token budget push you toward a worse solution: if the right approach is harder or longer, take it and see it through. Match complexity to the actual problem and prefer robustness and long-term maintainability, without over-engineering or adding unrequested scope.

## Deleting records or data

Never from a filter or query, never in the same run as anything else, never test data by default. Print the exact
ids, save a before-state (the items AND whatever links to them from the other side), get Ivan's approval, then delete
in a separate run and verify by an independent path. Canonical rule: `C:\code\AGENTS.md` "Deleting records or data".
Knack addendum and the enforcing tool (`safe-delete-records.js`): `C:\code\KnackApps\AGENTS.md`.
Origin: Belmont CRM incident 2026-09-17, 48 records lost to a silently ignored filter.
