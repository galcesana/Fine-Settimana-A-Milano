## Quick repository guidance for AI coding agents

This repository is a small static website for a trip (Milan, Dec 2025). The project is intentionally simple: HTML, CSS, tiny inline JS, and external assets loaded via CDN. Use the instructions below to make focused edits that match the project's conventions.

### Big picture
- Single-page static site: `index.html` is the canonical source of truth. There is no build tool or server code. Edits are made directly to HTML/CSS/JS in `index.html` and content in `README.md`.
- Deployment: via GitHub Pages; updating the repo (push to `main`) will publish changes.

### Key files and patterns (examples)
- `index.html` — everything is here: header, sections (`#map`, `#schedule`, `#flights`, `#tickets`, `#info`, `#transport`, `#checklist`, `#notes`) and a bottom sticky nav.
  - Map: the Google MyMaps embed is in the iframe at `section#map` (replace `iframe.src` to change the map).
  - Schedule: day cards are `.card` elements inside `section#schedule` — add or copy a `.card` block to add days.
  - Flights: PNR and placeholders live in `.flight-value` and `editable-placeholder` spans (e.g., `ZM16VM`).
  - Interactive behaviour: small inline script at the end handles checklist checkbox toggling and nav active state. Notes are intentionally non-persistent (`* Notes are temporary and clear on refresh.` in the UI).

### Styling & UI conventions
- Mobile-first, responsive design: `.container` max-width is `800px` and there is a bottom sticky nav (`nav.bottom-nav`) that must remain accessible on small screens.
- CSS variables at the top (`:root`) control colors and sizes — prefer modifying variables for global theming instead of hardcoding colors.
- Reuse existing classes (`.card`, `.event-item`, `.editable-placeholder`) rather than introducing many new utility classes.

### JavaScript and behavior
- Keep JavaScript minimal and inline (current script at bottom). If you add new behaviors, prefer plain DOM API to avoid adding heavy dependencies.
- Checklist: toggling only changes DOM classes; it does not persist to storage. If you add persistence, clearly document it and add a small, opt-in feature (e.g., localStorage) and keep default behavior unchanged.
- Navigation active state uses scroll position and `scrollIntoView` on nav items — don't remove or impair this logic unless you update the scroll offsets consistently.

### What NOT to assume
- There is no build step (no package.json, no bundler). Do not add complex build tooling unless the user explicitly requests it.
- No backend or API exists — do not introduce server-side assumptions.

### Typical small tasks and examples (how to edit safely)
- Update flight times: edit the relevant `.flight-value` spans in `section#flights` (search for PNR `ZM16VM` to find block).
- Add a day to schedule: copy a `.card` group inside `section#schedule` and change `schedule-date` and `event-item` contents.
- Replace the map: update the `iframe` `src` in `section#map` with a new Google MyMaps embed link.
- Change theme color: adjust `--primary` or `--accent` in `:root` in the `<style>` block.

### Commit & PR guidance
- Commit small, atomic changes with a one-line summary (e.g., `Update flight times in index.html`, `Add schedule card for 26/12`).
- If a change impacts layout or navigation behavior, include a short screenshot or description in the PR to help reviewers validate mobile behavior.

### Where to look for more context
- `README.md` — describes purpose and that site is deployed on GitHub Pages.
- `index.html` — main source to edit; it contains both styles and the tiny JS.

If any section here is unclear or you'd like me to expand examples (e.g., how to add a small localStorage persistence for the checklist), tell me which area to expand.
